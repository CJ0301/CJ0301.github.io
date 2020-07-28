---
layout: 		post
title: 			"高等数学_9"
subtitle: 		'无穷级数'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---

## 常数项级数
#### 概念及其敛散性
给定一个无穷数列$u_1,u_2,...,u_n,...$，将其各项用加号连起来得到记号$\sum^{\infty}_{n=1}u_n$即  

$$\sum^{\infty}_{n=1}u_n=u_1+u_2+...+u_n+...$$

叫做无穷级数，简称级数，其中$u_n$叫做该级数的通项。若$u_n$是常数而不是函数，则$\sum^{\infty}_{i=1}u_n$就被称为常数项无穷级数。简称常数项级数。

将级数各项逐一相加：  

$$S_1=u_1,S_2=u_1+u_2,...,S_n=u_1+u_2+...+u_n$$

这是级数的部分和，$$\{S_n\}是级数的部分和数列，若\lim\limits_{n\rightarrow\infty}S_n=S,则\sum^{\infty}_{n=1}u_n收敛 \\
，S为收敛级数\sum^{\infty}_{n=1}u_n的和；若\lim\limits_{n\rightarrow\infty}S_n不存在或为\pm\infty则称\sum^{\infty}_{n=1}u_n发散。$$

例1🌰.$$判断几何级数(等比数列) \\
\sum^{\infty}_{n=1}aq^{n-1}=a+aq+aq^2+...+aq^{n-1}+...的敛散性，其中a\neq0$$

$$
\sum^{n=1}_{\infty}aq^{n-1}=\frac{a(1-q^n)}{1-q} \\
求\lim\limits_{n\rightarrow\infty}S_n \\
1.|q|<1，\lim\limits_{n\rightarrow\infty}S_n=\frac{a}{1-q} \\
2.q>1或q<-1，\lim\limits_{n\rightarrow\infty}S_n不存在 \\
3.q=1，\lim\limits_{n\rightarrow\infty}S_n不存在 \\
q=-1，\lim\limits_{n\rightarrow\infty}S_n不存在
$$

性质  

1.若级数$$\sum^{\infty}_{n=1}u_n,\sum^{\infty}_{n=1}v_n均收敛，且和分别为S,T，则任给常数a,b有\sum^{\infty}_{n=1}(au_n+bv_n)$$也收敛，其和为aS+bT，即

$$\sum^{\infty}_{n=1}(au_n+bv_n)=a\sum^{\infty}_{n=1}u_n+b\sum^{\infty}_{n=1}v_n$$

级数$\sum^{\infty}_{n=1}u_n$去掉前m项，得  

$$\sum^{\infty}_{n=m+1}=u_{m+1}+u_{m+2}+...+u_{m+k}+...$$

称为$\sum^{\infty}_{n=1}u_n$的m项后余项。

2.若级数$\sum^{\infty}_{n=1}u_n$收敛，则它的任意m项后余项也收敛；反之成立。

3.若$$\sum^{\infty}_{n=1}u_n收敛,\lim\limits_{n\rightarrow\infty}u_n=0$$。

4.收敛级数的项任意加括号后所得新级数仍收敛，其和不变。  
注意：  
加括号后的新级数发散，原级数必然发散(逆否命题)。  
若加括号得到的新级数收敛，不能断言原级数一定收敛。

5.若原级数绝对收敛，无论各项如何重排列，所得级数也绝对收敛。

#### 级数敛散性的判别方法
1、正项级数  
若通项$u_n\geqslant0$n=1,2,...，则称$\sum^{\infty}_{n=1}u_n$为正项级数。      
特性：单调不减下界为0

(1)收敛原则    
正项级数$$\sum^{\infty}_{n=1}u_n收敛的充分必要条件是它的部分和数列\{S_n\}$$有界

(2)比较判别法  
两个正项级数$$\sum^{\infty}_{n=1}u_n和\sum^{\infty}_{n=1}v_n，若从某项起有u_n\leqslant v_n成立，则$$  
1. 若$$\sum^{\infty}_{n=1}v_n收敛，则\sum^{\infty}_{n=1}u_n也收敛$$  
2. 若$$\sum^{\infty}_{n=1}u_n发散，则\sum^{\infty}_{n=1}v_n也发散$$  
通俗来说就是：两正项级数，大的收敛，则小的必收敛；小的发散，则大的必发散。

(3)比较判别法的极限形式  
两个正项级数$$\sum^{\infty}_{n=1}u_n和\sum^{\infty}_{n=1}v_n，v_n\neq0，且$$  

$$\lim\limits_{n\rightarrow\infty}=\frac{u_n}{v_n}=A$$  
1. 若A=0，则当$$\sum^{\infty}_{n=1}v_n收敛时，\sum^{\infty}_{n=1}u_n也收敛$$  
2. $$若A= +\infty，则当\sum^{\infty}_{n=1}v_n发散时，\sum^{\infty}_{n=1}u_n也发散$$
3. $$若0<A<+\infty，则\sum^{\infty}_{n=1}u_n与\sum^{\infty}_{n=1}v_n有相同的敛散性。$$

(4)比值判别法(达朗贝尔判别法)
给出一个正项级数$$\sum^{\infty}_{n=1}u_n，如果\lim\limits_{n\rightarrow\infty}\frac{u_{n+1}}{u_n}=\rho,那么$$

1. $$若\rho<1，则\sum^{\infty}_{n=1}u_n收敛$$
2. $$若\rho>1，则\sum^{\infty}_{n=1}u_n发散$$
3. =无法判别敛散性

例2🌰.$$判断级数\sum^{\infty}_{n=1}\frac{1}{\sqrt{n}}的敛散性$$

$$\sum^{\infty}_{n=1}\frac{1}{\sqrt{n}}=1+\frac{1}{\sqrt{2}}+...+\frac{1}{\sqrt{n}}+...>\sqrt{n}\\
\lim\limits_{n\rightarrow+\infty}\sqrt{n}=+\infty \\
\therefore\{S_n\}无界\Rightarrow\sum^{\infty}_{n=1}\frac{1}{\sqrt{n}}发散
$$

例3🌰.$$判断级数\sum^{\infty}_{n=1}\frac{1}{n}的敛散性(调和级数)$$

$$x>0时，x>\ln(1+x)\Rightarrow\frac{1}{n}>\ln(1+\frac{1}{n}) \\
\sum^{\infty}_{n+1}\ln(1+\frac{1}{n})=\ln\frac{2}{1}+\ln\frac{3}{2}+...+\ln\frac{n+1}{n} \\
=\ln(n+1) \\
\sum^{\infty}_{n+1}\ln(1+\frac{1}{n})发散，\therefore\sum^{\infty}_{n=1}\frac{1}{n}发散$$

P一级数$$\sum^{\infty}_{n=1}\frac{1}{n^P}\begin{cases}
P>1 & 收敛 \\
P\leqslant1 & 发散
\end{cases}$$

例4🌰.$$已知级数\sum^{\infty}_{n=1}u_n绝对收敛，判断\sum^{\infty}_{n=1}\frac{u_n^2}{1+u_n^2}的敛散性，其中u_n\neq0$$

$$已知\sum^{\infty}_{n=1}|u_n|收敛 \\
1+u_n^2\geqslant2|u_n|，\therefore\frac{u_n^2}{1+u_n^2}\leqslant\frac{|u_n|}{2} \\
\therefore\sum^{\infty}_{n=1}\frac{u_n^2}{1+u_n^2}收敛$$

例5🌰.$$判断级数\sum^{\infty}_{n=1}\frac{\vert a\vert^nn!}{n^n}，其中a为非零常数$$

$$记u_n=\frac{\vert a\vert ^nn!}{n^n}，则 \\
\lim\limits_{n\rightarrow\infty}\frac{u_{n+1}}{u_n}=\lim\limits_{n\rightarrow\infty}\frac{\vert a\vert ^{n+1}·(n+1)!}{(n+1)^{n+1}}·\frac{n^n}{\vert a\vert ^n·n!} \\
=\vert a\vert\lim\limits_{n\rightarrow\infty}(\frac{n}{n+1})^n \\
=\vert a\vert e^{\lim\limits_{n\rightarrow\infty}\frac{-n}{n+1}}$$

2、交错级数  
若级数各项正负相间出现，称这样的级数为交错级数，一般写为  

$$\sum^{\infty}_{n=1}(-1)^{n-1}u_n=u_1-u_2+u_3-...+(-1)^{n-1}u_n+...$$  

若$$\{u_n\}单调不增且\lim\limits_{n\rightarrow\infty}u_n=0，则该级数收敛。$$

3、任意项级数
对任意项级数$$\sum^{\infty}_{n=1}u_n一般只研究它的绝对值级数，即给他每一项加上绝对值\sum^{\infty}_{n=1}|u_n|$$

定义1 $$\sum^{\infty}_{n=1}u_n为任意项级数，若\sum^{\infty}_{n=1} \vert u_n\vert收敛，则称\sum^{\infty}_{n=1}u_n绝对收敛$$

定义2 $$\sum^{\infty}_{n=1}u_n为任意项级数，若\sum^{\infty}_{n=1}u_n收敛，但\sum^{\infty}_{n=1} \vert u_n\vert发散，则称\sum^{\infty}_{n=1}u_n条件收敛$$

定理 $$若\sum^{\infty}_{n=1} \vert u_n\vert收敛，则\sum^{\infty}_{n=1}u_n必收敛$$

## 幂级数
#### 概念及其收敛域
1、概念
1.函数项级数  
设函数列${u_n(x)}$定义在区域I上，称  

$$u_1(x)+u_2(x)+...+u_n(x)+...$$

为定义在区间I上的函数项级数，记为$$\sum^{\infty}_{n=1}u_n(x)，当x取确定值x_0时，\sum^{\infty}_{n=1}u_n(x)成为常数项级数\sum^{\infty}_{n=1}u_n(x_0)$$

2.幂级数  
若$$\sum^{\infty}_{n=1}u_n(x)的一般项u_n(x)是n次幂函数，则称\sum^{\infty}_{n=1}u_n(x)为幂级数，一般形式为$$  

$$\sum^{\infty}_{n=1}a_n(x-x_0)^n=a_0+a_1(x-x_0)+...+a_n(x-x_0)^n$$

标准形式为  

$$\sum^{\infty}_{n=1}a_nx^n=a_0+a_1x+a_2x^2+...+a_nx^n+...$$

其中$a_n$为幂级数系数  

收敛点与发散点  
若给定$$x_0\in I，有\sum^{\infty}_{n=1}u_n(x_0)收敛，则称点x_0为幂级数\sum^{\infty}_{n=1}u_n(x)的收敛点；\\
若给定x_0\in I，有\sum^{\infty}_{n=1}u_n(x_0)发散，则称点x_0为幂级数\sum^{\infty}_{n=1}u_n(x)的发散点$$

收敛域  
函数项级数$$\sum^{\infty}_{n=1}u_n(x)的所有收敛点集合称为它的收敛域$$

阿贝尔定理  
当幂级数$$\sum^{\infty}_{n=1}a_nx^n在点x=x_1(x_1\neq0)处收敛时，满足|x|<|x_1|的一切x，幂级数绝对收敛；\\
\sum^{\infty}_{n=1}a_nx^n在点x=x_2(x_2\neq0)处发散时，满足|x|>|x_2|的一切x，幂级数绝对发散；$$

收敛域求法   
1.若$$\lim\limits_{n\rightarrow\infty}|\frac{a_{n+1}}{a_n}|=\rho，则\sum^{\infty}_{n=1}a_nx^n的收敛半径R的表达式为 \\
R=\begin{cases}
\frac{1}{\rho} & \rho\neq0 \\
+\infty & \rho=0 \\
0 & \rho=+\infty
\end{cases}$$

2.$$开区间(-R,R)为幂级数\sum^{\infty}_{n=1}a_nx^n的收敛区间； \\
单独考察x=\pm R处的敛散性就可以确定其收敛域为(-R,R)或[-R,R)或(-R,R]或[-R,R]$$

#### 幂级数求和函数
在收敛域上，记$$S(x)=\sum^{\infty}_{n=1}u_n(x)，并称S(x)为\sum^{\infty}_{n=1}u_n(x)的和函数$$

运算法则  
若幂级数$$\sum^{\infty}_{n=1}a_nx^n与\sum^{\infty}b_nx^n的收敛半径分别为R_a和R_b(R_a\neq R_b)，则有$$

1.$$k\sum^{\infty}_{n=1}a_nx^n=\sum^{\infty}_{n=1}la_nx^n,\vert x\vert<R_a,k为常数$$

2.$$\sum^{\infty}_{n=1}a_nx^n\pm\sum^{\infty}_{n=1}b_nx^n=\sum^{\infty}_{n=1}(a_n+b_n)x^n,\vert x\vert<R=min\{R_a,R_b\}$$
