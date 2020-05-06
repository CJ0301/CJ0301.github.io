---
layout: 		post
title: 			"高等数学_4"
subtitle: 		'不定积分'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---

## 不定积分
#### 不定积分的概念与性质
一、概念  
1、原函数
$$设f(x)、F(x)(x\in I)$$  

$$若\forall x\in I,有F'(X)=f(X)$$

$$则F(x)为f(x)的原函数$$

注：  
1.连续函数一定存在原函数。  
2.$$若f(x)存在原函数，则\exists无数个原函数，任两个原函数相差常数。$$

2、不定积分
$$设F(x)为f(x)的一个原函数，F(x)+c为f(x)的所有原函数，称为f(x)的不定积分，记\int f(x)dx，即\int f(x)dx=F(x)+c$$

注：  
1.$$\int\frac{d}{dx}f(x)dx=\int f'(x)dx=f(x)+c$$  
2.$$\frac{d}{dx}\int f(x)dx=\frac{d}{dx}[F(X)+c]=f(x)$$

例1🌰.$$\int x^{\frac{1}{2}}dx=\frac{2}{3}x^{\frac{3}{2}}+c$$

例2🌰.$$\int\frac{1}{x}dx$$

$$解：x>0时，(\ln x)'=\frac{1}{x},\int\frac{1}{x}dx=\ln x+c$$

$$x<0时，[\ln(-x)]'=\frac{1}{-x}*(-1)=\frac{1}{x}，\int\frac{1}{x}dx=\ln(-x)+c$$

$$\therefore\int\frac{1}{x}dx=\ln|x|+c$$

二、积分表(部分)  
1.$$\int kdx=kx+c$$  

2.$$\int x^a dx=\begin{cases}
\frac{1}{a+1}x^{a+1}+c & a\neq-1 \\
\ln|x|+c & a=-1
\end{cases}$$  

3.$$\int a^x dx=\begin{cases}
\frac{a^x}{\ln a} & a\neq e \\
e^x+c & a=e
\end{cases}$$  

4.三角函数$$\begin{cases}
\int sinx dx = -cosx+c \\
\int cosx dx = sinx+c \\
\int tanx dx = -\ln|cosx|+c\\
\int cotx dx = \ln|sinx|+c\\
\int secx dx = \ln|cscx-cotx|+c\\
\int cscx dx = \ln|secx+tanx|+c\\
\int sec^2x dx = tanx+c \\
\int csc^2x dx = -cotx+c \\
\int secxtanx dx = secx+c \\
\int cscxcotxdx = -cscx+c \\
\end{cases}$$  

🔥. $$\int tanx dx 推导：$$

$$\int tanx dx = \int\frac{sinx}{cosx}dx$$

$$=-\int\frac{1}{cosx}d(cosx)$$

$$设cosx=t$$

$$-\int\frac{1}{t}dt=-\int|t|+c=-\ln|cosx|+c$$

$$\therefore \int tanx dx = -\ln|cosx|+c$$

🔥. $$\int cotx dx 推导：$$

$$\int cotx dx=\int\frac{cosx}{sinx}dx=\int\frac{1}{sinx}d(sinx)=\ln|sinx|+c$$

$$\therefore\int cotxdx=\ln|sinx|+c$$

🔥. $$\int cscx dx 推导：$$

$$\int cscx dx=\int\frac{1}{sinx}dx=\int\frac{1}{2sin\frac{x}{2}cos\frac{x}{2}}dx$$

$$=\int\frac{1}{tan\frac{x}{2}cos\frac{x}{2}}d(\frac{x}{2})=\int\frac{sec^2\frac{x}{2}}{tan\frac{x}{2}}d(\frac{x}{2})$$

$$设\frac{x}{2}=t$$

$$\int\frac{sec^2t}{tant}dt$$

$$=\frac{1}{tant}=d(tant)$$

$$=\ln|tant|+c=\ln|tan\frac{x}{2}|+c$$

$$\because tan\frac{x}{2}=\frac{sin\frac{x}{2}}{cos\frac{x}{2}}=\frac{2·\frac{1-cosx}{2}}{sinx}$$

$$=\frac{1-cosx}{sinx}=cscx-cotx$$

$$\therefore\int cscx dx=\ln|cscx-cotx|+c$$

🔥. $$\int secx dx 推导：$$

$$\int secx dx=\int\frac{1}{cosx}dx=\int\frac{1}{sin(x+\frac{\pi}{2})}dx$$

$$\int csc(x+\frac{\pi}{2})d(x+\frac{\pi}{2})$$

$$\ln|csc(x+\frac{\pi}{2}-cot(\frac{\pi}{2}))|+c$$

$$=\ln|secx+tanx|+c$$

$$\therefore\int secx dx=\ln|secx+tanx|+c$$

5.平方和差$$\begin{cases}
\int \frac{1}{\sqrt{1-x^2}}dx=arcsinx+c \\
\int \frac{1}{\sqrt{a^2-x^2}}dx=arcsin\frac{x}{a}+c \\
\int \frac{1}{1+x^2}dx = arctanx+c \\
\int \frac{1}{a^2+x^2}dx = \frac{1}{a}arctanx+c \\
\int \frac{1}{x^2-a^2}dx = \frac{1}{2a}\ln|\frac{x-a}{x+a}|+c \\
\int\frac{1}{\sqrt{x^2+a^2}}dx=\ln(x+\sqrt{x^2+a^2})+c \\
\int\frac{1}{\sqrt{x^2-a^2}}dx=\ln|x+\sqrt{x^2-a^2}|+c \\
\int\sqrt{a^2-x^2}dx=\frac{a^2}{2}arcsin\frac{x}{a}+\frac{x}{2}\sqrt{a^2-x^2}+c
\end{cases}$$

例1🌰.$$\int\frac{dx}{x^2}$$

$$解：\int\frac{dx}{x^2}=\int x^{-2}dx=-\frac{1}{x}+c$$

例2🌰.$$\int 2^xe^xdx$$

$$解：\int 2^xe^xdx=\int(2e)^xdx=\frac{(2e)^x}{\ln 2e}+c$$

例3🌰.$$\int \frac{1}{\sqrt{a^2-x^2}}dx$$

$$\int \frac{1}{\sqrt{a^2-x^2}}dx=\int \frac{1}{\sqrt{1-(\frac{x}{a})^2}}d(\frac{x}{a})$$

$$=arcsin\frac{x}{a}+c$$

例4🌰.$$\int\frac{1}{x^2-a^2}dx$$

$$原式=\int\frac{1}{(x-a)(x+a)}dx=\frac{1}{2a}\int(\frac{1}{x-a}-\frac{1}{x+a}dx)$$

$$=\frac{1}{2a}[\int\frac{1}{x-a}d(x-a)-\int\frac{1}{x+a}d(x+a)]$$

$$\frac{1}{2a}|\frac{x-a}{x+a}|+c$$

例5🌰.$$\int\frac{dx}{x(1+2\ln x)}$$

$$解：原式=\frac{1}{2}\int\frac{1}{1+2\ln x}d(1+2\ln x)$$

$$=\frac{1}{2}\ln|1+2\ln x|+c$$

例6🌰.$$\int\frac{e^{3\sqrt{x}}}{\sqrt{x}}dx$$

$$解：原式=\frac{2}{3}\int e^{3\sqrt{x}}d(3\sqrt{x})$$

$$=\frac{2}{3}e^{3\sqrt{x}}+c$$

三、性质  
1.$$\int[f(x)\pm g(x)]dx=\int f(x)dx\pm \int g(x)dx$$

$$证：\because(左)'=f(x)\pm g(x)$$

$$又\because(右)'=(\int f(x)dx)'\pm(\int g(x)dx)'$$

$$=f(x)\pm g(x)$$

2.$$\int kf(x)dx=k\int f(x)dx$$

$$证：(左)' = kf(x)$$

$$(右)'=kf(x)$$

$$\therefore \int kf(x)dx=k\int f(x)dx$$

例1🌰.$$\int(x^2+\frac{2}{x}-sinx)dx$$

$$解：\int(x^2+\frac{2}{x}-sinx)dx=\int x^2dx+2\int\frac{1}{x}dx-\int sinxdx$$

$$=\frac{1}{3}x^3+2\ln|x|+cosx+c$$

例2🌰.$$\int\frac{x^4}{1+x^2}dx$$

$$\int\frac{x^4}{1+x^2}dx = \int\frac{x^4-1+1}{1+x^2}dx$$

$$=\int\frac{x^4-1}{1+x^2}dx+\int\frac{1}{1+x^2}dx$$

$$=\int(x^2-1)dx+\int\frac{1}{1+x^2}dx$$

$$=\frac{1}{3}x^3-x+arctanx+c$$

例3🌰.$$\int sin^2\frac{x}{2}dx$$

$$解：\int sin^2\frac{x}{2}dx=\frac{1}{2}\int(1-cosx)dx$$

$$=\frac{1}{2}(x-sinx)+c$$

#### 换元积分法
一、第一类换元积分法

例1🌰.$$\int cos(2x+3)dx$$

$$解：\int cos(2x+3)dx=\frac{1}{2}\int cos(2x+3)d(2x+3)$$

$$设2x+3=t$$

$$=\frac{1}{2}\int costdt=\frac{1}{2}sint+c=\frac{1}{2}sin(2x+3)+c$$

例2🌰.$$\int\frac{x}{(1+x^2)^2}dx$$

$$解：\int\frac{x}{(1+x^2)^2}dx=\frac{1}{2}\int\frac{1}{(1+x^2)^2}d(1+x^2)$$

$$设1+x^2=t$$

$$\frac{1}{2}\int\frac{1}{t^2}dt=-\frac{1}{2t}+c=-\frac{1}{2(1+x^2)}+c$$

例3🌰.$$\int\frac{dx}{\sqrt{x(1-x)}}$$

$$解：原式=2\int\frac{dx}{2\sqrt{x}·\sqrt{1-x}}=2\int\frac{d(\sqrt{x})}{\sqrt{1-(\sqrt{x})^2}}$$

$$设\sqrt{x}=t$$

$$2\int\frac{dt}{\sqrt{1-t^2}}=2arcsint+c=2arcsin\sqrt{x}+c$$

例4🌰.$$\int sec^4xdx$$

$$解：原式=\int sec^2xd(tanx)=\int(tan^2x+1)d(tanx)$$

$$设tanx=t$$

$$\int(1+t^2)dt=\frac{1}{3}t^3+t+c=\frac{1}{3}tan^3x+tanx+c$$

例5🌰.$$\int x^2 e^{x^3}dx$$

$$解：原式=\frac{1}{3}\int e^{x^3}d(x^3)$$

$$设x^3=t$$

$$\frac{1}{3}\int e^tdt=\frac{1}{3}e^{x^3}+c$$

Th1.$$\int f[\phi(x)]\phi'(x)dx=\int f[\phi(x)]d\phi(x)$$  
$$设\phi(x)=t$$  
$$\int f(t)dt=F(t)+c=F[\phi(x)]+c$$  

二、第二类换元积分法  
$$\int f(x)dx,设x=\phi(t),\Rightarrow\int f[\phi(x)]·\phi'(t)dt$$
$$=\int g(t)dt=G(t)+c$$
$$=G[\phi^{-1}(x)]+c$$

(一)$$无理函数\Rightarrow有理函数$$  
注：不一定要转换

例1🌰.$$\int\frac{sin\sqrt{x}}{\sqrt{x}}dx(第一类换元积分法)$$

$$原式=2\int sin\sqrt{x}d(\sqrt{x})$$

$$=-2cos\sqrt{x}+c$$

例2🌰.$$\int\frac{dx}{\sqrt{x}(1+x)}(第一类换元积分法)$$

$$解：原式=2\int\frac{1}{1+(\sqrt{x})^2}d(\sqrt{x})$$

$$=2arctan\sqrt{x}+c$$


例3🌰.$$\int\frac{1}{\sqrt{x}+\sqrt[3]{x}}dx$$

$$设x=t^6$$

$$解：原式=\int\frac{6t^5}{t^3+t^2}dt$$

$$=6\int\frac{(t^3+1)-1}{t+1}dt=6\int(t^2-t+1-\frac{1}{t+1})dt$$

$$=2t^3-3t^2+6t-6\ln|t+1|+c$$

$$=2\sqrt{x}-3\sqrt[3]{x}+6\sqrt[6]{x}-6\ln(\sqrt[6]{x}+1)+c$$

(二)三角代换  
Case1.$$\sqrt{a^2-x^2},设x=asint,\Rightarrow acost$$

例1🌰.$$\int\sqrt{a^2-x^2}dx(a>0)$$

$$解：令x=asint$$

$$原式=\int a^2 cos^2t dt=\frac{a^2}{2}\int(1+cos2t)dt$$

$$=\frac{a^2}{2}(t+\frac{1}{2}sin2t)+c$$

$$=\frac{a^2}{2}t+\frac{a^2}{2}sintcost+c$$

$$=\frac{a^2}{2}arcsin\frac{x}{a}+\frac{a^2}{2}*\frac{x}{a}*\frac{\sqrt{a^2-x^2}}{a}$$

$$\therefore \int\sqrt{a^2-x^2}dx=\frac{a^2}{2}arcsin\frac{x}{a}+\frac{x}{2}\sqrt{a^2-x^2}+c$$

例2🌰.$$\int\frac{1}{x^2\sqrt{1-x^2}}dx$$

$$解：令x=sint$$

$$原式=\int\frac{cost}{sin^2x·cost}dt=\int csc^2tdt$$

$$=-cott+c$$

$$=-\frac{\sqrt{1-x^2}}{x}+c$$

Case2.$$\sqrt{x^2+a^2},设x=atant,\Rightarrow asect$$

例3🌰.$$\int\frac{dx}{\sqrt{(x^2+1)^3}}$$

$$解：令x=tant$$

$$原式=\int\frac{sec^2t}{sec^3t}dt=\int\frac{1}{sect}dt=\int costdt$$

$$=sint+c$$

$$=\frac{x}{\sqrt{x^2+1}}+c$$

例4🌰.$$\int\frac{1}{\sqrt{x^2+a^2}}dx(a>0)$$

$$解：令x=atant$$

$$原式=\int\frac{asec^2t}{asect}dt=\int sectdt$$

$$=\ln|sect+tant|+c$$

$$=\ln|\frac{x}{a}+\frac{\sqrt{x^2+a^2}}{a}|+c$$

$$=\ln(x+\sqrt{x^2+a^2})+c$$

$$\therefore\int\frac{1}{\sqrt{x^2+a^2}}dx=\ln(x+\sqrt{x^2+a^2})+c$$

Case3.$$\sqrt{x^2-a^2},设x=asect,\Rightarrow atant$$

例5🌰.$$\int\frac{1}{\sqrt{x^2-a^2}}dx$$

$$解：x=asect$$

$$原式=\frac{asecttantdt}{atant}\int sectdt$$

$$=\ln|sect+tant|+c$$

$$=\ln|\frac{x}{a}+\frac{\sqrt{x^2-a^2}}{a}|+C$$

$$=\ln|x+\sqrt{x^2-a^2}|+c$$

例6🌰.$$\int\frac{dx}{x^2+x+1}$$

$$解：原式=\int\frac{d(x+\frac{1}{2})}{(\frac{\sqrt{3}}{2})^2+(x+\frac{1}{2})^2}$$

$$=\frac{2}{\sqrt{3}}arctan\frac{x+\frac{1}{2}}{\frac{\sqrt{3}}{2}}+c$$

例7🌰.$$\int\frac{1}{\sqrt{4x^2+a}}dx$$

$$解：原式=\frac{1}{2}\int\frac{1}{(2x)^2+(3)^2}d(2x)$$

$$=\frac{1}{2}\ln(2x+\sqrt{4x^2+9})+c$$

#### 分部积分法

$$(uv)'=u'v+uv'$$

$$\Rightarrow\int(uv)'dx=\int u'vdx+\int uv'dx$$

$$\Rightarrow uv=\int vdu+\int udv$$

$$\therefore\int udv=uv-\int vdu$$

Case1.$$\int x^a·e^xdx$$

例1🌰.$$\int x^2e^xdx$$

$$解：原式=\int x^2d(e^x)=x^2e^x-\int e^xd(x^2)$$

$$=x^2e^x-2\int xe^xdx=x^2e^x-2\int xd(e^x)$$

$$=x^2e^x-2(xe^x-\int e^xdx)$$

$$=x^2e^x-2xe^x+2e^x+c$$

Case2.$$\int x^n·\ln x dx$$

例2🌰.$$\int x^2·\ln x dx$$

$$解：原式=\int\ln xd(\frac{1}{3}x^3)$$

$$=\frac{1}{3}x^3\ln x-\frac{1}{3}\int x^3d(\ln x)$$

$$=\frac{1}{3}x^3\ln x-\frac{1}{3}\int x^2dx$$

$$=\frac{1}{3}x^3\ln x-\frac{1}{9}x^3+c$$

Case3.$$\int x^a·三角函数 dx$$

例3🌰.$$\int x^2 cos2xdx$$

$$解：原式=\int x^2d(\frac{1}{2}sin2x)$$

$$=\frac{1}{2}x^2sin2x-\frac{1}{2}\int sin2xd(x^2)$$

$$=\frac{1}{2}x^2sin2x-\int xsin2xdx$$

$$=\frac{1}{2}x^2sin2x+\int xd(\frac{1}{2}cos2x)$$

$$=\frac{1}{2}x^2sin2x+\frac{1}{2}xcos2x-\frac{1}{2}\int cos2x dx$$

$$=\frac{1}{2}x^2sin2x+\frac{1}{2}xcos2x-\frac{1}{4}sin2x+c$$

Case4.$$\int x^a·反三角函数 dx$$

例4🌰.$$\int xarctanxdx$$

$$解：原式=\int arctanxd(\frac{1}{2}x^2)$$

$$=\frac{1}{2}x^2arctanx-\frac{1}{2}\int x^2d(arctanx)$$

$$=\frac{1}{2}x^2arctanx-$$

例5🌰.$$\int arcsinx dx$$

$$解：原式=xarcsinx-\int xd(arcsinx)$$

$$=xarcsinx-\int\frac{x}{\sqrt{1-x^2}}dx$$

$$=xarcsinx+\int\frac{1}{2\sqrt{1-x^2}}d(1-x^2)$$

$$=xarcsinx+\sqrt{1-x^2}+c$$

Case5.$$\int e^{ax}·\begin{cases}
cosbx \\
sinbx
\end{cases}dx$$

例6🌰.$$\int e^xcos3xdx$$

$$设I=\int e^xcos3xdx$$

$$解：原式=\int cos3xd(e^x)$$

$$=e^xcos3x-\int e^xd(cos3x)$$

$$=e^xcos3x+3\int e^xsin3xdx$$

$$=e^xcos3x+3\int sin3xd(e^x)$$

$$=e^xcos3x+3(e^xsin3x-\int e^xd(sin3x))$$

$$=e^xcos3x+3e^xsin3x-9\int e^xcos3xdx$$

$$=e^xcos3x+3e^xsin3x-9I$$

$$I=\frac{1}{10}e^x(cos3x+3sin3x)+c$$

Case6.$$\int\begin{cases}
sec^nx \\
csc^nx
\end{cases}dx(n为奇数)$$
注：偶次不定积分分部积分

$$\int sec^2xdx=tanx+c$$

$$\int sec^4xdx=\int(tanx^2+1)d(tanx)$$

$$=\frac{1}{3}tan^3x+tanx+c$$

$$I_1=\int secxdx=\ln|secx+tanx|+c$$

例7🌰.$$I_3=\int sec^3xdx$$

$$解：原式=\int sexd(tanx)$$

$$=secxtanx-\int tanxd(secx)$$

$$=secxtanx-\int tan^2x·secxdx$$

$$=secxtanx-\int(sec^2x-1)secxdx$$

$$=secxtanx-I_3+\ln|secx+tanx|$$

$$\therefore I_3=\int sec^3xdx=\frac{1}{2}(secxtanx+\ln|secx+tanx|)+c$$


