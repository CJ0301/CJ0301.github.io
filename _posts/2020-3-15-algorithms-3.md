---
layout: 		post
title: 			"算法"
subtitle: 		'动态规划啊动态规划'
author: 		"CJ"
header-img: 	"img/post-bg-fblog.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 动态规划
之前讲分治的时候提到过斐波那契数列，该数列的数学形式为：

$$F(n)=\begin{cases}
1 & n=1 \\
1 & n=2 \\
F(n-1)+F(n-2) & n>2
\end{cases}$$

在学编程初期讲到递归的时候，我们解决这类问题通常都是这样的👇：
```java
public static int Fibonacci(int n) {
	if(n==1||n==2) {
		return 1;
	}else {
		return Fibonacci(n-1)+Fibonacci(n-2);
	}
}
```

这种方法计算有个很致命的缺点👇：
![](/img/in-posts/20200315-tree.jpg)

可以明显的看到F(2)和F(1)的加和执行了三次，同时存在大量的结点重复。

#### 动态规划基础
> 动态规划也是一种分治思想，但是它会将子问题的结构进行存储，避免重复运算。

动态规划的两个条件：
1. 最优子结构
2. 子问题重叠

使用方式：
1. 分析最优解的结构特性
2. 建立最优值的递归式
3. 自底向上计算最优值并记录
4. 构造最优解

以斐波那契数列为例
1. 从n=3开始，F(n)的值为其前两项的加和,那么将F(n)看作一个最小子问题,那么求解F(n)包含了F(n-1)和F(n-2)两个子问题。
2. 建立递推式$$F(n)=\begin{cases}
1 & n=1 \\
1 & n=2 \\
F(n-1)+F(n-2) & n>2
\end{cases}$$
3. 自底而上计算最优值
![](/img/in-posts/20200315-tree-up.jpg)
4. 构造最优解

```java
public static int Fibonacci(int n) {
	if(n<1)
		return -1;
	int[] F = new int[n+1];
	F[1] = 1;
	F[2] = 1;
	for(int i=3;i<=n;i++)
		F[i] = F[i-1]+F[i-2];
	return F[n];
}
```