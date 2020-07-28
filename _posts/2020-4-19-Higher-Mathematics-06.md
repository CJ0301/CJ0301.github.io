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
\vec{a}·\vec{b}=0 \Leftrightarrow \vec{a}\perp\vec{b}
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
$$以一个属于平面\alpha的点M_0(x_0,y_0,z_0)和一个平面的法向量\vec{n}=\{A,B,C\}，任取一点坐标为\{x,y,z\}$$

$$确定平面\alpha:A(x-x_0)+B(y-y_0)+C(z-z_0)=0$$

(2)截距式  
$$取三个点A(a,0,0),B(0,b,0),C(0,0,c),形成一个平面\alpha$$

$$\vec{AB}=\{-a,b,0\}$$

$$\vec{AC}=\{-a,0,c\}$$

$$\vec{n}=\vec{AB}×\vec{AC}=\{bc,ac,ab\}$$

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
设$$M_0(x_0,y_0,z_0),\vec{s}=\{m,n,p\}//L$$

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

$$\vec{AB}×\vec{AC}=\{0,0,-3\}$$

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

例4🌰.$$求过点M_1(2,0,1)，M_2(1,1,0)，M_3(0,1,1)的平面方程$$

解：$$\vec{M_1M_2}=(-1,1,-1),\vec{M_1M_3}=(-2,1,0)  \\
取\vec{n}=\vec{M_1M_2}×\vec{M_1M_3}  \\
=(1,2,1) \\
点法式：x-2+2y+z-1=0$$

例5🌰.$$求过点(3,2,1)与x轴的平面方程$$

$$(一般式)\because平面过x轴，方程为By+Cz=0 \\
\therefore 2B+C=0 \\
By-2Bz=0，即y-2z=0$$

两平面夹角即是法向量夹角  
例6🌰.$$求平面x+2y-z-2=0与平面2x-y+z+1=0的夹角$$

$$\vec{n_1}=(1,2,-1)，\vec{n_2}=(2,-1,1) \\
cos\theta=\frac{\vec{n_1}·\vec{n_2}}{|\vec{n_1}||\vec{n_2}|}=\frac{1}{6} \\
\therefore\theta=arccos\frac{1}{6}$$

点到平面的距离  
$$d=\frac{|Ax_0+By_0+Cz_0+D|}{\sqrt{A^2+B^2+C^2}}$$  
例6🌰.$$求点M_0(1,2,3)到平面x-2y+z-1=0的距离$$

$$d=\frac{|1-4+3-1|}{\sqrt{1^2+(-2)^2+1^2}}=\frac{\sqrt{6}}{6}$$

一般式转标准方程  
例7🌰.$$把直线\begin{cases}
2x+y+z+1=0 \\
x+y+z-1=0
\end{cases}化为标准方程$$

$$第一步，找点 \\
令z=0，\begin{cases}
2x+y+1=0 \\
x+y-1=0
\end{cases} \\
求得直线过点(-2,3,0) \\
取\vec{s}=\vec{n_1}×\vec{n_2}=(0,-1,1) \\
\therefore标准方程为:\frac{x+2}{0}=\frac{y-3}{-1}=\frac{z-0}{1}$$

两直线夹角  
例7🌰.$$求l_1:\frac{x-1}{1}=\frac{y+2}{2}=\frac{z-1}{3}与\\
l_2:\frac{x-2}{-4}=\frac{y-1}{5}=\frac{z-4}{-2}的夹角$$

$$\vec{s_1}=(1,2,3),\vec{s_2}=(-4,5,-2) \\
cos\theta=\frac{\vec{s_1}·\vec{s_2}}{|\vec{s_1}|·|\vec{s_2}|}=0 \\
\therefore\theta=90°$$

直线与平面位置关系  
例8🌰.$$试确定l:\frac{x+3}{2}=\frac{y+4}{7}=\frac{z-3}{-3}与\\
平面:4x-2y-2z-3=0的位置关系$$

$$\vec{s}=(2,3,-3) \vec{n}(4,-2,-2) \\
cos\theta=\frac{8-14+6}{|\vec{s}||\vec{n}|}=0 \\
任意找一点(-3,-4,3)代入平面，代入得点不在平面上 \\
\therefore l//平面$$

直线与平面交点    
例9🌰.$$求直线\frac{x-2}{1}=\frac{y-3}{1}=\frac{z-1}{2}与 \\
x+2y+z-4=0的交点坐标$$

$$化为参数式：\begin{cases}
x=2+t \\
y=3+t
z=1+2t
\end{cases}带入平面 \\
得t=-1 \\
交点(1,2,-1)$$

过点与直线相垂直的直线方程  
例10🌰.$$求过点M_0(2,-1,3)且与直线\frac{x-1}{1}=\frac{y+1}{-1}=\frac{z-1}{2}垂直相交的直线$$

$$求过M_0与直线垂直的平面 \\
\vec{n}=\vec{s}=(1,-1,2) \\
\therefore平面为x-2-(y+1)+2(z-3)=0 \\
求得直线与平面交点为t=\frac{5}{6} \therefore交点M(\frac{11}{6},-\frac{11}{6},\frac{16}{6})\\
\therefore\vec{M_0}{M}=(-\frac{1}{6},-\frac{5}{6},-\frac{1}{3}) \\
\therefore垂线：x-2=\frac{y+1}{5}=\frac{z-3}{2}$$

例11🌰.$$求过点M(-1,0,1)与直线\frac{x-2}{3}=\frac{y+1}{-4}=\frac{z}{1}垂直，且与直线\frac{x+1}{1}=\frac{y-3}{1}=\frac{z}{2}相交的直线方程$$

$$求过点M与直线l_1垂直的平面 \\
3(x+1)-4(y-0)+(z-1)=0 \\
l_2:\begin{cases}
x=-1+t \\
y=3+t \\
z=2t
\end{cases}代入平面得t=13,P(12,16,26) \\
\vec{MP}=(13,16,25) 直线：\frac{x+1}{13}=\frac{y}{16}=\frac{z-1}{25}$$

例12🌰.$$求平行于x轴且通过两点M(1,1,1)与点N(2,3,4)的平面方程$$

$$取x轴向量\vec{i}=(1,0,0) \\
\vec{MN}=(1,2,3) \\
取\vec{n}=\vec{i}×\vec{MN}=(0,-3,2)，取M(1,1,1)得平面 \\
0(x-1)-3(y-1)+2(z-1)=0$$


