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
#### 预备知识 
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

#### 三个中值定理
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

例1🌰.$$f(x)\in c[a,b],(a,b)内可导,f(a)f(b)>0,f(a)f(\frac{a+b}{2})<0,证明:\exists\xi\in(a,b),使得f'(\xi)=0$$

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
$$证明：\exists\xi\in(0,1),使\xi f'(\xi)+2f(\xi)=0$$

$$分析：[\ln(f(x))]'=\frac{f'(x)}{f(x)}$$

$$xf'(x)+2f(x)=0\Rightarrow\frac{f'(x)}{f(x)}+\frac{x}{2}=0$$

$$[\ln f(x)]'+(lnx^2)'=0$$

$$[\ln x^2f(x)]'=0$$

$$证:令\phi(x)=x^2f(x)$$

$$\phi(x)\in c[0,1],在(0,1)内可导$$

$$\because f(1)=0,\therefore\phi(0)=\phi(1)=0$$

$$\therefore\exists\xi\in(0,1),使\phi'(\xi)=0$$

$$而\phi'(x)=2xf(x)+x^2f'(x)$$

$$\therefore 2\xi f(\xi)+\xi^2f'(\xi)=0$$

$$\because\xi\neq0,\therefore2f(\xi)+\xi f'(\xi)=0$$

#### 洛必达法则
背景：$$\frac{0}{0}型(\frac{\infty}{\infty}型),等价无穷小解决的问题有限。$$

$$如:\lim\limits_{x\rightarrow0}\frac{(1+x)^{sinx}-1}{x^2}$$

$$=\lim\limits_{x\rightarrow0}\frac{e^{sinx·\ln(1+x)}}{x^2}=\lim\limits_{x\rightarrow0}\frac{sinx·\ln(1+x)}{x^2}$$

$$\lim\limits_{x\rightarrow0}\frac{x^2}{x^2}=1$$

$$又如:\lim\limits_{x\rightarrow0}\frac{x-sinx}{x^3}$$

$$\neq\lim\limits_{x\rightarrow0}\frac{x-x}{x^3}$$

(加减法不一定能用等价无穷小，精度不够)

Th1.$$(\frac{0}{0}型)设:$$  
1.$$f(x)·g(x)在x=a的去心领域内可导且g'(x)\neq0$$。  
2.$$\lim\limits_{x\rightarrow a}f(x)=0,\lim\limits_{x\rightarrow a}g(x)=0$$。
3.$$\lim\limits_{x\rightarrow a}\frac{f'(x)}{g'(x)}=A(或\infty)$$

$$则\lim\limits_{x\rightarrow a}\frac{f(x)}{g(x)}=A，即\lim\limits_{x\rightarrow a}\frac{f(x)}{g(x)}=\lim\limits_{x\rightarrow a}\frac{f'(x)}{g'(x)}$$  

Note:f(a)的值与其极限无关

$$证:令f(a)=0,g(a)=0(保证连续性),则f(x),g(x)在x=a邻域内连续，去心邻域内可导$$

$$\frac{f(x)}{g(x)}=\frac{f(x)-f(a)}{g(x)-g(a)}(x为a的去心邻域内的点，以a、x为端点用柯西中值定理)$$

$$=\frac{f'(\xi)}{g'(\xi)}(\xi介于a与x之间)$$

$$\therefore\lim\limits_{x\rightarrow a}\frac{f(x)}{g(x)}=\lim\limits_{x\rightarrow a}\frac{f'(\xi)}{g'(\xi)}=\lim\limits_{\xi\rightarrow a}\frac{f'(\xi)}{g'(\xi)}=A$$

例1🌰.$$\lim\limits_{x\rightarrow0}\frac{x-sinx}{x^3}$$

$$解：\lim\limits_{x\rightarrow0}\frac{x-sinx}{x^3}=\lim\limits_{x\rightarrow0}\frac{1-cosx}{3x^2}=\frac{1}{6}$$

例2🌰.$$\lim\limits_{x\rightarrow0}\frac{x-\ln(1+x)}{x^2}$$

$$解:原式=\lim\limits_{x\rightarrow0}\frac{1-\frac{1}{1+x}}{2x}=\lim\limits_{x\rightarrow0}\frac{\frac{x}{1+x}}{2x}=\frac{1}{2}$$

Th2.$$(\frac{\infty}{\infty}型)$$    
1.$$f(x)\rightarrow\infty,g(x)\rightarrow\infty(x\rightarrow a)$$  
2.f(x)、g(x)在x=a去心邻域内可导  
3.$$\lim\limits_{x\rightarrow a}\frac{f'(x)}{g'(x)}=A(或\infty)$$ 

$$\lim\limits_{x\rightarrow a}\frac{f(x)}{g(x)}=\lim\limits_{x\rightarrow a}\frac{f'(x)}{g'(x)}$$

例1🌰.$$\lim\limits_{x\rightarrow +\infty}x(\frac{\pi}{2}-arctanx)(\infty·0型)$$

$$解:原式=\lim\limits_{x\rightarrow +\infty}\frac{\frac{\pi}{2}-arctanx}{\frac{1}{x}}(\frac{0}{0}型)$$

$$=\lim\limits_{x\rightarrow +\infty}\frac{-\frac{1}{1+x^2}}{-\frac{1}{x^2}}=\frac{x^2}{1+x^2}$$

例2🌰.$$\lim\limits_{x\rightarrow +\infty}\frac{\ln x}{x^a}(a>0)(\frac{\infty}{\infty}型)$$

$$解：原式=\lim\limits_{x\rightarrow +\infty}\frac{\frac{1}{x}}{ax^{a-1}}=\frac{1}{a}\lim\limits_{x\rightarrow +\infty}\frac{1}{x^a}=0$$

例3🌰.$$\lim\limits_{x\rightarrow +\infty}\frac{x^3}{e^x}(\frac{\infty}{\infty}型)$$

$$解:原式=\lim\limits_{x\rightarrow +\infty}\frac{3x^2}{e^x}=\lim\limits_{x\rightarrow +\infty}\frac{6x}{e^x}$$

$$=\lim\limits_{x\rightarrow +\infty}\frac{6}{e^x}=0$$

例4🌰.$$\lim\limits_{x\rightarrow 0^+}x^x$$

$$解:原式=e^{\lim\limits_{x\rightarrow 0^+}x\ln x}$$

$$\because\lim\limits_{x\rightarrow 0^+}x\ln x(0·\infty型)=\lim\limits_{x\rightarrow 0^+}\frac{\ln x}{\frac{1}{x}}$$

$$=\lim\limits_{x\rightarrow 0^+}\frac{\frac{1}{x}}{-\frac{1}{x^2}}=\lim\limits_{x\rightarrow 0^+}(-x)=0$$

$$\therefore原式=e^0=1$$

Notes:  
1.$$洛必达法则适用于\frac{0}{0}、\frac{\infty}{\infty}，且条件满足时可重复使用。$$   
2.$$\frac{\ln x}{x^a}\rightarrow0(a>0,x\rightarrow+\infty)$$  
$$  \frac{x^a}{e^x}\rightarrow0(a>0,x\rightarrow+\infty)$$  
3.$$\lim\frac{f'(x)}{g'(x)}\exists是\lim\frac{f}{g}\exists的充分不必要条件,即洛必达法则不一定成功$$

$$如：\lim\limits_{x\rightarrow\infty}\frac{3x+sinx}{x}(\frac{\infty}{\infty})$$

$$\lim\limits_{x\rightarrow\infty}\frac{(3x+sinx)'}{(x)'}=\lim\limits_{x\rightarrow\infty}(3+cosx)不存在$$

$$而\lim\limits_{x\rightarrow\infty}\frac{3x+sinx}{x}=\lim\limits_{x\rightarrow\infty}(3+\frac{sinx}{x})=3$$

#### 泰勒公式
背景：$$\frac{0}{0}型求极限精度不够,如\lim\limits_{x\rightarrow0}\frac{x-tanx}{x^3}$$  
$$tanx=x+?x^3+o(x^3)$$  
$$设f(x)在x=x_0邻域内n+1阶可导$$  
$$f(x)=P_n(x)+R_n(x)(P_n(x)主，R_n(x)次)，f(n)\approx P_n(x)$$  

Th1.$$(泰勒公式) f(x)在x=x_0邻域内n+1阶可导，则$$

$$f(x)=P_n(x)+R_n(x)(P_n(x)主，R_n(x)次)$$

$$其中P_n(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+...+\frac{f^{(n)}}{n!}(x-x_0)^n$$

$$R_n(x)=\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1},\xi介于x_0与x之间。$$

$$证明：P_n(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+...+\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n$$

$$P_n(x_0)=f(x_0)$$

$$P_n'(x)=f'(x_0)+f''(x_0)(x-x_0)+...+\frac{f^{(n)}(x_0)}{(n-1)!}(x-x_0)^{n-1}$$

$$p_n'(x_0)=f'(x_0)$$

$$P_n''(x)=f''(x_0)+f'''(x_0)(x-x_0)+...+\frac{f^{(n)}(x_0)}{(n-2)!}(x-x_0)^{n-2}$$

$$P_n''(x_0)=f''(x_0)$$

$$...$$

$$P_n^{(n)}(x_0)=f^{(n)}(x_0)$$

$$令R_n(x)=f(x)-P_n(x)$$

$$R_n(x_0)=0,R_n'(x_0)=0,...,R_n^{(n)}(x_0)=0$$

$$R_n^{(n+1)}(x)=f^{(n+1)}(x)$$

$$\frac{R_n(x)}{(x-x_0)^{n+1}}=\frac{R_n(n)-R_n(x_0)}{(x-x_0)^{n+1}-(x_0-x_0)^{n+1}}$$

$$根据柯西中值定理得，=\frac{R_n'(x_1)}{(n+1)(x_1-x_0)^n}(x_1介于x_0与x之间)$$

$$=\frac{R_n'(x_1)-R_n'(x_0)}{(n+1)(x_1-x_0)^n-(n+1)(x_0-x_0)^n}=\frac{R_n''(x_2)}{(n+1)n(x_2-x_0)^{n-1}}(x_2介于x_0与x_1之间)$$

$$=...=\frac{R_n^{(n-1)}(x_{n-1})}{(n+1)...2(x_{n-1}-x_0)}(x_{n-1}介于x_0与x_{n-2}之间)$$

$$=\frac{R_n^{(n-1)}(x_{n-1})-R_n^{(n-1)}(x_0)}{(n+1)!(x_{n-1}-x_0)-(n+1)!(x_0-x_0)}$$

$$=\frac{R_n^{(n+1)}(\xi)}{(n+1)!}=\frac{f^{(n+1)}(\xi)}{(n+1)!}(\xi介于x_0与x_{n-1}之间)$$

$$\therefore\frac{R_n(x)}{(x-x_0)^{n+1}}=\frac{f^{(n+1)}(\xi)}{(n+1)!}$$

$$\therefore R_n(x)=\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}(\xi介于x与x_0之间)$$

$$即f(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+...$$

$$+\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n+\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}$$

$$特别的,当x_0=0$$

$$f(x)=f(0)+f'(0)x+\frac{f''(0)}{2!}x^2+...+\frac{f^{(n)}(0)}{n!}x^n+\frac{f^{(n+1)}(\xi)}{(n+1)!}x^{n+1}(\xi介于0与x之间) 麦克劳林公式$$

$$R_n(x)=\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1} 拉格朗日型余项$$

Th2.$$f(x)在x=x_0邻域内n阶可导,则f(x)=P_n(x)+o((x-x_0)^n) 皮亚诺型余项$$

$$证明：P_n(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+...+\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n$$

$$P_n(x_0)=f(x_0)$$

$$P_n'(x_0)=f'(x_0)$$

$$...$$

$$P_n^{(n)}(x_0)=f^{n}(x_0)$$

$$R_n(x)=f(x)-P_n(x)$$

$$R_n(x_0)=R_n'(x_0)=...=R_n^{(n)}(x_0)$$

$$\lim\limits_{x\rightarrow x_0}\frac{R_n(x)}{(x-x_0)^n}=\lim\limits_{x\rightarrow x_0}\frac{R_n'(x)}{n(x-x_0)^{n-1}}$$

$$=...=\lim\limits_{x\rightarrow x_0}\frac{R_n^{(n-1)}(x)}{n!(x-x_0)}$$

$$=\lim\limits_{x\rightarrow x_0}\frac{R_n^{(n-1)}(x)-R_n^{(n-1)}(x_0)}{n!(x-x_0)-n!(x_0-x_0)}$$

$$利用柯西中值定理，得=\frac{1}{n!}R_n^{(n)}(x_0)=0$$

$$\therefore R_n(x)=o((x-x_0)^n)$$

$$\therefore f(x)=f(x_0)+f'(x_0)(x-x_0)+...+\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n+o((x-x_0)^n)$$

例1🌰.$$求f(x)=e^x的n阶麦克劳林公式。$$

$$解：f(x)=e^x,f'(x)=e^x,...,f^{(n)}(x)=e^x$$

$$f(0)=1,f'(0)=1,...,f^{(n)}(0)=1$$

$$e^x=f(0)+f'(0)x+...+\frac{f^{(n)}(0)}{n!}x^n+o(x^n)$$

$$\therefore e^x=1+x+\frac{x^2}{2!}+...+\frac{x^n}{n!}+o(x^n)$$

例2🌰.$$f(x)=sinx$$

$$解：f(x)=sinx,f'(x)=cosx,f''(x)=-sinx,f'''(x)=-cosx,...$$

$$f(0)=0,f'(0)=1,f''(0)=0,f'''(0)=-1,...$$

$$sinx=f(0)+f'(0)x+...+\frac{f^{(n)}(0)}{n!}x^n+o(x^n)$$

$$\therefore sinx=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\frac{x^7}{7!}$$

同上，可推得：

$$cosx=1-\frac{x^2}{2!}+\frac{x^4}{4!}-...+\frac{(-1)^n}{(2n)!}x^{2n}+o(x^{2n})$$

$$\frac{1}{1-x}=1+x+x^2+...+x^n+o(x^n)$$

$$\frac{1}{1+x}=1-x+x^2-...+(-1)^nx^n+o(x^n)$$

$$\ln(1+x)=x-\frac{x}{2}+\frac{x^3}{3}-...+\frac{(-1)^{n-1}x^n}{n}+o(x^n)$$

$$(1+x)^a=1+ax+\frac{a(a-1)}{2!}x^2+\frac{a(a-1)(a-2)}{3!}x^3+...+\frac{a(a-1)..(a-n+1)}{n!}x^n+o(x^n)$$

实际使用：  

$$x-sinx=\frac{1}{6}x^3+o(x^3) \\

\Rightarrow x-sinx\approx\frac{1}{6}x^3 \\

\Rightarrow x-sinx\sim\frac{1}{6}x^3(x\rightarrow0) \\

x^3-sinx^3=\frac{1}{6}(x^3)^3+o(x^3) \\

\Rightarrow x^3-sinx^3\approx\frac{1}{6}(x^3)^3 \\

\Rightarrow x^3-sinx^3\sim\frac{1}{6}x^9(x\rightarrow0)$$

例题：

例1🌰.$$\lim\limits_{x\rightarrow0}\frac{x-sinx}{x^3}$$

$$解：\because sinx=x-\frac{x^3}{3!}+o(x^3)$$

$$\therefore x-sinx=\frac{x^3}{6}+o(x^3) \sim \frac{x^3}{6}$$

$$\therefore原式=\frac{1}{6}$$

例2🌰.$$\lim\limits_{x\rightarrow0}\frac{x-\ln(1+x)}{x^2}$$

$$解：\ln(1+x)=x-\frac{x^2}{2}+0(x^2)$$

$$x-\ln(1+x)=\frac{x^2}{2}+o(x^2) \sim\frac{x^2}{2}$$

$$\therefore原式=\frac{1}{2}$$

例3🌰.$$\lim\limits_{x\rightarrow0}\frac{e^{-\frac{x^2}{2}}-1+\frac{x^2}{2}}{x^3sinx}$$

$$解：原式=\lim\limits_{x\rightarrow0}\frac{e^{-\frac{x^2}{2}}-1+\frac{x^2}{2}}{x^4}$$

$$\because e^x=1+x+\frac{x^2}{2!}+o(x^2)$$

$$\therefore e^{-\frac{x^2}{2}}=1-\frac{x^2}{2}+\frac{x^4}{8}+o(x^4)$$

$$\therefore e^{-\frac{x^2}{2}}-1+\frac{x^2}{2}=\frac{x^4}{8}+o(x^4) \sim \frac{x^4}{8}$$

$$\therefore原式=\frac{1}{8}$$

例4🌰.$$\lim\limits_{x\rightarrow0}\frac{sinx-xcosx}{sin^3x}$$

$$解：原式=\lim\limits_{x\rightarrow0}\frac{sinx-xcosx}{x^3}$$

$$\because sinx=x-\frac{x^3}{3!}+o(x^3)$$

$$cosx=1-\frac{x^2}{2!}+o(x^2)$$

$$\therefore xcosx=x-\frac{x^3}{2}+o(x^3)$$

$$\therefore sinx-xcosx=\frac{x^3}{3}+o(x^3)\sim\frac{x^3}{3}$$

$$原式=\frac{1}{3}$$

例5🌰.$$\lim\limits_{x\rightarrow0}\frac{[sin-sin(sinx)]xinx}{x^4}$$

$$sin x-sin(sinx)\sim\frac{1}{6}sin^3x \\

原式=\lim\limits_{x\rightarrow0}\frac{\frac{1}{6}sin^4}{x^4} \\

=\frac{1}{6}
$$

无穷小运算：  
1. 有限个无穷小和是无穷小。  
2. 有界函数与无穷小的乘积是无穷小。
3. 有限个无穷小成绩是无穷小。
4. 运算性质：
设m，n为正整数，则  
$$a.o(x^m)\pm o(x^n)=o(x^l),l=min\{m,n\}(加减法时低阶吸收高阶) \\
b.o(x^m)·o(x^n)=o(x^{m+n}),x^m·o(x^n)=o(x^{m+n})(乘法时阶数累加) \\
c.o(x^m)=o(kx^m)=k·o(x^m),k\neq0且为常数(非零常数相乘不影响阶数)$$

🌰：  
$$o(x^2)=o(x^3)=o(x^2) \\
o(x^3)+o(x^3)=o(x^3) \\
o(x^3)-o(x^3)=o(x^3)$$

用泰勒公式时需要展开到多少次幂：  
1）$$\frac{A}{B}型，适用于“上下同阶”原则。$$  
如果分母或分子是x的k次幂，则应把分子或分母展开到x的k次幂，可称为“上下同阶”原则。  
🌰：  
$$\lim\limits_{x\rightarrow0}\frac{x-sinx}{x^3}=\frac{1}{6}$$

2）A-B型，适用于幂次最低原则  
将A,B展开到系数不相等的x的最低次幂为止。  
🌰：  
$$
\lim\limits_{x\rightarrow0}cosx-e^{-\frac{x^2}{2}} \\
cosx=1-\frac{x^2}{2}+\frac{1}{24}x^4+o(x^4) \\
e^{-\frac{x^2}{2}}=1-\frac{x^2}{2}+\frac{1}{8}x^4+o(x^4) \\
\Rightarrow cosx-e^{-\frac{x^2}{2}}=-\frac{1}{12}x^4+o(x^4) \\
\Rightarrow cosx-e^{-\frac{x^2}{2}}\sim-\frac{1}{12}x^4
$$

更多🌰：   
1）$$x-sinx \\
x=1·x^1+0·x^3 \\
sinx=x^1-\frac{1}{6}x^3+o(x^3) \\
\Rightarrow x-sinx=\frac{1}{6}x^3+o(x^3)
\Rightarrow x-sinx\sim\frac{1}{6}x^3$$

2）$$x+sinx \Rightarrow x-(-sinx)\\
x=1·x^1 \\
-sinx=(-1)·x^1+o(x) \\
\Rightarrow x+sinx=x-(-sinx)=2x+o(x)
\Rightarrow x+sinx\sim 2x$$

3）$$\lim\limits_{x\rightarrow0}\frac{sin^2x-x^2}{e^4-1} \\
=\lim\limits_{x\rightarrow0}\frac{(sinx+x)(sinx-x)}{x^4} \\
=\lim\limits_{x\rightarrow0}\frac{-\frac{1}{3}x^4}{x^4} \\
=-\frac{1}{3}
$$

#### 海涅定理(归结定理)
$$\lim\limits_{x\rightarrow x_0}f(x)=A存在\Leftrightarrow \\
\lim\limits_{n\rightarrow\infty}f(x_n)=A存在(对于任何的数列x_n\rightarrow x_0)$$

1.$$"\Leftarrow"往往用于否定存在性$$
1.$$"\Rightarrow"考计算$$

🌰：  
1）$$
\lim\limits_{x\rightarrow0}\frac{1}{x}sin\frac{1}{x} \\
取x_n=\frac{1}{n\pi},n\rightarrow\infty,\lim\limits_{n\rightarrow\infty}f(x_n) \\
=\lim\limits_{n\rightarrow\infty}n\pi sinn\pi=0 \\
取x_n'=\frac{1}{(2n+\frac{1}{2})\pi},n\rightarrow\infty \\
\lim\limits_{n\rightarrow\infty}f(x_n')=(2n+\frac{1}{2})\pi·sin(2n\pi+\frac{1}{2}\pi)=\infty
$$

2）$$
\lim\limits_{n\rightarrow\infty}(ntan\frac{1}{n})^{n^2}(n为正整数) \\
(数列转函数)\lim\limits_{x\rightarrow0}(\frac{tanx}{x})^{\frac{1}{x^2}}=e^{\lim\limits_{x\rightarrow0}\frac{1}{x^2}\ln\frac{tanx}{x}} \\
\ln(1+g(x))\sim g(x),g(x)\rightarrow0 \\
\frac{tanx-x}{x}\sim\frac{1}{3}x^3 \\
=e^{\frac{1}{3}}
$$
#### 单调性与极值、最值

一、函数单调性及判别法      
(一)def- $$y=f(x)(x\in I)$$    
1.$$if\forall x_1,x_2\in I 且x_1<x_2，有f(x_1)<f(x_2)，称f(x)再I上为单调增函数$$  
2.$$if\forall x_1,x_2\in I 且x_1<x_2，有f(x_1)>f(x_2)，称f(x)再I上为单调减函数$$

(二)判别法  
Th1.$$f(x)\in c[a,b],(a,b)内可导$$  
1.$$Iff'(x)>0(a<x<b)\Rightarrow f(x)在[a,b]上严格递增$$  
2.$$Iff'(x)<0(a<x<b)\Rightarrow f(x)在[a,b]上严格递减$$

$$证：\forall x_1,x_2\in[a,b]且x_1<x_2$$

$$(拉格朗日)f(x_2)-f(x_1)=f'(\xi)(x_2-x_1)(x_1<\xi<x_2)$$

$$\because f'(x)>0(a<x<b)$$

$$\therefore f(x_2)-f(x_1)>0\Rightarrow f(x_1)<f(x_2)$$

$$\therefore f(x)在[a,b]上严格递增$$

Note:在(a,b)内除有少数几个点不可导或导数等于0以外，f'(x)>0(<0)
则f(x)在[a,b]上严格递增(递减)

例1🌰.$$f(x)-sinx在[-\pi,\pi]单调性$$

$$解：f'(x)=1-cosx$$

$$\because在(-\pi,\pi)内除f'(0)=0外f'(x)>0$$

$$\therefore f(x)在[-\pi,\pi]递增$$

例2🌰.$$f(x)=e^x-x-1$$

$$解：x\in(-\infty,+\infty)$$

$$f'(x)=e^x-1=0\Rightarrow x=0$$

$$当x\in(-\infty,0)时,f'(x)<0\Rightarrow f(x)在(-\infty,0]递减$$

$$当x\in(0,+\infty)时,f'(x)>0\Rightarrow f(x)在[0,+\infty)递增$$

例3🌰.$$f(x)=\sqrt[3]{x^2}$$

$$解：x\in(-\infty,+\infty)$$

$$f'(x)=\frac{2}{3}x^{-\frac{1}{3}}$$

$$在X=0时,f(x)不可导$$

$$当x\in(-\infty,0)时,f'(x)<0\Rightarrow f(x)在(-\infty,0]递减$$

$$当x\in(0,+\infty)时,f'(x)>0\Rightarrow f(x)在[0,+\infty)递增$$

二、极值  
(一)def- $$y=f(x)(x\in D),x_0\in D$$  
1.$$If\exists\delta>0,当0<|x-x_0|<\delta时,f(x)<f(x_0),x_0为极大点,f(x_0)为极大值$$    
2.$$If\exists\delta>0,当0<|x-x_0|<\delta时,f(x)>f(x_0),x_0为极小点,f(x_0)为极小值$$

(二)求解步骤  
y=f(x)  
1.$$x\in D$$  
2.f'(x)$$\begin{cases}
=0 (驻点)\\
不存在
\end{cases}(不一定为极值点)$$

(三)判别法    
Th1.(第一充分条件)  
1.$$\begin{cases}
x<x_0 & f'(x)<0 \\
x>x_0 & f'(x)>0
\end{cases}\Rightarrow x_0为极小值$$  
2.$$\begin{cases}
x<x_0 & f'(x)>0 \\
x>x_0 & f'(x)<0
\end{cases}\Rightarrow x_0为极大值$$

Th2.(第二充分条件)f'(x_0)=0  
1.$$If f''(x_0)>0,x=x_0为极小点$$  
1.$$If f''(x_0)<0,x=x_0为极大点$$  

$$证：f'(x_0)=0,f''(x_0)>0$$

$$f''(x_0)=\lim\limits_{x\rightarrow x_0}\frac{f'(x)-f'(x_0)}{x-x_0}=\lim\limits_{x\rightarrow x_0}\frac{f'(x)}{x-x_0}>0$$

$$(极限保号性)\exists\delta>0,当0<|x-x_0|<\delta时,\frac{f'(x)}{x-x_0}>0$$

$$\begin{cases}
f'(x)<0 , x\in(x_0-\delta,x_0) \\
f'(x)>0 , x\in(x_0,x_0+\delta)
\end{cases}$$

$$\therefore x=x_0为极小值$$

例1🌰.$$f(x)=(x-4)\sqrt[3]{(x+1)^2}$$

$$解：1.x\in(-\infty,+\infty)$$

$$2.f'(x)=\frac{5(x-1)}{3\sqrt[3]{x+1}},f'(-1)不存在,f'(1)=0$$

$$3.\begin{cases}
x<-1 & f'(x)>0 \\
-1<x<1 & f'(x)<0
\end{cases}\Rightarrow x=-1为极大值,f(-1)=0$$

$$\begin{cases}
-1<x<1 & f'(x)<0 \\
x>1 & f'(x)>0
\end{cases}\Rightarrow x=1为极小值,f(1)=-3\sqrt[3]{4}$$

三、最值  
case1.$$f(x)\in c[a,b] \exists m,M$$
1.$$f'(x)\begin{cases}
=0 \\
不存在
\end{cases}(a<x<b)\Rightarrow x_1,x_2,...,x_n$$

2.$$\begin{cases}
m = min{f(a),f(x_1),...,f(x_n),f(b)} \\
M = max{f(a),f(x_1),...,f(x_n),f(b)}
\end{cases}$$

例1🌰.$$f(x)=x^2+(1-x)^2(0\leqslant x\leqslant 1)最值$$

$$f'(x)=2x-2(1-x)=0\Rightarrow x=\frac{1}{2}$$

$$\because f(0)=f(1)=1 f(\frac{1}{2})=\frac{1}{2}$$

$$\therefore m=\frac{1}{2},M=1$$

$$\therefore \frac{1}{2}\leqslant x^2+(1-x)^2\leqslant 1(0\leqslant x\leqslant 1)$$

case2.无限区间的最值  
若x=x_0为f(x)位移极值点，x=x_0即为最值点  
例1🌰.$$f(x)=\ln x-\frac{x}{e}+2(x>0)求最大值$$

$$解：x\in(0,+\infty)$$

$$f'(x)=\frac{1}{x}-\frac{1}{e}=0\Rightarrow x=e$$

$$f''(x)=-\frac{1}{x^2}$$

$$\because f''(e)=-\frac{1}{e^2}<0$$

$$\therefore M=f(e)=2$$

$$\therefore x=e为最大值$$

#### 凹凸性与拐点
一、$$def- y=f(x)(x\in I)$$    
1.$$If\forall x_1,x_2\in I且 x_1\neq x_2,有f(\frac{x_1+x_2}{2})<\frac{f(x_1)+f(x_2)}{2},称f(x)在I内为凹函数$$    

2.$$If\forall x_1,x_2\in I且 x_1\neq x_2,有f(\frac{x_1+x_2}{2})>\frac{f(x_1)+f(x_2)}{2},称f(x)在I内为凸函数$$

二、判别法  
Th2.  
1.$$If f''(x)>0(a<x<b),则f(x)在(a,b)内凹$$
2.$$If f''(x)<0(a<x<b),则f(x)在(a,b)内凸$$

$$证：\forall x_1,x_2\in(a,b)且x_1\neq x_2$$

$$取\frac{x_1+x_2}{2}\triangleq x_0$$

$$f(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(\xi)}{2!}(x-x_0)^2(\xi介于x_0与x之间)$$

$$\because f''(x)>0$$

$$\therefore f(x)\geqslant f(x_0)+f'(x_0)(x-x_0) 且在x=x_0时取等于$$

$$\because x_1\neq x_0 x_2\neq x_0$$

$$\therefore f(x_1)>f(x_0)+f'(x_0)(x1-x_0),f(x_2)>f(x_0)+f'(x_0)(x2-x_0)$$

$$\Rightarrow \frac{f(x_1+x_2)}{2}>f(x_0)+f'(x_0)·(\frac{x_1+x_2}{2}-x_0)=f(x_0)$$

$$\therefore f(\frac{x_1+x_2}{2})<\frac{f(x_1)+f(x_2)}{2}$$

$$\therefore f(x)在(a,b)内为凹函数$$

Notes:若x<x_0,x>x_0两侧y=f(x)凹凸性不同，则(x_0,f(x_0))为y=f(x)的拐点

例1🌰.$$y=x^3的凹凸性$$

$$解：y''=6x=0\Rightarrow x=0$$

$$x<0时，y''<0,y=x^3在(-\infty,0)内为凸函数$$

$$x>0时，y''>0,y=x^3在(0,+\infty)内为凸函数$$

$$(0,0)为y=x^3的拐点$$

#### 描图
y=f(x)  
1.$$x\in D$$  
2.$$f'(x)\begin{cases}
=0 \\
不存在
\end{cases}$$  
3.$$f''(x)\begin{cases}
=0 \\
不存在
\end{cases}$$  
4.$$表格$$  
5.$$渐近线\begin{cases}
水平 \\
铅直 \\
斜
\end{cases}$$  
6.描图


