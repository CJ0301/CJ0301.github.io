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
f(x)\in[a,b] \\
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