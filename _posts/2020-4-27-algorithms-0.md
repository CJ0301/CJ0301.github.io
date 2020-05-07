---
layout: 		post
title: 			"算法"
subtitle: 		'递归啊递归'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

> 简单的来说，递归就是函数中存在调用函数本身的情况。

## 递归
#### 解题思路
1.一个问题拆分出的子问题能用同一个函数解决。
2.子问题存在中止解。

🌰：求正整数n的阶乘。

1.明确函数功能：1*2*...*n

2.寻找关系式$$f(n)=\begin{cases}
1 & n=1 \\
n*f(n-1) & n > 1
\end{cases}$$

3.根据关系式，找到递推关系与中止条件。

```java
/**
 * 求 n 的阶乘
 */
public int fact(int n) {
    // 第二步的临界条件
    if (n < =1) {
        return 1;
    }

    // 第二步的递推公式
    return n * fact(n-1)
}
```

#### 尾递归优化
以上面的阶乘为例，当我们算fact(6)时会经历这样的过程:
```
6 * fact(5)
6 * (5 * fact(4))
6 * (5 * (4 * fact(3))))
...//展开
6 * (5 * (4 * (3 * (2 * (1 * 1)))))) // <= 最终的展开
6 * (5 * (4 * (3 * (2 * 1)))))
6 * (5 * (4 * (3 * 2))))
6 * (5 * (4 * 6)))
...//计算
720 // <= 最终的结果
```
由于传统递归方法是先压栈到临界条件在进行计算的，对空间损耗较大，所以我们要用尾递归的形式对算法进行优化。
```java
/**
 * 求 n 的阶乘
 */
public int fact(int n,int r) {
    if (n <= 0) {
        return 1 * r;
    } else {
        return fact(n - 1, r * n);
    }
}
```
这里用了去记录每次运算结果，与普通递归相比减少了空间占用。

注：  
1.递归不是为了求得最优解，只是一种简化解决问题的思路。
2.递归不一定求的是最优解。
3.一般情况下，最好将递归转换成非递归

#### 例题
1.汉罗塔问题
```java
public static void hanoi(int n,String p1,String p2,String p3) {
	if(n==1) {
		move(n, p1, p3);//只有一个盘子时将n移动到p3
		return;
	}
	hanoi(n-1, p1, p3, p2);//将n-1个盘子从B移到C
	move(n, p1, p3);
	hanoi(n-1, p2, p1, p3);//将n-1个盘子从A移到B
}
	
public static void move(int num,String from,String to) {
	System.out.println("将"+num+"号盘子从 "+from+" 挪到 "+to);
} 
```