---
layout: 		post
title: 			"高等数学_2"
subtitle: 		'导数与微分'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
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

$$(secx)'=(\frac{1}{cosx})'=\frac{sinx}{cos^2x}=secxtanx$$

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

$$\therefore\phi'(y)=\frac{1}{f'(x)}$$

11.$$y=arcsinx(-1<x<1),x=siny$$

$$y'=\frac{1}{x'}$$

$$(arcsinx)'=\frac{1}{cosy}=\frac{1}{\sqrt{1-sin^2y}}=\frac{1}{\sqrt{1-x^2}}$$

$$\therefore(arcsinx)'=\frac{1}{\sqrt{1-x^2}}$$

12.$$y=arccosx(-1<x<1,0<y<\pi),x=cosy$$

$$(arccosx)'=-\frac{1}{siny}=-\frac{1}{\sqrt{1-cos^2y}}=-\frac{1}{\sqrt{1-x^2}}$$

$$\therefore(arccosx)'=-\frac{1}{\sqrt{1-x^2}}$$

13.$$y=arctanx(-\infty<x<+\infty,-\frac{\pi}{2}<y<\frac{\pi}{2}),x=tany$$

$$(arctanx)'=\frac{1}{sec^2y}=\frac{1}{1+tan^2y}=\frac{1}{1+x^2}$$

$$\therefore(arctanx)'=\frac{1}{1+x^2}$$

14.$$y=arccotx,x=coty$$

$$(arccotx)'=\frac{1}{-csc^2x}=-\frac{1}{1+cot^2y}=-\frac{1}{1+x^2}$$

$$\therefore(arccotx)'=-\frac{1}{1+x^2}$$

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
Th3.$$y=f(u)可导,u=\phi(x)可导且\phi'(x)\neq0,则y=f[\phi(x)]关于x可导,且$$

$$\frac{dy}{dx}=f'(u)·\phi'(x)=f'[\phi(x)]\phi'(x)=\frac{dy}{du}·\frac{du}{dx}$$

$$证：\phi'(x)=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta u}{\Delta x}\neq0\Rightarrow\Delta u=O(\Delta x)$$

$$f'(u)=\lim\limits_{\Delta u\rightarrow0}\frac{\Delta y}{\Delta u}$$

$$\frac{dy}{dx}=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}=\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta u}·\frac{\Delta u}{\Delta x}$$

$$\because u=O(\Delta x)$$

$$=\lim\limits_{\Delta u\rightarrow0}\frac{\Delta y}{\Delta u}·\frac{\Delta u}{\Delta x}$$

$$=f'(u)·\phi'(x)=f'[\phi(x)]\phi'(x)$$

例1🌰.$$y=e^{x^3}求\frac{dy}{dx}$$

$$解：y=e^u,u=x^3$$

$$\frac{dy}{dx}=\frac{dy}{du}·\frac{du}{dx}=e^u·3x^2=3x^2e^{x^3}$$

例2🌰.$$y=sin\frac{2x}{1+x^2},求\frac{dy}{dx}$$

$$解：y=sinu,u=\frac{2x}{1+x^2}$$

$$\frac{dy}{dx}=cosu·\frac{2(1+x^2)-4x^2}{(1+x^2)^2}$$

$$=cos\frac{2x}{1+x^2}·\frac{2(1-x^2)}{(1+x^2)^2}$$

例3🌰.$$y=\sqrt[3]{1-2x^2},求\frac{dy}{dx}$$

$$=-\frac{4}{3}x(1-2x^2)^{-\frac{2}{3}}$$

例4🌰.$$y=e^{sin\frac{1}{x}},求\frac{dy}{dx}$$

$$y'=e^{sin\frac{1}{x}}·cos\frac{1}{x}·(-\frac{1}{x^2})$$

例5🌰.$$y=(1+x^2)^{sinx},\frac{dy}{dx}=?$$

$$y=e^{sinx·\ln(1+x^2)}$$

$$\frac{dy}{dx}=e^{sinx·\ln(1+x^2)}·[(sinx)'·\ln(1+x^2)+sinx(ln(1+x^2))']$$

$$=e^{sinx·\ln(1+x^2)}[cosx·\ln(1+x^2)+sinx·\frac{1}{1+x^2}·2x]$$

例6🌰.$$y=a^{x^a},\frac{dy}{dx}=?$$

$$y=e^{x^a\ln a}$$

$$\frac{dy}{dx}=a\ln a·x^{a-1}·a^{x^a}$$

#### 高阶导数
$$如：y=x^3,y'=3x^2,y''=6x$$

$$y=f(x)的导数为f'(x),f'(x)的导数被称为f(x)的二阶导数,记f''(x)或\frac{d^2y}{dx^2}$$

一阶导数：$$f'(x)或\frac{dy}{dx}$$  
二阶导数：$$f''(x)或\frac{d^2y}{dx^2}=\frac{d}{dx}(\frac{dy}{dx})$$  
三阶导数：$$f'''(x)或\frac{d^3y}{dx^3}$$  
四阶导数：$$f^{(4)}(x)或\frac{d^4y}{dx^4}$$  

例1🌰.$$y=sin3x,求y^{(4)}$$

$$y'=3cos3x$$

$$y''=-9sin3x$$

$$y'''=-27cos3x$$

$$y^{(4)}=81sin3x$$

例2🌰.$$y=\frac{1}{3x+4},y^{(n)}$$

$$y=(3x+4)^{-1}$$

$$y=(-1)(3x+4)^{-2}·3$$

$$y=(-1)(-2)(3x+4)^{-3}·3^2$$

$$...$$  

$$y^{(n)}=(-1)(-2)...(-n)(3x+4)^{-(n+1)}·3^n$$

$$=\frac{(-1)^n·n!·3^n}{(3x+4)^{n+1}}$$

总结：

$$(uv)'=u'v+uv'$$

$$(uv)''=u''v+2u'v'+uv''$$

$$...$$

$$(uv)^{(n)}=C_n^0u^{(n)}v+C_n^1u^{(n-1)}v'+...+C_n^nuv^{(n)}$$

#### 隐函数及参数方程确定的函数的导数

函数表达方法：  
1. 显函数 y=f(x)
2. 隐函数$$F(x \vert y)=0\Rightarrow y=\phi(x)$$
3. $$参数形式 \begin{cases}
x =\phi(t) \\
y = \Phi(t)
\end{cases}$$

显函数求导：  

$$y=e^{sin^2\frac{1}{x}}$$

$$\frac{dy}{dx}=e^{sin^2\frac{1}{x}}·2sin\frac{1}{x}·cos\frac{1}{x}·(-\frac{1}{x^2})$$

$$=-\frac{1}{x^2}·e^{sin^2\frac{1}{x}}·sin\frac{2}{x}$$

隐函数求导：  

$$F(x|y)=0，将y看作\phi(x)$$

例1🌰.$$求e^y+xy-e=0$$

$$\Rightarrow e^y·\frac{dy}{dx}+y+x·\frac{dy}{dx}=0$$

$$\Rightarrow\frac{dy}{dx}=-\frac{y}{x+e^y}$$

例2🌰.$$y^5+2y-x-3x^7=0\Rightarrow y=y(x)，求\frac{dy}{dx}\vert_{x=0}$$

$$1.x=0\Rightarrow y=0$$

$$2.5y^4·\frac{dy}{dx}+2\frac{dy}{dx}-1-21x^6=0$$

$$3.x=0,y=0代入，\frac{dy}{dx}|_{x=0}=\frac{1}{2}$$

例3🌰.$$求\frac{x^2}{16}+\frac{y^2}{9}=1在(2,\frac{3}{2}\sqrt{3})处的切线$$

$$解：1.\frac{x^2}{16}+\frac{y^2}{9}=1\Rightarrow\frac{x}{8}+\frac{2y}{9}·\frac{dy}{dx}=0$$

$$2.将(2,\frac{3}{2}\sqrt{3})代入$$

$$\frac{dy}{dx}\vert_{(2,\frac{3}{2}\sqrt{3})}=-\frac{\sqrt{3}}{4}$$

$$切线：y=2\sqrt{3}-\frac{\sqrt{3}}{4}x$$

例4🌰.$$y=x^{sinx},\frac{dy}{dx}=?$$

$$方法1.y=e^{sinx\ln x}$$

$$y'=e^{sinx\ln x}·(cosx·\ln x+\frac{sinx}{x})$$

$$=x^{sinx}(cosx·\ln x+\frac{sinx}{x})$$

$$方法2.y=e^{sinx\ln x}\Rightarrow \ln y=sinx·lnx$$

$$\frac{1}{y}\frac{dy}{dx}=cosx·\ln x+\frac{sinx}{x}$$

$$\frac{dy}{dx}=x^{sinx}(cosx·\ln x+\frac{sinx}{x})$$

例5🌰.$$y=\sqrt{\frac{(x-1)(x-2)}{(x-3)(x-4)}}$$

$$解：\ln y=\frac{1}{2}[\ln(x-1)+\ln(x-2)-\ln(x-3)\ln(x-4)]$$

$$\frac{1}{y}·\frac{dy}{dx}=\frac{1}{2}(\frac{1}{x-1}+\frac{1}{x-2}-\frac{1}{x-3}-\frac{1}{x-4})$$

例6🌰.$$2^{xy}+2x=y,y''(0)=?$$

$$解：1.x=0\Rightarrow y=1$$

$$2.2^{xy}·\ln2·(y+x\frac{dy}{dx})+2=\frac{dy}{dx}$$

$$代入x=0,y=1,y'(0)=\ln2+2$$

$$\ln2[2^{xy}·ln2·(y+x\frac{dy}{dx})^2+2^{xy}·(2\frac{dy}{dx}+x\frac{d^2y}{dx^2})]=\frac{d^2y}{dx^2}$$

$$将x=0,y=1,y'(0)=\ln2+2代入得$$

$$y''(0)=\ln2(\ln2+2\ln2+4)$$

参数形式：  

1.$$\begin{cases}
x =\phi(t) \\
y = \Phi(t)
\end{cases},\phi(t)、\Phi(t)可导，且\phi(t)\neq0$$

$$\frac{dy}{dx}=\frac{dy/dt}{dx/dt}=\frac{\Phi'(t)}{\phi'(t)}$$

2.$$\phi(t)、\Phi(t)二阶可导，且\phi(t)\neq0$$


$$\frac{dy}{dx}=\frac{dy/dt}{dx/dt}=\frac{\Phi'(t)}{\phi'(t)}$$

$$\frac{d^2y}{dx^2}=\frac{d(\frac{dy}{dx})}{dx}=\frac{d[\frac{\Phi'(t)}{\phi'(t)}]}{dx}$$

$$=\frac{d^2y}{dx^2}=\frac{d(\frac{dy}{dx})}{dx}=\frac{d[\frac{\Phi'(t)}{\phi'(t)}]/dt}{dx/dt}$$

$$=\frac{[\frac{\Phi'(t)}{\phi'(t)}]'}{\phi'(t)}$$

例1🌰.$$\begin{cases}
x =arctant \\
y = \ln(1+t^2)
\end{cases}求\frac{dy}{dx},\frac{d^2y}{dx^2}$$

$$解：\frac{dy}{dx}=2t$$

$$\frac{d^2y}{dx^2}=\frac{d(2t)/dt}{dx/dt}=2(1+t^2)$$

#### 函数的微分

🌰.$$y=x^2,x_0=3$$

$$\Delta y=y(3+\Delta x)-y(3)=(3+\Delta x)^2-9$$

$$=6\Delta x+(\Delta x)^2=6\Delta x+o(\Delta x)$$

def-$$y=f(x)(x\in D),x_0\in D,\Delta y=f(x_0+\Delta x)-f(x_0)$$

$$If=A\Delta x+o(\Delta x)$$

$$则称f(x)在x=x_0处可微$$

$$A\Delta x为y=f(x)在x=x_0处的微分，记作dy|_{x=x_0}$$

Notes:  
$$1.可导\Leftrightarrow可微$$

$$证\Rightarrow 设f(x)在x=x_0可导，则$$

$$\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}=f'(x_0)\Rightarrow\frac{\Delta y}{\Delta x}=f'(x_0)+\alpha(\alpha\rightarrow0\Delta x\rightarrow 0)$$

$$\Delta y=f'(x_0)\Delta x+\alpha\Delta x$$

$$\because\lim\limits_{\Delta x\rightarrow0}\frac{\alpha\Delta x}{\Delta x}=0,\therefore\alpha\Delta x=o(\Delta x)$$

$$\therefore\Delta y=f'(x_0)\Delta x+o(\Delta x),即y=f(x)在x=x_0处可微$$

$$证\Leftarrow 设f(x)在x=x_0可微，则$$

$$\Delta y = A\Delta x+o(\Delta x)$$

$$\Rightarrow \frac{\Delta y}{\Delta x}=A+\frac{o(\Delta x)}{\Delta x}$$

$$\therefore\lim\limits_{\Delta x\rightarrow0}\frac{\Delta y}{\Delta x}=A=f'(x_0)$$

2.$$\Delta y=A\Delta x+o(\Delta x)，则A=f'(x_0)$$

3.$$设y=f(x)可导，则$$

$$dy=df(x)=f'(x)dx$$


一、近似计算
$$\Delta y=f'(x_0)\Delta x+o(\Delta x)$$

$$f(x_0+\Delta x)-f(x_0)=f'(x_0)\Delta x+o(\Delta x)$$

$$f(x_0+\Delta x)-f(x_0)\approx f'(x_0)\Delta x$$

$$\therefore f(x_0+\Delta x)\approx f(x_0)+f'(x_0)\Delta x$$

例1🌰.$$\sqrt{4.003}\approx?$$

$$解：f(x)=\sqrt{x},x_0=4,\Delta x=0.003$$

$$f(4)=2,f'(x)=\frac{1}{2\sqrt{x}},f'(4)=\frac{1}{4}$$

$$\therefore\sqrt{4.003}=f(4+0.003)\approx f(4)+f'(4)*0.003$$

$$=2+\frac{1}{4}*0.003$$