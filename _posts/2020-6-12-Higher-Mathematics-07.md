---
layout: 		post
title: 			"高等数学_7"
subtitle: 		'二重积分'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---
## 定义
D为xOy面上的有界闭区域，f(x,y)在D上有界。  
1.$$D\Rightarrow\Delta a_1,\Delta a_2,...,\Delta a_n$$  
2.$$\forall(\xi_i,\eta_i)\in\Delta a_i,作 \\
\sum\limits_{i=1}^{n} f(\xi_i,\eta_i)\Delta a_i$$  
3.$$\lambda为\Delta a_1,...,\Delta a_n直径最大者 \\
If\lim\limits_{\lambda\rightarrow0}\sum\limits_{i=1}^{n}f(\xi_i,\eta_i)\Delta a_i\exists \\
得此极限为f(x,y)在D上的二重积分 \\
记 \iint\limits_{D} f(x,y)da \\
\iint\limits_{D}  f(x,y)da \triangleq \lim\limits_{\lambda\rightarrow0}\sum\limits_{i=1}^{n}f(\xi_i,\eta_i)\Delta a_i$$

在公式$\iint\limits_{D}  f(x,y)d\sigma中$  
D为积分区域，f(x,y)为被积函数，x,y是积分变量，$d\sigma$为面积元素。  
整体的几何含义就是底面积为D，顶面为z=f(x,y)的曲顶柱体的体积。

性质：  
假定f(x,y)，g(x,y)在闭区域D上连续，A为D的面积。   
性质1.  
若D上f(x,y)$\equiv1，则由定义可知\iint\limits_{D}  f(x,y)d\sigma=A$  
性质2.线性性质  
$$\iint\limits_{D}[f(x,y)+g(x,y)]d\sigma=\iint\limits_{D}f(x,y)d\sigma+\iint\limits_{D}g(x,y)d\sigma \\
\iint\limits_{D}kf(x,y)d\sigma=k\iint\limits_{D}f(x,y)d\sigma$$   
性质3.区域可加性  
$$设D=D_1\cup D_1，且D_1，D_2无公共内点， \\
则有\iint\limits_{D}f(x,y)d\sigma=\iint\limits_{D_1}f(x,y)d\sigma+\iint\limits_{D_2}f(x,y)d\sigma$$  

性质4.$$若f(x,y)\geqslant 0，(x,y)\in D，则 \\
\iint\limits_{D}f(x,y)d\sigma\geqslant0$$

推论1.  
$$若f(x,y)\geqslant g(x,y)，(x,y)\in D，则 \\
\iint\limits_{D}f(x,y)d\sigma\geqslant\iint\limits_{D}g(x,y)d\sigma$$

推论2.  
$$|\iint\limits_{D}f(x,y)d\sigma|\leqslant \iint\limits_{D}|f(x,y)|d\sigma$$

性质5.估值性质  
$$设f(x,y)在有界闭区域D上的最大值为M，最小值为m，D的面积为A，则 \\
mA\leqslant\iint\limits_{D}f(x,y)d\sigma\leqslant MA$$

性质6(二重积分中值定理).  
$$若f(x,y)在D上连续，则存在一点(\xi,\eta)\in D，满足：\\
\iint\limits_{D}f(x,y)d\sigma=f(\xi,\eta)A$$

#### 直角坐标系计算
直角坐标系下，用平行于坐标轴的直线网划分区域D，面积元素为：  
$$d\sigma=dxdy$$  
所以在直角坐标系下，二重积分可写为：  
$$\iint\limits_{D}  f(x,y)d\sigma=\iint\limits_{D}  f(x,y)dxdy$$

步骤：一投 二代 三计算
$$\begin{cases}
投影到x & \int^b_adx\int^{\phi_2(x)}_{\phi_1(x)}f(x,y)dy\\
投影到y & \int^b_ady\int^{\phi_2(y)}_{\phi_1(y)}f(x,y)dx
\end{cases}$$

选择积分次序原则：  
1）积分容易  
2）尽量不分块  

先投影到x轴  
积分区域为$a\leqslant x \leqslant b,\phi_1(x)\leqslant y\leqslant\phi_2(x)$

$$
\iint\limits_{D}f(x,y)d\sigma=\\
\int^b_adx\int^{\phi_2(x)}_{\phi_1(x)}f(x,y)dy
$$


先投影到y轴  
积分区域为$a\leqslant y \leqslant b,\phi_1(x)\leqslant x\leqslant\phi_2(x)$

$$
\iint\limits_{D}f(x,y)d\sigma=\\
\int^b_ady\int^{\phi_2(y)}_{\phi_1(y)}f(x,y)dx
$$

例1🌰.将$\iint\limits_{D}f(x,y)dxdy转化为二次积分$  
其中D由直线y=x，y=x-2，y=2，y=4围成。
解法1 将D向y轴投影
$$D=\begin{cases}
2\leqslant y \leqslant 4 \\
y\leqslant x \leqslant y+2 
\end{cases}$$

解法2 将D向x轴投影  
$$
以x=4为分界线，将D分成D_1、D_2 \\
D_1=\begin{cases}
2 \leqslant x \leqslant 4 \\
2 \leqslant y \leqslant x
\end{cases} \\
D_2=\begin{cases}
4 \leqslant x \leqslant 6 \\
z-2 \leqslant y \leqslant 4
\end{cases} \\
\iint\limits_{D}f(x,y)dxdy=\iint\limits_{D_1}f(x,y)dxdy+\iint\limits_{D_2}f(x,y)dxdy \\
=\int_2^4dx\int_2^xf(x,y)dy+\int_6^4dx\int_4^{x-2}f(x,y)dy
$$

例2🌰.求$\iint\limits_{D}(x^2+y)dxdy，其中D是抛物线y=x^2和x=y^2所围的平面闭区域$

向x轴投影  
$$\int_0^1dx\int_{x^2}^{\sqrt{x}}(x^2+y)dy$$

