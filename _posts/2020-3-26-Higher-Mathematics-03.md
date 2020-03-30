---
layout: 		post
title: 			"高等数学_3"
subtitle: 		'微分中值定理'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---

## 微分中值定理
预备知识：  
1.极值点：

$$If\exists\delta>0,当0<|x-a|<\delta时，f(x)<f(a)，则x=a为极大点，f(a)为极大值$$

$$If\exists\delta>0,当0<|x-a|<\delta时，f(x)>f(a)，则x=a为极小点，f(a)为极小值$$

2.$$f'(a)\begin{cases}
&> 0 \\
&< 0 \\
&= 0 \\
&不存在
\end{cases}$$

$$If f'(x)>0\Rightarrow\lim\limits_{x\rightarrow a}\frac{f(x)-f(a)}{x-a}>0$$

$$\exists\delta>0,当0<|x-a|<\delta时$$

$$由极限保号性得,\frac{f(x)-f(a)}{x-a}>0$$

$$\begin{cases}
f(x)<f(a) & x\in(a-\delta,a) \\
f(x)>f(a) & x\in(a,a+\delta)
\end{cases}$$

$$\Rightarrow左小右大，\therefore a非极值点$$

$$If f'(x)<0\Rightarrow\lim\limits_{x\rightarrow a}\frac{f(x)-f(a)}{x-a}<0$$

$$\exists\delta>0,当0<|x-a|<\delta时$$

$$由极限保号性得,\frac{f(x)-f(a)}{x-a}<0$$

$$\begin{cases}
f(x)>f(a) & x\in(a-\delta,a) \\
f(x)<f(a) & x\in(a,a+\delta)
\end{cases}$$

$$\Rightarrow左大右小，\therefore a非极值点$$

Notes:  
1.$$f(x)在x=a取极值\Rightarrow f'(a)=0或f'(a)不存在$$  
2.$$f(x)可导且在x=a取极值\Rightarrow f'(a)=0$$

但是反过来就不正确  
反例1：$$y=x^3,y'=3x^2,y'(0)=0$$  
$$x=0不是极值点$$

一、罗尔定理  
Th1.若满足$$\begin{cases}
f(x)\in c[a,b] \\
f(x)在(a,b)内可导 \\
f(a)=f(b)
\end{cases} 则\exists\xi\in(a,b),使得f'(\xi)=0(至少一个)$$

$$证：f(x)\in c[a,b]\Rightarrow f(x)在[a,b]上一定取到最小值m和最大值M$$

Case1.$$m=M$$

$$则f(x)\equiv c_0$$

$$\forall\xi\in(a,b),f'(\xi)=0$$


Case2.$$m<M$$

$$\because f(a)=f(b),m<M$$


$$\therefore m,M至少一个在(a,b)内取到$$

$$设\exists\xi\in(a,b),使f(\xi)=M$$

$$\Rightarrow f'(\xi)=0或不存在$$

$$\because f(x)在(a,b)内可导\therefore f'(\xi)=0$$

例1🌰.$$f(x)\in c[a,b],(a,b)内可导,f(a)f(b)>0,f(a)f(\frac{1+b}{2})<0,证明:\exists\xi\in(a,b),使得f'(\xi)=0$$

$$f(a)f(\frac{a+b}{2})<0\Rightarrow\exists x_1\in(a,\frac{a+b}{2}),f(x_1)=0$$

$$f(a)f(b)>0\Rightarrow f(\frac{a+b}{2})f(b)<0$$

$$\Rightarrow\exists x_2\in(\frac{a+b}{2},b),f(x_2)=0$$

$$\because f(x_1)=f(x_2)$$

$$\therefore \exists\xi\in(x_1,x_2)\subset(a,b),使f'(\xi)=0$$

二、拉格朗日中值定理  
Th2.若满足$$\begin{cases}
f(x)\in c[a,b] \\
f(x)在(a,b)内可导
\end{cases}则\exists\xi\in(a,b),使f'(\xi)=\frac{f(b)-f(a)}{b-a}$$

$$证明：曲线L：y=f(x),直线L_{AB}:y=f(a)+\frac{f(b)-f(a)}{b-a}(x-a)$$

$$令\phi(x)=曲-直=f(x)-f(a)-\frac{f(b)-f(a)}{b-a}(x-a)$$

$$\phi(x)\in c[a,b],\phi(x)在(a,b)内可导$$

$$\because\phi(a)=\phi(b)=0$$

$$\therefore根据罗尔中值定理,\exists\xi\in(a,b),使\phi'(\xi)=0$$

$$而\phi'(\xi)=f'(x)-\frac{f(b)-f(a)}{b-a}$$

$$\therefore f'(\xi)=\frac{f(b)-f(a)}{b-a}$$

Notes:  
1.$$If f(a)=f(b),拉格朗日定理即为罗尔定理$$
2.等价形式:$$f'(\xi)=\frac{f(b)-f(a)}{b-a}$$

$$\Leftrightarrow f(b)-f(a)=f'(\xi)(b-a)$$

$$\Leftrightarrow f(b)-f(a)=f'(a+\theta(b-a))(b-a)(0<\theta<1)$$

例1🌰.$$验证f(x)=x^3-x^2-x在[0,2]上满足拉格朗日中值定理的条件,求\xi$$

$$\because f(x)\in c[0,2],在(0,2)内可导$$

$$\therefore在[0,2]上满足拉格朗日中值定理的条件$$

$$由f'(\xi)=\frac{f(2)-f(0)}{2-0}$$

$$\Rightarrow 3\xi^2-2\xi-1=1$$

$$\Rightarrow 3\xi^2-2\xi-2=0$$

$$\xi=\frac{2\pm\sqrt{4+24}}{6}=\frac{1\pm\sqrt{7}}{3}$$

$$\xi_1=\frac{1+\sqrt{7}}{3}\in(0,2),\xi_2=\frac{1-\sqrt{7}}{3}舍$$

推论:$$f(x)\in c[a,b],(a,b)内f'(x)\equiv0,则f(x)\equiv c_0(a\leqslant x \leqslant b)$$

$$证：\forall x_1,x_2\in[a,b],x_1\neq x_2$$

$$f(x_2)-f(x_1)=f'(\xi)(x_2-x_1)=0$$

$$\Rightarrow f(x_1)=f(x_2)$$

$$\therefore f(x)\equiv c_0(a\leqslant x \leqslant b)$$

三、柯西中值定理
Th3.若满足$$\begin{cases}
f(x)、g(x)\in c[a,b] \\
f(x)、g(x)在(a,b)内可导 \\
g'(x)\neq0(a<x<b)
\end{cases}则\exists\xi\in(a,b),使得\frac{f(b)-f(a)}{g(b)-g(a)}=\frac{f'(\xi)}{g'(\xi)}$$

1.$$g'(x)\neq0(a<x<b)\Rightarrow\begin{cases}
g'(\xi)\neq0 \\
g(b)-g(a)\neq0
\end{cases}$$

$$为什么g(b)-g(a)\neq0?$$

$$Ifg(b)-g(a)=0\Rightarrow g(a)=g(b)$$

$$根据罗尔中值定理\exists\eta\in(a,b),g'(\eta)=0,矛盾\therefore g(b)-g(a)\neq0$$

2.$$If g(x)=x,柯西中值定理即为拉格朗日中值定理$$

3.$$拉：\phi(x)=曲-直=f(x)-f(a)-\frac{f(b)-f(a)}{b-a}(x-a)$$
$$柯:\phi(x)=f(x)-f(a)-\frac{f(b)-f(a)}{g(b)-g(a)}[g(x)-g(a)]$$

$$证：令\phi(x)=f(x)-f(a)-\frac{f(b)-f(a)}{g(b)-g(a)}[g(x)-g(a)]$$

$$\phi(x)\in c[a,b],(a,b)内可导$$

$$\phi(a)=0,\phi(b)=0$$

$$\because\phi(a)=\phi(b)=0$$

$$\therefore\exists\xi\in(a,b),使\phi'(\xi)=0$$

$$而\phi'(x)=f'(x)-\frac{f(b)-f(a)}{g(b)-g(a)}g'(x)$$

$$\therefore f'(\xi)=\frac{f(b)-f(a)}{g(b)-g(a)}g'(\xi)$$

$$\therefore \frac{f'(\xi)}{g'(\xi)}=\frac{f(b)-f(a)}{g(b)-g(a)}$$

典型例题：  
例1🌰.$$f(x)\in c[0,2],(0,2)内可导,f(0)+2f(1)=3,f(2)=1,证明:\exists\xi\in(0,2),使f'(\xi)=0$$

$$证：1.f(x)\in c[0,1],则f(x)在[0,1]上有m,M$$

$$3m\leqslant f(0)+2f(1)\leqslant 3M$$

$$\Rightarrow m \leqslant 1 \leqslant M$$

$$\exists c\in[0,1],使f(c)=1$$

$$2.\because f(c)=f(2)=1$$

$$\therefore\exists\xi\in (c,2)\subset(0,2),使f'(\xi)=0$$

例2🌰.$$\lim\limits_{x\rightarrow\infty}f'(x)=e,求\lim\limits_{x\rightarrow\infty}[f(x+2)-f(x)]$$

$$解：f(x+2)-f(x)=f'(\xi)·2(x<\xi<x+2)$$

$$\therefore\lim\limits_{x\rightarrow\infty}[f(x+2)-f(x)]=2\lim\limits_{x\rightarrow\infty}f'(\xi)=2e$$

例3🌰.$$0<a<b,证：\frac{b-a}{b}<\ln\frac{b}{a}<\frac{b-a}{a}$$

$$令f(x)=\ln x$$

$$f(x)\in c[a,b],(a,b)内可导,f'(x)=\frac{1}{x}$$

$$\ln\frac{b}{a}=f(b)-f(a)=f'(\xi)(b-a)(a<\xi<b)$$

$$=frac{b-a}{\xi}$$

$$\because a<\xi<b,\therefore\frac{b-a}{b}<\frac{b-1}{\xi}<\frac{b-a}{a}$$

$$\therefore\frac{b-a}{b}<\ln\frac{b}{a}<\frac{b-a}{a}$$

例4🌰.$$f(x)\in c[a,b],在[a,b]上有 \vert f'(x)\vert \leqslant M$$

$$a<c<b,f(c)=0,证：|f(a)|+|f(b)|\leqslant M(b-a)$$

$$f(c)-f(a)=f'(\xi_1)(c-a)(a<\xi_1<c)$$

$$f(b)-f(c)=f'(\xi_2)(b-c)(c<\xi_2<b)$$

$$\because f(c)=0,\therefore \begin{cases}
|f(a)| = |f'(\xi_1)|(c-a) \leqslant M(c-a) \\
|f(b)| = |f'(\xi_2)|(b-c) \leqslant M(b-c)
\end{cases}$$

$$\Rightarrow |f(a)| + |f(b)| \leqslant M(b-a)$$

$$罗尔-\begin{cases}
f^{(n)}(\xi)=0  \\
f(a)=f(b) 
\end{cases}$$

$$拉格朗日-\begin{cases}
f(b)-f(a)或\frac{f(b)-f(a)}{b-a} & 拉格朗日 \\
f(a)f(b)f(c) & 两次拉格朗日
\end{cases}$$

例5🌰.$$f(x)二阶可导,\lim\limits_{x\rightarrow0}\frac{f(x)-1}{x}=0,f(1)=1,证明\exists\xi\in(0,1),使f''(\xi)=0$$

$$\lim\limits_{x\rightarrow0}\frac{f(x)-1}{x}=0\Rightarrow f(0)=1(根据极限),f'(0)=0(根据导数定义)$$

$$\because f(0)=f(1)=1$$

$$\therefore\exists c\in(0,1),使f'(c)=0$$

$$又\because f'(0)=f'(c)=0$$

$$\therefore\exists\xi\in(0,c)\subset(0,1),使得f''(\xi)=0$$

例6🌰.$$f(x)\in c[0,1],(0,1)内可导且f(1)=0,证：\exists\xi\in(0,1),使\xi f'(\xi)+2f(\xi)=0$$

$$证：\exists\xi$$