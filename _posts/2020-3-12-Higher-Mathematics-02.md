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

1)一般函数
1.$$f(x)=c$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}=\lim\limits_{h\rightarrow0}\frac{c-c}{h}=0$$

$$\therefore(c)'=0$$

2.$$f(x)=x^n$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{f(x+h)-f(x)}{h}=\lim\limits_{h\rightarrow0}\frac{(x+h)^n-x^n}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{x^n+c_n^1x^{n-1}h+...+c_n^n h^n-x^n}{h}=nx^{n-1}$$

$$\therefore(x^n)'=nx^{n-1}$$

$$一般的,(x^a)'=ax^{a-1}$$

3.$$f(x)=a^x(a>0切a\neq1)$$

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

2）三角函数
5.$$f(x)=sinx$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{sin(x+h)-sinx}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{2cos(x+\frac{h}{2})·sin\frac{h}{2}}{h}$$

$$=\lim\limits_{h\rightarrow0}cos(x+\frac{h}{2})·\frac{sin\frac{h}{2}}{\frac{h}{2}}=cosx$$

$$\therefore(sinx)'=cosx$$

6.$$f(x)=cosx$$

$$f'(x)=\lim\limits_{h\rightarrow0}\frac{cos(x+h)-cosx}{h}$$

$$=\lim\limits_{h\rightarrow0}\frac{-2sin(x+\frac{h}{2})·sin\frac{h}{2}}{h}$$

$$=-\lim\limits_{h\rightarrow0}sin(x+\frac{h}{2})·\frac{sin\frac{h}{2}}{\frac{h}{2}}=-sinx$$

$$\therefore(cosx)'=-sinx$$

7.$$f(x)=tanx$$

$$(tanx)'=(\frac{sinx}{cosx})'=\frac{(sinx)'cosx-sinx(cosx)'}{cos^2x}$$

$$=\frac{1}{cos^2x}=sec^2x$$

$$\therefore(tanx)'=sec^2x$$

8.$$f(x)=cotx$$

$$(cotx)'=(\frac{cosx}{sinx})'=-\frac{1}{sin^2x}=-csc^2x$$

$$\therefore(cotx)'=-csc^2x$$

9.$$f(x)=secx$$

$$(secx)'=(\frac{1}{cosx})=\frac{sinx}{cos^2x}=secxtanx$$

$$\therefore(secx)'=secxtanx$$

10.$$f(x)=cscx$$

$$(cscx)'=-\frac{cosx}{sin^2x}=-cscxcotx$$

$$\therefore(cscx)'=-cscxcotx$$

3）反函数

Th1.$$y=f(x)\Rightarrow x=\phi(y)$$

例1🌰.$$求y=\ln(x+\sqrt{1+x^2})的反函数$$

$$解：y=\ln(x+\sqrt{1+x^2})\Rightarrow x+\sqrt{1+x^2}=e^y$$

$$\because-x+\sqrt{1+x^2}=e^{-y}$$

$$\therefore 2x=e^y-e^{-y}$$

$$\therefore x=\frac{e^y-e^{-y}}{2}$$

Th2.$$y=f(x)可导且f'(x)\neq0,x=\phi(y)为反函数，则\phi(y)可导，且\phi'(y)=\frac{1}{f'(x)}$$

$$证：f'(x)=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}\neq0\Rightarrow\Delta y=O(\Delta x)(同阶无穷小)$$

$$\phi'(y)=\lim\limits_{\Delta y\rightarrow0}\frac{\Delta x}{\Delta y}=\frac{1}{f'(x)}$$

$$\therefore\phi'(y)=f'(x)$$

Notes:
1.$$F'(X)\exists\Rightarrow f_-'(x_0)、f_+'(x_0)\exists且相等$$

2.$$设f(x)连续,若\lim\limits_{x\rightarrow a}\frac{f(x)-b}{x-a}=A,则f(a)=b,f'(a)=A$$

3.y=f(x)在x=a处的切线为：$$y-f(a)=f'(a)(x-a)$$

4.$$f(x)在x=x_0处可导\Rightarrow f(x)在x=x_0处连续,反过来不正确$$

5.三角的和差化积
![](/img/in-posts/20200319-sumToMul.png)

#### 函数的求导法则
初等函数-$$由\begin{cases}
常数 \\
基本初等函数
\end{cases}经过有限次的\begin{cases}
四则 \\
复合
\end{cases}而成的式子$$

一、基本公式    
$$1.(c)'=0$$  
$$2.(x^a)'=ax^{a-1}$$  
$$3.(a^x)'=a^x\ln a$$  
$$4.(\log_ax)'=\frac{1}{x\ln a}$$  
$$5.三角函数$$  
$$6.反三角函数$$  

二、四则求导法则  
若u(x)、v(x)可导，则  
$$1.[u(x)\pm v(x)]'=u'(x)\pm v'(x)$$  
$$2.[u(x)v(x)]'=u'(x)v(x)+u(x)v'(x)$$  
$$3.[\frac{u(x)}{v(x)}]'=\frac{u'(x)v(x)-u(x)v'(x)}{v^2(x)}(v(x)\neq0)$$  

证明1：令f(x)=u(x)+v(x)

$$f'(x)=\lim\limits_{h \rightarrow 0}\frac{f(x+h)-f(x))}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{u(x+h)+v(x+h)-u(x)-v(x)}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{\Delta u+\Delta v}{h}$$

$$=u'(x)+v'(x)$$

$$即(u+v)'=u'+v'，同理(u-v)'=u'-v'$$

证明2：f(x)=u(x)v(x)

$$f'(x)=\lim\limits_{h \rightarrow 0}\frac{f(x+h)-f(x))}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{u(x+h)v(x+h)-u(x)v(x)}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{u(x+h)v(x+h)-u(x)v(x+h)+u(x)v(x+h)-u(x)v(x)}{h}$$

$$=\lim\limits_{h \rightarrow 0}[\frac{\Delta u}{h}·v(x+h)+u(x)·\frac{\Delta v}{h}]$$

$$=u'(x)v(x)+u(x)v'(x)$$

$$即(uv)'=u'v+uv'$$

证明3：f(x)=\frac{u(x)}{v(x)}

$$f'(x)=\lim\limits_{h \rightarrow 0}\frac{f(x+h)-f(x))}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{\frac{u(x+h)}{v(x+h)}-\frac{u(x)}{v(x)}}{h}$$

$$=\lim\limits_{h \rightarrow 0}\frac{1}{v(x)v(x+h)}*\frac{u(x+h)v(x)-u(x)v(x+h)}{h}$$

$$=\frac{1}{v^2(x)}\lim\limits_{h\rightarrow0}\frac{u(x+h)v(x)-u(x)v(x)+u(x)v(x)-u(x)v(x+h)}{h}$$

$$=\frac{1}{v^2(x)}\lim\limits_{h\rightarrow0}\frac{\Delta u}{h}v(x)-u(x)\frac{\Delta v}{h}$$

$$=\frac{u'(x)v(x)-u(x)v'(x)}{v^2(x)}$$

$$即(\frac{u}{v})'=\frac{u'v-uv'}{v^2}$$

Notes:
1.(ku)'=ku'(k为常数)
2.(uvw)'=u'vw+uv'w+uvw'

例1🌰.f(x)=x(x+1)(x+2)...(x+100),求f'(0)=?

方法一：  

$$f'(0)=\lim\limits_{x\rightarrow0}\frac{f(x)-f(0)}{x}=\lim\limits_{x\rightarrow0}(x+1)(x+2)...(x+100)=100!$$

方法二：

$$f'(x)=(x+1)...(x+100)+x(x+2)...(x+100)+...+x(x+1)(x+99)$$

$$\therefore f'(0)=100!$$

三、复合函数求导法则





