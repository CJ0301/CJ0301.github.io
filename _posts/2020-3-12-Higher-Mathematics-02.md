---
layout: 		post
title: 			"高等数学_2"
subtitle: 		'导数与微分'
author: 		"CJ"
header-img: 	"img/post-bg-fblog.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---
## 导数与微分
#### 导数的概念
举一个🌰：
如图,y=f(x)
![](/img/in-posts/20200312-line.png)
$$K_{M_0M}=\frac{f(a+\Delta x)-f(a)}{\Delta x}=\frac{\Delta y}{\Delta x},M_0(a,f(a)),M(a+\Delta x,f(a+\Delta x))$$

过M_0做曲线的切线

$$K_切=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}$$

一、导数的定义  

$$y=f(x)(x\in D),x_0\in D,x_0+\Delta x\in D$$

$$\Delta y=f(x_0+\Delta x)-f(x_0)$$

$$若\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}\exists,则f(x)在x_0可导,极限值为f(x)在x_0处的导数,记f'(x_0),\frac{dy}{dx}|_{x=x_0}$$

$$即\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}=f'(x_0)$$

Notes:
1. 等价定义：

$$f'(x_0)=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}=\lim\limits_{\Delta x\rightarrow0}\frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}$$

$$f'(x_0)=\lim\limits_{x\rightarrow x_0}\frac{f(x)-f(x_0)}{x-x_0}$$

$$f(x)在x=x_0可导\Rightarrow f(x)在x=x_0处连续$$

$$\Delta x\rightarrow 0\begin{cases}
\Delta x\rightarrow0^- \\
\Delta x\rightarrow0^+
\end{cases},x\rightarrow a\begin{cases}
x\rightarrow a^- \\
x\rightarrow a^+
\end{cases}$$

例1🌰. $$ f(x) = \vert x\vert,证f'(x)是否存在 $$

$$解:f_-'(0)=\lim\limits_{x\rightarrow0^-}\frac{f(x)-f(0)}{x-0}=\lim\limits_{x\rightarrow0^-}\frac{|x|}{x}=-1$$

$$f_+'(0)=\lim\limits_{x\rightarrow0^+}\frac{f(x)-f(0)}{x-0}=\lim\limits_{x\rightarrow0^+}\frac{|x|}{x}=1$$

$$\because f_-'(0)\neq f_+'(0),\therefore f'(x)不存在$$

二、用定义求导数
1.$$y=f(x)=c$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}=\lim\limits_{h\rightarrow0}\frac{c-c}{h}=0$$

$$\therefore(c)'=0$$

2.$$y=f(x)=x^n$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}=\lim\limits_{h\rightarrow0}\frac{(x+h)^n-x^n}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{x^n+c_n^1x^{n-1}h+...+c_n^n h^n-x^n}{h}=nx^{n-1}$$

$$\therefore(x^n)'=nx^{n-1}$$

$$一般的,(x^a)'=ax^{a-1}$$

3.$$y=a^x(a>0切a\neq1)$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}=\lim\limits_{h\rightarrow0}\frac{a^{x+h}-a^x}{h}$$

$$=a^x\lim\limits_{h\rightarrow0}\frac{a^h-1}{h}=a^x\lim\limits_{h\rightarrow0}\frac{e^{h\ln a}-1}{h}$$

$$=a^x\ln a$$

$$\therefore(a^x)'=a^x\ln a$$

4.$$f(x)=log_ax(a>0且a\neq1)$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{\log_a(x+h)-\log_ax}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{1}{h}\log_a(1+\frac{h}{x})$$

$$=\lim\limits_{h\rightarrow0}\log_a[(1+\frac{h}{x})^{\frac{x}{h}}]^{\frac{1}{x}}$$

$$=\log_a(e^{\frac{1}{x}})=\frac{1}{x}\log_ae=\frac{1}{x\ln a}$$

$$\therefore(\log_ax)'=\frac{1}{x\ln a}$$

Notes:
1.$$F'(X)\exists\Rightarrow f_-'(x_0)、f_+'(x_0)\exists且相等$$

2.$$设f(x)连续,若\lim\limits_{x\rightarrow a}\frac{f(x)-b}{x-a}=A,则f(a)=b,f'(a)=A$$

3.y=f(x)在x=a处的切线为：y-f(a)=f'(a)(x-a)

4.$$f(x)在x=x_0处可导\Rightarrow f(x)在x=x_0处连续,反过来不正确$$

#### 函数的求导法则