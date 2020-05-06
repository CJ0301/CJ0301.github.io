---
layout: 		post
title: 			"数据结构"
subtitle: 		'串'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---
> 串是由零个或多个字符组成的有限序列，又称字符串。

## 串
串与线性表有很多相似之处，但是线性表更强调单个元素的增删改查，而串更多的是查找子串位置、替换子串等操作。

#### 常见字符ASCII值
1. 0~9 48~57
2. A~Z 65~90
3. a~z 97~122

#### 抽象数据类型
```
ADT 串(string)

Data
	串中元素仅由一个字符构成，相邻元素具有前驱和后继的关系。

Operation
	StrAssign(T,*chars):生成一个其值等于字符串常量chars的串T。
	StrCopy(T,S):串S存在，由S复制得串T。
	ClearString(S):串S存在，将串清空。
	StringEmpty(S):若串S为空，返回true，否则返回false。
	StrLength(S):若返回串S的元素个数，即串的长度。
	StrCompare(S,T):若S>T,返回值>0,若S=T，返回0，若S<T,返回值<0。
	Concat(T,S1,S2):用T返回由S1和S2联接而成的新串。
	SubString(Sub,S,pos,len):串S存在，pos在[1,StrLength(S)]内，且len在[0,StrLength(S)-pos+1]，用Sub返回串S的第pos个字符起长度为len的子串。
	Index（S,T，pos):串S和T存在，T是非空串，pos在[1,StrLength(S)]内。若主串S中存在和串T值相同的子串，则返回他在主串S中第pos个字符之后第一次出现的位置，否则返回0。
	Replace(S,T,V):串S、T和V存在，T是非空串。用V替换主串S中出现的所有与T相等的不重叠的子串。
	StrInsert(S,pos,T):串S和T存在，pos在[1,StrLength(S)+1]内。在串S的第pos个字符之前插入串T。
	StrDelete(S,pos,len):串S存在，pos在[1,StrLength(S)-len+1]内。在串S中删除第pos个字符起长度为len的子串。
```

#### 串的顺序存储
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include<math.h>
#include<string.h>
#define OK 1
#define TRUE 1
#define FALSE 0
#define ERROR 0
#define OVERLOW -1 

#define MAX_STR_LEN 40 // 用户可在255(1个字节)以内定义最大串长  
typedef char SString[MAX_STR_LEN + 1]; // 0号单元存放串的长度  

#define DestroyString ClearString // DestroyString()与ClearString()作用相同  

typedef int Status;

Status StrAssign(SString T, char *chars)
{ // 生成一个其值等于chars的串T  
	int i;
	if (strlen(chars) > MAX_STR_LEN)
		return ERROR;
	else
	{
		T[0] = strlen(chars);
		for (i = 1;i <= T[0];i++)
			T[i] = *(chars + i - 1);
		return OK;
	}
}
void StrCopy(SString T, SString S)
{ // 由串S复制得串T  
	int i;
	for (i = 0;i <= S[0];i++)
		T[i] = S[i];
}
Status StrEmpty(SString S)
{ // 若S为空串，则返回TRUE；否则返回FALSE  
	if (S[0] == 0)
		return TRUE;
	else
		return FALSE;
}
int StrCompare(SString S, SString T)
{// 初始条件：串S和T存在。操作结果：若S>T，则返回值>0；若S=T，则返回值=0；若S<T，则返回值<0  
	int i;
	for (i = 1;i <= S[0] && i <= T[0];++i)
		if (S[i] != T[i])
			return S[i] - T[i];
	return S[0] - T[0];
}
int StrLength(SString S)
{ // 返回串S的元素个数  
	return S[0];
}
void ClearString(SString S)
{ // 初始条件：串S存在。操作结果：将S清为空串(见图4.3)  
	S[0] = 0; // 令串长为零  
}
Status Concat(SString T, SString S1, SString S2) // 算法4.2改  
{ // 用T返回S1和S2联接而成的新串。若未截断，则返回TRUE；否则返回FALSE  
	int i;
	if (S1[0] + S2[0] <= MAX_STR_LEN)
	{ // 未截断  
		for (i = 1;i <= S1[0];i++)
			T[i] = S1[i];
		for (i = 1;i <= S2[0];i++)
			T[S1[0] + i] = S2[i];
		T[0] = S1[0] + S2[0];
		return TRUE;
	}
	else
	{ // 截断S2  
		for (i = 1;i <= S1[0];i++)
			T[i] = S1[i];
		for (i = 1;i <= MAX_STR_LEN - S1[0];i++)
			T[S1[0] + i] = S2[i];
		T[0] = MAX_STR_LEN;
		return FALSE;
	}
}
Status SubString(SString Sub, SString S, int pos, int len)
{ // 用Sub返回串S的自第pos个字符起长度为len的子串。算法4.3  
	int i;
	if (pos<1 || pos>S[0] || len<0 || len>S[0] - pos + 1)
		return ERROR;
	for (i = 1;i <= len;i++)
		Sub[i] = S[pos + i - 1];
	Sub[0] = len;
	return OK;
}
int Index(SString S, SString T, int pos)
{ // 返回子串T在主串S中第pos个字符之后的位置。若不存在，则函数值为0。  
	// 其中，T非空，1≤pos≤StrLength(S)。算法4.5  
	int i, j;
	if (1 <= pos && pos <= S[0])
	{
		i = pos;
		j = 1;
		while (i <= S[0] && j <= T[0])
			if (S[i] == T[j]) // 继续比较后继字符  
			{
				++i;
				++j;
			}
			else // 指针后退重新开始匹配  
			{
				i = i - j + 2;
				j = 1;
			}
		if (j > T[0])
			return i - T[0];
		else
			return 0;
	}
	else
		return 0;
}
Status StrInsert(SString S, int pos, SString T)
{ // 初始条件：串S和T存在，1≤pos≤StrLength(S)+1  
	// 操作结果：在串S的第pos个字符之前插入串T。完全插入返回TRUE，部分插入返回FALSE  
	int i;
	if (pos<1 || pos>S[0] + 1)
		return ERROR;
	if (S[0] + T[0] <= MAX_STR_LEN)
	{ // 完全插入  
		for (i = S[0];i >= pos;i--)
			S[i + T[0]] = S[i];
		for (i = pos;i < pos + T[0];i++)
			S[i] = T[i - pos + 1];
		S[0] += T[0];
		return TRUE;
	}
	else
	{ // 部分插入  
		for (i = MAX_STR_LEN;i >= pos + T[0];i--)
			S[i] = S[i - T[0]];
		for (i = pos;i < pos + T[0] && i <= MAX_STR_LEN;i++)
			S[i] = T[i - pos + 1];
		S[0] = MAX_STR_LEN;
		return FALSE;
	}
}
Status StrDelete(SString S, int pos, int len)
{ // 初始条件：串S存在，1≤pos≤StrLength(S)-len+1  
	// 操作结果：从串S中删除自第pos个字符起长度为len的子串  
	int i;
	if (pos<1 || pos>S[0] - len + 1 || len < 0)
		return ERROR;
	for (i = pos + len;i <= S[0];i++)
		S[i - len] = S[i];
	S[0] -= len;
	return OK;
}
Status Replace(SString S, SString T, SString V) // 此函数与串的存储结构无关  
{ // 初始条件：串S，T和V存在，T是非空串  
	// 操作结果：用V替换主串S中出现的所有与T相等的不重叠的子串  
	int i = 1; // 从串S的第一个字符起查找串T  
	Status k;
	if (StrEmpty(T)) // T是空串  
		return ERROR;
	do
	{
		i = Index(S, T, i); // 结果i为从上一个i之后找到的子串T的位置  
		if (i) // 串S中存在串T  
		{
			StrDelete(S, i, StrLength(T)); // 删除该串T  
			k = StrInsert(S, i, V); // 在原串T的位置插入串V  
			if (!k) // 不能完全插入  
				return ERROR;
			i += StrLength(V); // 在插入的串V后面继续查找串T  
		}
	} while (i);
	return OK;
}
void StrPrint(SString T)
{ // 输出字符串T。另加  
	int i;
	for (i = 1;i <= T[0];i++)
		printf("%c", T[i]);
	printf("\n");
}
```

#### 串的链式存储
串的链式存储拓展性好，但是内存占用高。
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>


//串的链式存储
typedef struct charNode {
	char data;
	struct charNode *next;
}charNode;
typedef charNode *charLink;
//c中字符串会有以下几种形式：字符串常量"hello"，char数组char m[40] = "hello,world"，char指针char *m = "hello,world"
void init(charLink *c, char s[]) {
	charLink p, q;
	(*c) = (charLink)malloc(sizeof(charNode));//创建链式串
	q = *c;//定义指针指向串
	for (int i = 0;s[i] != '\0';i++) {//c里面所有定义的字符串后面都会有一个‘\0’，他代表结束
		p = (charLink)malloc(sizeof(charNode));
		p->data = s[i];//这里类似链表的尾插法
		q->next = p;
		q = p;
	}
	q->next = NULL;
}
//获取串长度
int getLength(charLink c) {
	int i = 0;
	charLink p;
	p = c;
	while (p->next) {
		p = p->next;
		i++;
	}
	return i;
}
//将两个串拼成一个串
void connection(charLink *c, charLink b) {
	charLink p = (*c)->next;//定义一个指针指向c的第一个字符。
	charLink p2 = b;//定义一个指针指向b
	charLink p3;//用来存储在b中取出的字符节点
	char s;//用来存放从b中取出的字符数据
	while (p2->next) {//从b的第一个字符节点开始取
		p2 = p2->next;
		s = p2->data;
		while (p->next) {//从c的第一个字符节点的next开始判断，如果不为空，就向下指，直到p成为c的最后一个字符节点
			p = p->next;
		}
		p3 = (charLink)malloc(sizeof(charNode));
		p3->data = s;
		p->next = p3;//类似链表的尾插法，让后插入的数据都往后排
		p = p3;
	}
	p->next = NULL;
}
void substring(charLink c, int index, int slength, charLink *s) {
	//当index+slength<=(*s).length+1时才能取
	charLink p, z;
	*s = (charLink)malloc(sizeof(charNode));
	z = *s;
	p = c->next;
	int i = 1, j = 1;
	//拿到主串的要取数据的第一个位置
	while (p->next&&i < index) {
		p = p->next;
		i++;
	}
	//取值赋值
	while (p&&j <= slength) {
		charLink n = (charLink)malloc(sizeof(charNode));
		n->data = p->data;
		z->next = n;
		z = n;
		p = p->next;
		j++;
	}
	z->next = NULL;

}
void display(charLink c) {
	charLink p = c->next;
	while (p) {
		char q = p->data;
		printf("%c ", q);
		p = p->next;
	}
	printf("\n");
}
```

#### 例题
例1🌰.给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。(leetcode459)
```java
public static boolean minCircle(String s) {
		int size = s.length();
		if(size==0||size==1) {
			return false;
		}
		boolean flag;
		int i,j;
		for(i=1;i<size;i++) {
			if(size%i==0) {
				flag=true;
				for(j=0;j<=size-i*2;j+=i) {
					if(!s.subSequence(j, j+i).equals(s.subSequence(j+i, j+i*2))) {
						flag=false;
						break;
					}
				}
				if(flag) {
					return flag;
				}
			}
		}
		return false;
	}
```