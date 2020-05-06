---
layout: 		post
title: 			"数据结构"
subtitle: 		'栈和队列'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

> 栈和队列是在线性表的基础上增添了一些规则的产物，同样有顺序存储与链式存储的形式。

## 栈
> 栈是限定仅在表尾进行插入删除操作的线性表

我们把允许插入和删除的一端称为栈顶，另一端称为栈底，是一种先进后出的线性表。

#### 抽象数据类型
```
ADT 栈(stack)

Data
	同线性表。元素具有相同类型，相邻元素有前驱和后继的关系

Operation
	InitStack(*S):初始化操作，建立一个空栈S。
	DestroyStack(*S):若栈存在，则销毁它。
	ClearStack(*S):将栈清空。
	StackEmpty(S):若栈为空，返回true，否则返回false。
	GetTop(S,*e):若栈存在且非空，用e返回S的栈顶元素。
	Push(*S,e):若栈S存在，插入新元素e到栈S中并成为栈顶元素。
	Pop(*S,*e):删除栈S中栈顶元素，并用e返回其值。
	StackLength(S):返回栈S的元素个数。

endADT

```

#### 栈的顺序存储结构
这里使用了动态分配的方法，init的时候要传入栈区的大小。
```c
typedef int ElemType;

typedef struct Stack {
	ElemType *top;
	ElemType *base;
}Stack;

void init(int size,Stack* s) {
	s->base = (ElemType *)malloc(size * sizeof(ElemType));
	s->top = s->base;
}

void push(Stack* s,int i) {
	if (s->top-s->base==4) {
		printf("栈满");
	}
	else {
		*(s->top) = i;
		(s->top)++;
	}
}

int pop(Stack* s) {
	if (s->top==s->base) {
		printf("栈空");
		return -1;
	}
	(s->top)--;
	return *(s->top);
}
```

#### 栈的链式存储结构
链式结构中，除栈顶外，栈中的元素都指向它下面的一个元素。
```c
#include <stdio.h>
#include <stdlib.h>

//状态
#define OK 1
#define true 1
#define ERROR 0
#define FALSE 0
typedef int Status;

typedef int ElemType;

typedef struct StackNode {
	ElemType data;
	StackNode *next;
}Stack,*StackTop;

typedef struct LinkStack {
	StackTop top;
	int count;
}LinkStack;

void init(LinkStack *S) {
	S->count = 0;
}

int StackEmpty(LinkStack *S) {
	return !S->count;
}

Status Push(LinkStack *S,ElemType e) {
	StackTop s = (StackTop)malloc(sizeof(StackNode));//生产新节点s
	s->data = e;//将值赋给新节点
	s->next = S->top;//将栈顶元素作为新节点的直接后继
	S->top = s;//将栈顶指针挪到新节点上
	S->count++;
	return OK;
}

Status Pop(LinkStack *S, ElemType* e) {
	StackTop p;
	if (StackEmpty(S)) {
		return ERROR;
	}
	*e = S->top->data;
	p = S->top;//p指向栈顶
	S->top = S->top->next;//将栈顶向下挪
	free(p);//删除原栈顶
	S->count--;
	return OK;
}
```

#### 逆波兰表达式
在我们平时计算带括号的表达式，如：1+1*2+(1+2)*3时，我们会将优先级最高的括号作为一个整体算出来再进行下一步计算，这个很容易让我们联想到在兔子数列的递归式里也有这样的情况，我们总会递归到f(2)+f(1)然后不断向上合并。

我们正常的读式子顺序是这样的：A*(C-D)-E，他的递归树长这个样子：
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200416-poland.png)


```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#define MAX_LEN 30
#define  MAX 100
//栈的数组实现
typedef struct
{
	int data[MAX_LEN];
	int top;
}Stack;
//为栈分配空间
Stack *Createstack()
{
	Stack *p;
	p = (Stack *)malloc(sizeof(*p));
	p->top = -1;
	return p;
}
//压栈
int Push(Stack *p, int x)
{
	if (p->top == MAX_LEN - 1)
	{
		return -1;
	}
	p->top++;
	p->data[p->top] = x;
	return 0;
}
//出栈
int Pop(Stack *L, int *x)
{
	if (L->top == -1)
	{
		return -1;
	}
	//利用传出参数传出栈顶元素
	*x = L->data[L->top];
	L->top--;
	return 0;
}
//栈顶
int TOP(Stack *L, int *x)
{
	if (L->top == -1)
	{
		return -1;
	}
	*x = L->data[L->top];
	return 0;
}
//判断栈是否为空
int Empty(Stack *L)
{
	return (L->top == -1);
}
//定义符号的优先级
int Priority(int ope)
{
	switch (ope)
	{
	case '(':   return 0;  //左括号已经在栈内时，如果比较，其优先级最低
	case '+':
	case '-':   return 1;
	case '*':
	case '%':
	case '/':   return 2;
	case '^':  return 3;
	default:   return -1;
	}
}
// 将两个数出栈、根据ope符号计算，然后再次入栈
void Calculation(Stack *snum, int ope)
{
	int n, n1, n2;
	Pop(snum, &n1);
	Pop(snum, &n2);
	switch (ope)
	{
	case '+':   n = n1 + n2; break;
	case '-':   n = n2 - n1; break;
	case '*':   n = n1 * n2; break;
	case '/':   n = n2 / n1; break;
	case '%':   n = n2 % n1; break;
	case '^':   n = pow(n2, n1);break;
	}
	Push(snum, n);
}
// 先处理除右括号外的符号
void Deal_ope(Stack *snum, Stack *sope, int ope)
{
	int old_ope;
	if (Empty(sope) || ope == '(')
	{
		Push(sope, ope);
		return;
	}
	TOP(sope, &old_ope);
	if (Priority(ope) > Priority(old_ope))
	{
		//传入符号大于当前栈顶，则将传入符号入栈
		Push(sope, ope);
		return;
	}
	//如果传入的符号优先级小于当前栈顶符号
	while (Priority(ope) <= Priority(old_ope))
	{
		//将当前栈顶的符号取出与数字栈中顶端的两个数字进行计算
		Pop(sope, &old_ope);
		printf("%c ", old_ope);
		Calculation(snum, old_ope);
		if (Empty(sope))
		{
			break;
		}
		//再次取出一个当前栈符号与传入符号比较，循环
		TOP(sope, &old_ope);
	}
	Push(sope, ope);
}
//单独处理右括号
void Right(Stack *snum, Stack *sope)
{
	int old_ope;
	TOP(sope, &old_ope);
	while (old_ope != '(')
	{
		//当前符号出栈然后将数字出栈两个进行计算,在括号内优先级最高
		Pop(sope, &old_ope);
		printf("%c ", old_ope);
		Calculation(snum, old_ope);
		//循环
		TOP(sope, &old_ope);
	}
	Pop(sope, &old_ope);//出现左括号时将它丢弃
}
// 打印数字栈
void Display(Stack *L)
{
	int i;
	if (L->top == -1)
	{
		return;
	}
	for (i = 0; i <= L->top; i++)
	{
		printf("%d ", L->data[i]);
	}
	printf("\n");
}
//打印符号栈
void Displayope(Stack *L)
{
	int i;
	if (L->top == -1)
	{
		return;
	}
	for (i = 0; i <= L->top; i++)
	{
		printf("%c ", L->data[i]);
	}
	printf("\n");
}
/*从文件中读入中缀表达式*/
void Readexpression(char a[])
{
	scanf("%s",a);
}

int main()
{
	char str[MAX];
	printf("中缀表达式为:");
	Readexpression(str);
	printf("%s\n", str);
	int i = 0, value = 0, flag = 0;   //数字的值
	int old_ope;
	Stack *numstack, *opestack;
	numstack = Createstack();  // 创建存放数字的栈
	opestack = Createstack();  // 创建存放运算符的栈
	printf("后缀表达式为:");
	//printf("栈的变化如下：\n");
	/* 表达式字符串解析函数,然后将高优先级的符号/(*)进行计算重新入栈
	   退出while大家的优先级都一样*/
	while (str[i] != '\0')
	{
		if (str[i] >= '0' && str[i] <= '9')
		{
			value *= 10;        //数字的获取，注意可能不止一位
			value += str[i] - '0';
			flag = 1;
		}
		else
		{
			if (flag)   //flag = 1说明value里面存储了数字，将其入栈
			{
				printf("%d ", value);
				Push(numstack, value);
				//flag标志清零，value存放数字的变量清零
				flag = 0;
				value = 0;
				//Display(numstack);
			}
			if (str[i] == ')')
			{
				Right(numstack, opestack);
				//Displayope(opestack);
			}
			else
			{
				Deal_ope(numstack, opestack, str[i]);
				//Displayope(opestack);
			}
		}
		i++;
	}
	if (flag)   //如果flag = 1.说明value里面还有数值,将其入栈
	{
		printf("%d ", value);
		Push(numstack, value);
		//Display(numstack);
	}
	while (!Empty(opestack))  //如果符号栈不为空，继续计算
	{
		Pop(opestack, &old_ope);
		printf("%c ", old_ope);
		Calculation(numstack, old_ope);
		//Displayope(opestack);
	}
	Pop(numstack, &value); //最终答案
	printf("\n%s = %d\n", str, value);
	system("pause");
	return 0;
}
```

#### 例题
例1🌰.给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

1.左括号必须用相同类型的右括号闭合。
2.左括号必须以正确的顺序闭合。(leetcode 20)

```java
public static boolean isValid(String s) {
	char[] c = s.toCharArray();
	if (c.length == 0)
		return true;
	if (c.length == 1)
		return false;

	Map<Character, Character> map = new HashMap<Character, Character>();
	map.put(')', '(');
	map.put(']', '[');
	map.put('}', '{');
	Stack<Character> stack = new Stack<Character>();
	int i = 0;
	while (i < c.length) {
		if (map.containsKey(c[i])) {
			if (stack.size() == 0)
				return false;
			if (map.get(c[i]) == stack.peek()) {
				stack.pop();
			} else {
				return false;
			}
		} else {
			stack.push(c[i]);
		}
		i++;
	}

	if (stack.size() == 0)
		return true;

	return false;
}
```

## 队列
> 队列是只允许在一段进行插入，另一端进行删除操作的线性表。

队列是一种先进先出的线性表。允许插入的一端称为队尾，允许删除的一段称为队头。

#### 抽象数据类型
```
ADT 队列(Queue)

Data
	同线性表。元素具有相同类型，相邻元素有前驱和后继的关系。

Operation
	InitQueue(*Q):初始化操作，建立一个空队列Q。
	DestoryQueue(*Q):若队列Q存在，则销毁。
	ClearQueue(Q):将队列Q清空。
	QueueEmpty(Q):若队列Q为空，返回true，否则返回false。
	GetHead(Q,*e):若队列Q存在且非空，用e返回队列Q的队头元素。
	EnQueue(*Q,e):若队列Q存在，插入新元素e到队列Q称为队尾元素。
	DeQueue(*Q,*e):删除队列Q中队头元素，并用e返回其值。
	QueueLength(Q):返回队列Q的元素个数。

endADT
```
#### 队列的顺序存储结构
因为普通队列和栈的实现差不多，这里实现一下循环队列

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
//状态
#define OK 1
#define true 1
#define ERROR 0
#define FALSE 0
typedef int Status;

#define MAX_SIZE 5
typedef int ElemType;

typedef struct Queue {
	ElemType data[MAX_SIZE];
	ElemType front;
	ElemType rear;
}Queue;

int init(Queue* Q) {
	Q->front = 0;
	Q->rear = 0;
	return OK;
}

int QueueLength(Queue Q) {
	return (Q.rear - Q.front + MAX_SIZE) % MAX_SIZE;
}

Status EnQueue(Queue *Q,ElemType e) {
	if ((Q->rear + 1) % MAX_SIZE == Q->front)
		return ERROR;
	Q->data[Q->rear] = e;
	Q->rear = (Q->rear + 1) % MAX_SIZE;
	return OK;
}

Status DeQueue(Queue* Q,ElemType *e) {
	if (Q->front==Q->rear) 
		return ERROR;
	*e = Q->data[Q->front];
	Q->front = (Q->front + 1) % MAX_SIZE;
	return OK;
}
```
#### 队列的链式存储结构
其实就是链表的改版。  

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

#define OK 1
#define true 1
#define ERROR 0
#define FALSE 0
typedef int Status;

typedef int ElemType;

typedef struct Queue {
	ElemType data;
	Queue* next;
}Queue, *QueueNode;

typedef struct LinkQueue{
	QueueNode front;
	QueueNode rear;
}LinkQueue;

Status EnQueue(LinkQueue* Q, ElemType e) {
	QueueNode n = (QueueNode)malloc(sizeof(Queue));
	if (!n) {
		printf("内存分配失败");
		return ERROR;
	}
	n->data = e;
	n->next = NULL;
	Q->rear->next=n;
	Q->rear = n;
	return OK;
}

Status DeQueue(LinkQueue *Q, ElemType* e) {
	QueueNode n;
	if (Q->front==Q->rear) {
		return ERROR;
	}
	n = Q->front->next;
	*e = n->data;
	Q->front->next = n->next;
	if (Q->rear==n) {
		Q->rear = Q->front;
	}
	free(n);
	return OK;
}

void init(LinkQueue *Q) {
	Q->front = (QueueNode)malloc(sizeof(Queue));
	Q->rear = Q->front;
}

```
