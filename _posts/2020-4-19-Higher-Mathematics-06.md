---
layout: 		post
title: 			"高等数学_6"
subtitle: 		'向量代数与空间解析几何'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---
## 空间解析几何
#### 理论
(一)defs  
1.向量的坐标形式  
$$假设\vec{i}、\vec{j}、\vec{k}分别为x轴、y轴、z轴上的单位向量，A(x_1,y_1,z_1),B(x_2,y_2,z_2)$$  

$$\vec{AB}=(x_2-x_1)\vec{i}+(y_2-y_1)\vec{j}+(z_2-z_1)\vec{k}$$

$$\triangleq\{x_2-x_1,y_2-y_1,z_2-z_1\}$$

2.模  
$$设\vec{a}=\{a_1,b_1,c_1\}$$

$$|\vec{a}|=\sqrt{a_1^2+b_1^2+c_1^2}$$

$$设\vec{a}\neq\vec{0},\vec{a}^0=\frac{\vec{a}}{|\vec{a}|}(单位化)$$

🌟3.方向角与方向余弦  
方向角：向量与坐标轴正方向的夹角。
  
$$设\alpha、\beta、\gamma为向量\vec{a}分别与x轴、y轴、z轴的夹角，\vec{a}=\{a_1,b_1,c_1\}。$$

$$cos\alpha=\frac{a_1}{|\vec{a}|}$$

$$cos\beta=\frac{b_1}{|\vec{a}|}$$

$$cos\gamma=\frac{c_1}{|\vec{a}|}$$

$$1.cos^2\alpha+cos^2\beta+cos^2\gamma=1$$

$$2.{cos\alpha,cos\beta,cos\gamma}=\frac{\vec{a}}{|\vec{a}|}=\vec{a}^0$$



(二)向量运算的刻画  
1、几何

1.$$\vec{a}+\vec{b}、\vec{a}-\vec{b}
加就用平行四边形法则，将向量b平移到起点与向量a终点重合位置，连接向量a起点与向量b终点得\vec{a}+\vec{b}。$$  
减法就先翻转向量b。

2.$$k\vec{a}\begin{cases}
k>0 & k\vec{a}与\vec{a}同，长为\vec{a}的k倍 \\
k=0 & k\vec{a}=\vec{0} \\
k<0 & k\vec{a}与\vec{a}不同，长为\vec{a}的|k|倍 
\end{cases}$$

3.内积

$$用一个斜向上夹角为\theta的力F将物块从A点拉到B点，做功为w$$

$$w=|\vec{F}|·cos\theta·|\vec{AB}|$$

$$\triangleq \vec{F}·\vec{AB}$$

$$\vec{a}·\vec{b}=|\vec{a}|·|\vec{b}|cos\theta$$

4.向量积  
向量积的结果是一个向量而非标量。  
$$\vec{a}×\vec{b}\begin{cases}
方向：与两向量垂直 \\
大小：|\vec{a}×\vec{b}|=|\vec{a}|·|\vec{b}|sin\theta
\end{cases}$$

2、代数刻划  

$$设\vec{a}=\{a_1,b_1,c_1\},\vec{b}=\{a_2,b_2.c_2\}$$

1.$$\vec{a}+\vec{b}=\{a_1+a_2,b_1+b_2,c_1+c_2\}$$

2.$$\vec{a}-\vec{b}=\{a_1-a_2,b_1-b_2,c_1-c_2\}$$

3.$$k\vec{a}=\{ka_1,kb_1,kc_1\}$$

4.$$\vec{a}·\vec{b}=a_1a_2+b_1b_2+c_1c_2$$

5.![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-04-19-math.png)

$$如：\vec{a}=\{2,1,-1\},\vec{b}=\{3,1,4\}$$

$$\vec{a}×\vec{b}=\{5,-11,-1\}$$

Notes：  
1.xyz轴呈逆时针。  
2.$$\vec{a}·\vec{b}:\begin{cases}
\vec{a}·\vec{b} = \vec{b}·\vec{a} \\
\vec{a}·\vec{a} = |\vec{a}|^2  \\
\vec{a}·\vec{b} \Leftrightarrow \vec{a}\perp\vec{b}
\end{cases}$$
3.$$\vec{a}×\vec{b}:\begin{cases}
\vec{a}×\vec{b}=-\vec{b}×\vec{a} \\
\vec{a}×\vec{b}\perp\vec{a},\vec{a}×\vec{b}\perp\vec{b} \\
\vec{a}×\vec{b}=\vec{0} \Leftrightarrow \vec{a} //\vec{b} \Leftrightarrow \frac{a_1}{a_2}=\frac{b_1}{b_2}=\frac{c_1}{c_2} \\
|\vec{a}×\vec{b}|=2S_{\Delta}
\end{cases}$$

#### 应用
(一)空间曲面  F(x,y,z)=0  
🌰:$$x^2+y^2=4在二维是一个圆，在三维是一个母线与z轴平行的圆柱体。$$  
1.特殊曲面  
(1)柱面

$$F(x,y)=0$$

(2)旋转曲面  
Case1.二维空间：

$$L：\begin{cases}
f(x,y)=0 \\
z=0
\end{cases}$$

$$绕x轴旋转：f(x,\pm\sqrt{y^2+z^2})$$

$$绕y轴旋转：f(\pm\sqrt{x^2+z^2},y)$$

🌰：$$L：\begin{cases}
\frac{x^2}{4}+y^2=1 \\
z=0
\end{cases}$$

$$绕x轴旋转：\frac{x^2}{4}+y^2+z^2=1$$

$$绕y轴旋转：\frac{x^2}{4}+y^2+\frac{z^2}{4}=1$$

又🌰：$$L：\begin{cases}
z=x^2 \\
y=0
\end{cases}$$

$$绕z轴旋转：z=x^2+y^2$$

Case2.三维空间：

2.退化 ——平面
(1)点法式  
$$以一个属于平面\alpha的点M_0(x_0,y_0,z_0)和一个平面的法向量\vec{n}={A,B,C}$$

$$确定平面\alpha:A(x-x_0)+B(y-y_0)+C(z-z_0)=0$$

(2)截距式  
$$取三个点A(a,0,0),B(0,b,0),C(0,0,c),形成一个平面\alpha$$

$$\vec{AB}={-a,b,0}$$

$$\vec{AC}={-a,0,c}$$

$$\vec{n}=\vec{AB}×\vec{AC}={bc,ac,ab}$$

$$\alpha:bc(x-a)+ac(y-0)+ab(z-0)=0$$

$$\alpha:\frac{x}{a}+\frac{y}{b}+\frac{z}{c}=1$$

(3)一般式  
$$\alpha:Ax+By+Cz+D=0$$

(二)空间曲线
1.形式  
(1)一般形式  
$$L:\begin{cases}
F(x,y,z)=0 \\
G(x,y,z)=0
\end{cases}$$

(2)参数式  
$$L:\begin{cases}
x=\phi(t) \\
y=\Phi(t) \\
z=\omega(t)
\end{cases}$$

2.退化 ——直线  
(1)点向式  
设$$M_0(x_0,y_0,z_0),\vec{s}={m,n,p}//L$$

$$L:\frac{x-x_0}{m}=\frac{y-y_0}{n}=\frac{z-z_0}{p}$$

(2)参数式  
令$$\frac{x-x_0}{m}=\frac{y-y_0}{n}=\frac{z-z_0}{p}=t$$

$$L:\begin{cases}
x=x_0+mt \\
y=y_0+nt \\
z=z_0+pt
\end{cases}$$

(3)一般式  
$$L:\begin{cases}
A_1x+B_1y+C_1z+D_1=0 \\
A_2x+B_2y+C_2z+D_2=0
\end{cases}$$

例1🌰.$$A(-1,0,1),B(1,1,1),C(2,0,1),求S_{\Delta}ABC$$.

$$解：\vec{AB}=\{2,1,0\},\vec{AC}=\{3,0,0\}$$

$$\vec{AB}×\vec{AC}={0,0,-3}$$

$$|\vec{AB}×\vec{AC}|=3$$

$$S_{\Delta}ABC=\frac{3}{2}$$

例2🌰.$$L:\begin{cases}
x-y-2=0 \\
2x+y-z-3=0
\end{cases}化为点向式$$

$$解：M_0\{1,-1,-2\}\in L$$

$$\because L与两平面的法向量\vec{n_1}与\vec{n_2}都垂直$$

$$\therefore 与L平行的向量\vec{S}=\vec{n_1}×\vec{n_2}$$

$$=\{1,-1,0\}×\{2,1,-1\}$$

$$=\{1,1,3\}$$

$$L:\frac{x-1}{1}=\frac{y+1}{1}=\frac{z+2}{3}$$

例3🌰.$$L:\frac{x-2}{1}=\frac{y+1}{-2}=\frac{z}{1},求直线L绕z轴旋转曲面$$

$$解：\forall M(x,y,z)\in 直线L绕z轴旋转曲面$$

$$M_0(x_0,y_0,z_0)\in L$$

$$圆心T(0,0,z)$$

$$|MT|=|M_0T|$$

$$\Rightarrow\sqrt{x^2+y^2}=\sqrt{x_0^2+y_0^2}$$

$$\Rightarrow x^2+y^2 = x_0^2+y_0^2 $$

$$\because M_0\in L$$

$$\therefore \frac{x_0-2}{1}=\frac{y_0+1}{-2}=\frac{z_0}{1}$$

$$\Rightarrow\begin{cases}
x_0=2+z \\
y_0=-1-2z
\end{cases}$$

$$\therefore 直线L绕z轴旋转曲面：x^2+y^2=5+8z+5z^2$$