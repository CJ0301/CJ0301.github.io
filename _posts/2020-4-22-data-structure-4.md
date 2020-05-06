---
layout: 		post
title: 			"数据结构"
subtitle: 		'树'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 树
> 树是n个结点的有限集。n=0时称为空树。在任意一棵非空树中：  
> (1)有且仅有一个根节点  
> (2)n>1时，其余结点可分为m(m>0)个互不相干的有限集{T1、T2...、Tm}，其中每一个集合本身又是一棵树，并称为根的子树。

#### 结点
树的结点包括根节点、内部结点、叶子结点。  
结点拥有子树数称为结点的度。  
结点的子树根结点称为孩子结点，该结点为孩子节点的双亲结点，同一个双亲的孩子结点互称兄弟结点，结点的子树任一结点都为该结点的子孙结点。

树结构的特点：
- 根节点是唯一存在的。
- 叶子结点无孩子结点可有多个。
- 中间结点有一个双亲多个孩子结点。

层数：树的根节点为第一层，根结点的子节点为第二层，第二层的所有子节点为第三层依此类推。

深度：根节点到当前节点的唯一路径长度。

高度：从当前结点到最远叶子节点路径长度。

#### 树的抽象数据类型
```
ADT 树(tree)

Data
	树是由一个根结点和若干棵子树构成。树中结点具有相同数据类型及层次关系。

Operation
	InitTree(*T):构造空树T。
	DestroyTree(*T):销毁树T。
	CreateTree(*T,definition):按definition中给出的树的定义来构造树。
	ClearTree(*T)：若树T存在，则将树T清为空树。
	TreeEmpty(T):若T为空树，返回true，否则返回false。
	TreeDepth(T):返回T的深度。
	Root(T):返回T的根节点。
	Value(T,cur_e):cur_e是树T中的一个结点，返回此结点的值。
	Assign(T,cur_e,value):给树T的结点cur_e赋值为value。
	Parent(T,cur_e):若cur_e是树T的非根结点，则返回它的双亲，否则返回空。
	LeftChild(T,cur_e):若cur_e是树T的非叶子结点，则返回它的最左孩子，否则返回空。
	RightSibling(T,cur_e):若cur_e有右兄弟，则返回它的右兄弟，否则返回空。
```

## 二叉树
> 二叉树是n(n$$\leqslant$$)

#### 性质
1.每个结点的度最大为2(最多有两个子树)  
2.左右子树有顺序  
3.即使某节点只有一颗子树，也要区分左右子树  
4.二叉树是有序树  
5.非空二叉树的第i层，最多有$$2^{i-1}$$个结点(i$$\geqslant$$1)  
6.在高度为h的二叉树上最多有$$2^h-1$$个结点(h$$\geqslant$$1)  
7.非空二叉树，如果叶子结点个数为n0,度为2的结点个数为n2，则有：n0=n2+1  
证明：假设度为1的结点个数为n1，那么二叉树的结点总数n=n0+n1+n2    
二叉树的边数T=n1+2*n2=n-1=n0+n1+n2-1

特殊二叉树：  
真二叉树：所有结点的度要么为0，要么为2。
满二叉树：所有结点的度要么为0，要么为2。且所有叶子结点都在最后一层。
完全二叉树：叶子结点只会出现最后2层，最后1层叶子结点都靠左对齐(度为1的结点只有左子树)。

#### 遍历
1.遍历方式
二叉树有三种遍历方式：前序、中序、后序。  
前序：$$根\rightarrow左\rightarrow右$$
中序：$$左\rightarrow根\rightarrow右$$
后序：$$左\rightarrow右\rightarrow根$$

2.遍历还原  
已知中序和前序可以确定唯一二叉树。  
已知中序和后序可以确定唯一二叉树。

#### 普通二叉树
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include<math.h>
#define OK 1
#define TRUE 1
#define FALSE 0
#define ERROR 0
#define OVERLOW -1 

typedef char ElementType;

typedef struct BiT {
	ElementType data;
	struct BiT *lChild, *rChild;
}BiTNode,*BiTree;

//前序遍历 中左右
void PreOrderTraverse(BiTree T) {
	if (T==NULL) 
		return;
	printf("%c",T->data);
	PreOrderTraverse(T->lChild);
	PreOrderTraverse(T->rChild);
}

//中序遍历 左中右
void InOrderTraverse(BiTree T) {
	if (T == NULL)
		return;
	PreOrderTraverse(T->lChild);
	printf("%c", T->data);
	PreOrderTraverse(T->rChild);
}

//后序遍历 左右中
void PostOrderTraverse(BiTree T) {
	if (T == NULL)
		return;
	PreOrderTraverse(T->lChild);
	PreOrderTraverse(T->rChild);
	printf("%c", T->data);
}

void CreateBiTree(BiTree *T) {
	ElementType ch;
	scanf("%c",&ch);
	if (ch=='#') {
		*T = NULL;
	}
	else {
		*T = (BiTree)malloc(sizeof(BiTNode));
		if (!*T) 
			exit(OVERFLOW);
		(*T)->data = ch;
		CreateBiTree(&(*T)->lChild);
		CreateBiTree(&(*T)->rChild);
	}
}
```



