---
layout: 		post
title: 			"高等数学_5"
subtitle: 		'定积分'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---
## 定积分
#### 定积分的基本概念
假设有一条曲线y=f(x)，求其在[a,b]范围内与x轴围成的面积。  
1.$$a=x_0<x_1<...<x_n=b$$  

$$[a,b]=[x_0,x_1]\cup..\cup[x_{n-1},x_n]$$

2.$$\forall \xi_i\in[x_{i-1},x_i]$$

$$\Delta S_i\approx f(\xi_i)\Delta x_i$$

$$S\approx\sum^n_{i=1}f(\xi_i)\Delta X_i$$

3.$$\lambda=max\{\Delta x_1,\Delta x_2,...,\Delta x_n\}$$

$$S=\lim\limits_{\lambda\rightarrow0}\sum^n_{i=1}f(\xi_i)\Delta X_i$$

#### 定积分的定义  
f(x)在[a,b]上有界
1.$$a=x_0<x_1<...<x_n=b$$

2.$$\forall\xi_i\in[x_{i-1},x_i],作\sum^n_{n=1}f(\xi_i)\Delta x_i$$

3.$$\lambda=max\{\Delta x_1,...,\Delta x_n\}$$

$$若\lim\limits_{\lambda\rightarrow0}\sum^n_{i=1}f(\xi_i)\Delta X_i\exists$$

$$得f(x)在[a,b]上可积,极限值记\int^b_af(x)dx$$

$$即\int^b_af(x)dx \triangleq \lim\limits_{\lambda\rightarrow0}\sum^n_{i=1}f(\xi_i)\Delta X_i$$

Notes:  
1.$$\lim\limits_{\lambda\rightarrow0}\sum^n_{i=1}f(\xi_i)\Delta X_i与\begin{cases}
[a,b]分法 \\
\xi_i取法
\end{cases}无关$$  
2.$$\lambda\rightarrow0\Rightarrow n\rightarrow\infty$$(反之错误)  
3.$$f(x)有界为可积的必要条件$$  
4.设f(x)在[0,1]上可积。  

$$[0,1]=[0,\frac{1}{n}]\cup...\cup[\frac{n-1}{n},\frac{n}{n}]$$

$$\lambda=\frac{1}{n},\lambda\rightarrow0\Leftrightarrow n\rightarrow\infty$$

$$\xi_1=\frac{1}{n},\xi_2=\frac{2}{n},...,\xi_n=\frac{n}{n}$$

$$\lim\limits_{\lambda\rightarrow0}\sum^n_{i=1}f(\xi_i)\Delta X_i=\int^1_0f(x)dx$$


$$\lim\limits_{n\rightarrow\infty}\frac{1}{n}\sum^n_{i=1}f(\frac{i}{n})=\int^1_0f(x)dx$$

例1🌰.$$\lim\limits_{n\rightarrow\infty}(\frac{1}{\sqrt{n^2+1}}+\frac{1}{\sqrt{n^2+2^2}}+...+\frac{1}{\sqrt{n^2+n^2}})$$

$$=\lim\limits_{n\rightarrow\infty}\frac{1}{n}\sum^n_{i=1}\frac{1}{\sqrt{(\frac{i}{n})^2+1}}$$

$$=\int^1_0\frac{1}{\sqrt{x^2+1}}dx=\ln(x+\sqrt{x^2+1})|^1_0=\ln(1+\sqrt{2})$$

#### 基本定理
1.定积分与$$\begin{cases}
上下限 \\
函数关系
\end{cases}有关,与积分变量无关，即\\ 
\int^b_af(x)dx=\int^b_af(t)dt$$

2.$$在函数f(x)定义域内取范围[a,b]，并在此范围内任取一点x\\
可得\int^x_af(x)dx=\int^x_af(t)dt\triangleq\phi(x)(积分上限公式)$$

Notes:  
1.$$\int^x_af(x)dx表达式中的x与上限的x不同$$  
2.$$\int^x_af(x,t)dt表达式中的x与上限的x相同$$

Th1.$$f(x)\in c[a,b],\phi(x)=\int^x_af(t)dt\\
则\phi'(x)=f(x)$$

Notes:  
1.$$\frac{d}{dx}\int^{\phi(x)}_af(t)dt=f[\phi(x)]\phi'(x)$$  
2.$$\frac{d}{dx}\int^{\phi_2(x)}_{\phi_1(x)}f(t)dt=f[\phi_2(x)]\phi'_2(x)-f[\phi_1(x)]\phi'_1(x)$$

例1🌰.$$\lim\limits_{x\rightarrow0^+}\frac{\int^x_0\sqrt{x-t}dt}{\sqrt{x}sinx}$$

$$解：\sqrt{x}sinx \thicksim x^{\frac{3}{2}}\\
\int^x_0\sqrt{x-t}dt,设u=x-t\\
得\int^0_x\sqrt{u}(-du)\\
=\int^x_0\sqrt{u}du=\frac{2}{3}u^{\frac{3}{2}}|^x_0=\frac{2}{3}x^{\frac{3}{2}}\\
\therefore原式=\frac{2}{3}$$

例2🌰.$$\lim\limits_{x\rightarrow0}\frac{\int^x_0tcostdt+cosx-1}{e^{-x^2}-1+x^2}$$

$$解：e^x=1+x+\frac{x^2}{2!}+o(x^2)\\
e^{-x^2}=1-x^2+\frac{x^4}{2}+o(x^4)\\
e^{-x^2}-1+x^2\thicksim\frac{1}{2}x^4\\
原式=\lim\limits_{x\rightarrow0}\frac{\int^x_0costdt+cosx-1}{\frac{1}{2}x^4}\\
(洛必塔法则)=\lim\limits_{x\rightarrow0}\frac{xcosx-sinx}{2x^3}\\
=\lim\limits_{x\rightarrow0}\frac{cosx-xsinx-cosx}{6x^2}=-\frac{1}{6}$$

例3🌰.$$f(x)连续，f(0)=0,f'(0)=\pi\\
\lim\limits_{x\rightarrow0}\frac{\int^x_0t(x-t)dt}{x^3}$$

$$解：设x-t=u \\
f^0_x(x-u)f(u)(-du) \\
=f^x_0(x-u)f(u)du \\
=xf^x_0f(u)du-f^x_0uf(u)du \\

原式=\lim\limits_{x\rightarrow0} \frac{f^x_0f(u)du+xf(x)-xf(x)}{3x^2} \\
=\lim\limits_{x\rightarrow0}\frac{f(x)}{6x} \\
=\frac{1}{6}\lim\limits_{x\rightarrow0}\frac{f(x)-f(0)}{x} \\
\frac{1}{6}f'(0)=\frac{\pi}{6}$$
