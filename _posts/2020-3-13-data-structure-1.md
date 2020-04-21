---
layout: 		post
title: 			"数据结构"
subtitle: 		'基本概念'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

> 数据结构是一门研究非数值计算的程序设计问题中的操作对象，以及他们之间的关系和操作等相关问题的学科。

## 数据结构
#### 基本概念
数据：是描述客观事物的符号，是计算机中可操作的对象，是能被计算机识别，并输入给计算机处理的符号集合。

数据元素：是组成数据的、有一定意义的基本单位，在计算机中通常作为整体处理。也被称为记录。

数据项：1.一个数据元素可由若干个数据项组成。2.数据项是数据不可分割的最小单位。

数据对象：性质相同的数据元素的集合，是数据的子集。

数据结构：相互之间存在一种或多种特定关系的数据元素的集合。

比如将人类作为一个数据对象，小明为其中的数据元素，而小明的年龄、性别、身高等都可以是小明的数据项，小明与小红之间的关系即为数据结构。

#### 结构
数据结构可分为逻辑结构与物理结构  
1、逻辑结构  
逻辑结构可分为以下四种：
1. 集合结构：类似于数学中的集合，所有元素平等。
2. 线性结构：数据元素为一对一的关系。
3. 树形结构：数据元素之间存在一对多的层次关系。
4. 图形结构：数据元素是多对多的关系。

2、物理结构
物理结构可分为顺序存储结构与链式存储结构
1. 顺序存储结构：数据存放在地址连续的存储单元里。
2. 链式存储结构：数据存在任意存储单元，只有逻辑上的结构。

#### 数据类型
是指一组性质相同的值的集合及定义在此集合上的一些操作的总称。
在C语言中，数据类型可分为两类：
1. 原子类型：不可分解的基本类型，如整形、字符型等。
2. 结构类型：由若干个类型组合而成，是可以再分解的。

## 线性表
#### 定义
> 零个或多个数据元素的有限序列

线性表可记为一个{an}的数列，当n=0时为空表，n>0时，表头表尾分别有一个直接后继和一个直接前驱，表中元素二者都有且仅有一个。

最基本的两个线性表结构为数组与链表，大多数数据结构都是由这两个数据结构衍生而来的。

#### 抽象数据类型
```
ADT 线性表(List)
Data
	线性标的数据对象集合为{a1,a2,...,an},每个元素的类型均为
	DataType。其中，除了第一个元素a1外，每个元素有且仅有一个直
	接前驱元素，除了最后一个元素an外，每个元素有且仅有一个直接后
	继元素。数据元素之间的关系是一对一的关系

Operation
	InitList(*L):	初始化操作，建立一个空的线性表L。
	ListEmpty(L):	若线性表为空，返回true，否则返回false。
	ClearList(*L):	将线性表清空。
	GetElement(L,i,*e):将线性表L中的第i个位置的元素返回给e
	LocateElem(L,e):将线性表L中查找到与给定值e相等的元素，查找成功，返回该元素在表中的序号，否则返回-1。
	ListInsert(*L,i,e):在线性表L中的第i个位置插入新元素e。
	ListDelete(*L,i,*e):删除线性表L中第i个位置的元素，并用e返回其值。
	ListLength(L):	返回线性表L的元素个数

endADT

```

上面都是些基础的操作，我们有些操作可以基于这些操作进行实现。如：
```c
/*将线性表Lb中但不在La中的数据元素插入La*/
void union(List *La,List Lb){
	int La_len,Lb_len,i;
	ElemType e;
	La_len = ListLength(La);
	Lb_len = ListLength(Lb);
	for(i=1;i<=Lb_len;i++){
		GetElem(Lb,i,e);//将Lb第i个数据元素返回给e
		if(!LocateElem(La,e)){//若La不存在相同数据元素
			ListInsert(La,++La_len,e);
		}
	}
}
```

#### 线性表的顺序存储结构
一、数组  
顺序表的顺序存储结构与数组的形式类似，都是占用一段连续的存储空间。  
注：下面是静态数组的代码，动态数组的实现考虑到地址空间的连续性问题，需要重新开辟一个容量更大的数组将元素全部迁移过去，可在增加元素的时候加入这段逻辑。
完整代码
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>

//状态
#define OK 1
#define true 1
#define ERROR 0
#define FALSE 0
typedef int Status;

//结构体
#define MAXSIZE 20
typedef int ElemType;
typedef struct
{
	ElemType data[MAXSIZE];
	int length;
}Sqlist;

//获取元素
Status GetElem(Sqlist L,int i,ElemType* e) {
	if (L.length == 0||i<1||i>L.length) {
		return ERROR;
	}
	*e = L.data[i - 1];
	return OK;
}

//插入元素
Status ListInsert(Sqlist *L,int i,ElemType e) {
	int k;
	if (L->length == MAXSIZE) {
		return ERROR;
	}
	if (i < 1||i>L->length+1) {
		return ERROR;
	}
	if (i<=L->length) {
		for (k = L->length - 1;k >= i - 1;k--) {
			L->data[k + 1] = L->data[k];
		}
	}
	L->data[i - 1] = e;
	L->length++;
	return OK;
}

//删除元素
Status ListDelete(Sqlist *L, int i, ElemType *e) {
	int k;
	if (L->length==0) {
		return ERROR;
	}
	if (i<1||i>L->length) {
		return ERROR;
	}
	*e = L->data[i - 1];
	if (i<L->length) {
		for (k = i;k < L->length;k++) {
			L->data[k - 1] = L->data[k];
		}
	}
	L->length--;
	return OK;
}

//初始化
void initList(Sqlist *L) {
	L->length = 0;
}

int main() {
	Sqlist* list = (Sqlist*)malloc(MAXSIZE * sizeof(int));
	ElemType* e = (ElemType*)malloc(sizeof(ElemType));
	initList(list);
	for (int i = 0;i < 10;i++) {
		ListInsert(list,i,i);
	}

	GetElem(*list,3,e);
	printf("%d",*e);
	system("pause");
}
```
顺序表的优点在于结构简单，因为是连续的存储空间，不需要额外的逻辑关系增加存储空间，随机读取快。而缺点就是插入删除需要移动后面的元素，存储空间容量的不灵活，若有超出还需重新开辟空间整体复制，浪费资源。

#### 线性表的链式存储结构
链表
链式存储结构就解决了插入删除需要大量移动工作的问题。  
完整代码
```c
#define  _CRT_SECURE_NO_WARNINGS 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Node
{
	int id;		//数据域
	struct Node *next;	//指针域
}SLIST;

//创建头节点
SLIST *SListCreat() 
{
	SLIST *pCur = NULL;		//当前节点
	SLIST *pHead = NULL;	//头结点
	SLIST *pNew = NULL;		//新节点

	//头结点，只是作为标志使用，不保存有效数据
	pHead = (SLIST *)malloc(sizeof(SLIST));
	if (pHead == NULL)
	{
		return NULL;
	}

	//pHead成员变量赋值，数据域任意即可，后面用不上
	pHead->id = -1;
	pHead->next = NULL;

	//保存当前节点
	//指针指向谁，就把谁的地址赋值给指针
	pCur = pHead;

	int data;

	//循环创建结点，结点数据域中的数值从键盘输入，以-1作为输入结束标志
	while (1)
	{
		printf("请输入数据：");
		scanf("%d", &data); 

		if (data == -1)
		{//输入-1，退出循环
			break;
		}

		//新节点分配空间
		pNew = (SLIST *)malloc(sizeof(SLIST));
		if (pNew == NULL)
		{//如果没有分配成功，跳出本次循环
			continue;
		}

		//pNew成员变量赋值
		pNew->id = data;
		pNew->next = NULL;

		//当前节点next指向新节点
		pCur->next = pNew;

		//新节点的next指向NULL
		pNew->next = NULL;

		//当前节点的位置移动到新节点的位置（pCur指向pNew）
		pCur = pNew;
	}

	
	//链表的头结点地址由函数值返回。
	return pHead;
}

//遍历节点
//顺序输出单向链表各项结点数据域中的内容
int SListPrint(SLIST *pHead)
{
	if (pHead == NULL)
	{
		return -1;
	}

	//保存头结点的下一个节点
	//因为头结点不是有效数据节点，下一个节点才是有效数据的结点
	SLIST *pCur = pHead->next;

	printf("head -> ");
	while (pCur != NULL)
	{
		printf("%d -> ", pCur->id);

		//节点往后移动，当前节点指向下一个节点
		pCur = pCur->next;
	}
	printf("NULL\n");

	return 0;
}

//在值为x的结点前，插入值为y的结点；
//若值为x的结点不存在，则插在表尾
int SListNodeInsert(SLIST *pHead, int x, int y)
{
	if (pHead == NULL)
	{
		return -1;
	}

	SLIST *pPre = pHead;		//上一个节点
	SLIST *pCur = pHead->next;	//当前节点
	SLIST *pNew = NULL;         //新节点

	while (pCur != NULL)
	{
		//如果当前节点数据域等于x，跳出循环
		if (pCur->id == x)
		{
			break;
		}

		//保存当前节点
		pPre = pCur;

		//当前节点往后移动，当前节点指向下一个节点
		//pPre和pCur相差一个节点，pPre为上一个节点，pCur为当前节点
		pCur = pCur->next;
	}

	//程序执行到这，有两种情况
	//1. 找到值为x的结点，pCur为当前匹配节点，pPre为上一个节点
	//2. 没有找到x的结点，节点移动到结尾，pPre为最后一个节点，pCur为NULL

	//在值为x的结点前，插入值为y的结点；
	//若值为x的结点不存在，则插在表尾
	
	//新节点分配空间
	pNew = (SLIST *)malloc(sizeof(SLIST));
	if (pNew == NULL)
	{
		return -2;
	}

	//pNew成员变量赋值
	pNew->id = y;
	pNew->next = NULL;

	//pPre的next指向pNew
	pPre->next = pNew;

	//pNew的next指向pCur
	pNew->next = pCur;

	return 0;
}

//删除第一个值为x的结点
int SListNodeDel(SLIST *pHead, int x)
{
	if (pHead == NULL)
	{
		return -1;
	}

	SLIST *pPre = pHead;		//上一个节点
	SLIST *pCur = pHead->next;	//当前节点
	int flag = 0; //标志位，0代表没有值为x的结点，1代表有


	while (pCur != NULL)
	{
		if (pCur->id == x)
		{
			//上一个节点指向当前节点的下一个节点
			pPre->next = pCur->next;

			//临时释放节点
			free(pCur);
			pCur = NULL;

			//标志位，0代表没有值为x的结点，1代表有
			flag = 1;

			//跳出循环
			break;
		}

		//保存当前节点
		pPre = pCur;

		//当前节点往后移动，当前节点指向下一个节点
		//pPre和pCur相差一个节点，pPre为上一个节点，pCur为当前节点
		pCur = pCur->next;
	}


	if (flag == 0)
	{ //标志位，0代表没有值为x的结点，1代表有
		printf("没有值为%d的结点\n", x);
		return -2;
	}

	return 0;
}

//释放所有节点
int SListDestroy(SLIST *pHead)
{
	if (pHead == NULL)
	{
		return -1;
	}

	SLIST *pTmp = NULL;	//临时释放节点

	while (pHead != NULL)
	{
		//临时释放节点
		pTmp = pHead;

		//头结点指向头结点next节点
		pHead = pHead->next;
		
		free(pTmp);
		pTmp = NULL;

	}

	return 0;
}

int main()
{
	SLIST *pHead = NULL;

	pHead = SListCreat(); //创建头结点
	printf("\n创建头结点后\n");
	SListPrint(pHead); //遍历所有节点

	
	SListNodeInsert(pHead, 4, 3);//在4前面插入3
	printf("\n在4前面插入3\n");
	SListPrint(pHead); //遍历所有节点

	
	SListNodeDel(pHead,  4);//删除第一个值为4的结点
	printf("\n删除第一个值为4的结点\n");
	SListPrint(pHead); //遍历所有节点


	SListDestroy(pHead);//释放所有节点
	pHead = NULL;
	SListPrint(pHead); //遍历所有节点

	printf("\n");
	system("pause");
	return 0;
}

```


