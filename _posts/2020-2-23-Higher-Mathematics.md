---
layout: 		post
title: 			"高等数学_1"
subtitle: 		'极限与连续'
author: 		"CJ"
header-img: 	"img/post-bg-fblog.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - Math
---
> 极限的本质在于无限的接近

## 极限
#### 数列极限的定义与性质

Notes：
1. []取整,[x]取不超过x的最大整数,🌰：[1.2] = 1,[-2.3] = -3
2. $$三角不等式: ||a|-|b|| \leq |a \pm b| \leq |a|-|b|$$

1、定义:   
&nbsp;{an} --> 数列   
&nbsp;A --> 常数  

$$
若\forall\epsilon > 0,\exists N > 0,当n>N时,|an - A| < \epsilon,则\lim\limits_{n \rightarrow \infty}an = A
$$

例1🌰. $$\lim\limits_{n \rightarrow \infty}\frac{n-1}{2n+1} = \frac{1}{2}$$

$$
证明：\forall\epsilon > 0,|\frac{n-1}{2n+1}-\frac{1}{2}|<\epsilon\Rightarrow  
\frac{3}{4n+2}<\epsilon  \Rightarrow 
n>\frac{3-2\epsilon}{4\epsilon}
$$

$$取N = [\frac{3-2\epsilon}{4\epsilon}] (向左取整)$$

$$当n>N时，不等式成立$$

2、性质：
- 唯一性：
$$若\lim\limits_{n \rightarrow \infty}an = A,\lim\limits_{n \rightarrow \infty}an = B,则A=B$$

$$证：设A>B$$

$$取\epsilon = \frac{A-B}{2}>0$$

$$\because\lim\limits_{n \rightarrow \infty}an = A$$

$$\therefore\exists N1>0,当n>N1时，|an-A|<\frac{A-B}{2}
\Rightarrow $$

$$\frac{A+B}{2}<an<\frac{3A-B}{2}(*)$$

$$\because\lim\limits_{n \rightarrow \infty}an = B$$

$$\therefore\exists N2>0,当n>N2时，|an-B|<\frac{A-B}{2}
\Rightarrow $$

$$\frac{3B-A}{2}<an<\frac{A+B}{2}(**)$$

$$取N = max\{N1,N2\},当n>N时,(*)(**)都成立，不等式矛盾，同理A<B矛盾$$

- 保号性：
$$\lim\limits_{n \rightarrow \infty}an = A\begin{cases}
& >0 \\
& <0 
\end{cases}\exists N>0,当n>N时，an\begin{cases}
& >0 \\
& <0 
\end{cases}$$

$$证：当A>0$$

$$取\epsilon=\frac{A}{2}>0$$

$$\because\lim\limits_{n \Rightarrow \infty}an = A,\therefore\exists N>0,当n>N时，|an-A|<\frac{A}{2} \rightarrow$$

$$an>\frac{A}{2}>0$$

- 有界性：
$$\lim\limits_{n \rightarrow \infty}an = A,则 \exists M>0，使|an| \leq M$$

$$取\epsilon=1>0$$

$$\because\lim\limits_{n \rightarrow \infty}an = A,\therefore N>0,当n>N时，|an-A|<1 \Rightarrow $$

$$||an|-|A||<1 \Rightarrow |an|<1+|A|$$

$$取M=MAX\{|a1|,|a2|,...|an|,1+|A|\}$$

$$\therefore\forall n,有|an|\leq M$$

#### 函数极限

Notes：
1. $$x \rightarrow a \Rightarrow x \neq a 
$$  
2. $$x \rightarrow a \Rightarrow \begin{cases}
x \rightarrow a^- & \\
x \rightarrow a^+ &
\end{cases}$$
3. $$a的去心邻域: 0<|x-a|<\delta \Rightarrow x\in(a-\delta)\bigcup(a+\delta)  
$$
4. $$\lim\limits_{x \rightarrow a}f(x) 与 f(a) 无关$$
5.   <center>$$\forall\epsilon>0,\exists\delta>0,当x\in(a-\delta,a)时$$
$$|f(x)-A<\epsilon|,则称A为f(x)在x=a处的左极限,记f(a-0) = A$$</center>
<center>$$\forall\epsilon>0,\exists\delta>0,当x\in(a,a+\delta)时$$
$$|f(x)-B<\epsilon|,则称B为f(x)在x=a处的右极限,记f(a+0) = B$$</center>
🌟$$\lim\limits_{x \rightarrow a}f(x)\exists\Rightarrow f(a-0)和f(a+0)\exists且相等$$

1、定义  
1.自变量趋向于有限数的情形

$$y = f(x)在x=a在去心邻域有定义$$

$$若\forall\epsilon > 0, \exists \delta > 0,当0<|x-a|<\delta时$$

$$|f(x)-A|<\epsilon$$

$$则\lim\limits_{x \rightarrow a}f(x) = A$$

例1🌰.$$\lim\limits_{x \rightarrow 2}(3x+2) = 8$$

$$证：\forall\epsilon>0$$

$$|(3x+2)-8| = 3|x-2|<\epsilon \Rightarrow |x-2|<\frac{\epsilon}{3}$$

$$取\delta = \frac{\epsilon}{3},当0<|x-2|<\delta时$$

$$|(3x+2)-8|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow 2}(3x+2) = 8$$

2.自变量趋向于无穷大的情形  
例1🌰.$$y=arctanx$$

$$\lim\limits_{x \rightarrow -\infty}arctanx=-\frac{\pi}{2}$$

$$\lim\limits_{x \rightarrow +\infty}arctanx=\frac{\pi}{2}$$

例2🌰.$$\lim\limits_{x \rightarrow + \infty}\frac{1}{2x+1}=0$$

$$证：\forall\epsilon>0$$

$$|\frac{1}{2x+1}|=\frac{1}{2x+1}<\epsilon \Rightarrow x>\frac{1}{2}(\frac{1}{\epsilon}-1)$$

$$取X=\frac{1}{2}(\frac{1}{\epsilon}-1)，当x>X时$$

$$|\frac{1}{2x+1}|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow + \infty}\frac{1}{2x+1}=0$$

2、性质
- 唯一性：
$$若\lim f(x) = A,\lim f(x)= B,则A=B$$

$$证：(只证明x \rightarrow a)$$

$$设A>B,取\epsilon = \frac{A-B}{2}>0$$

$$\because\lim\limits_{x \rightarrow a}f(x) = A$$

$$\therefore\delta1>0,当0<|x-a|<\delta1时$$

$$|f(x)-A|<\frac{A-B}{2} \Rightarrow \frac{A+B}{2}<f(x)<\frac{3A-B}{2}(*)$$

$$又\because\lim\limits_{x \rightarrow a}f(x) = B$$

$$\therefore\delta2>0,当0<|x-a|<\delta2时$$

$$|f(x)-B|<\frac{A-B}{2} \Rightarrow \frac{3B-A}{2}<f(x)<\frac{A+B}{2}(**)$$

$$取\delta = min\{\delta1,\delta2\},当0<|x-a|<\delta时,(*)(**)都正确，矛盾$$

- 保号性：
$$\lim\limits_{x \rightarrow a}f(x) = A\begin{cases}
& >0 \\
& <0 
\end{cases}
则\exists\delta>0,当0<|x-a|<\delta时,f(x)\begin{cases}
& >0 \\
& <0 
\end{cases}$$

$$证：当A>0$$

$$取\epsilon=\frac{A}{2}>0,\exists\delta>0,当0<|x-a|<\delta时$$

$$|f(x)-A|<\frac{A}{2} \Rightarrow f(x)>\frac{A}{2}>0$$

#### 无穷小与无穷大

Notes：
1. 0是无穷小，但无穷小未必是0
2. 非零函数是否为无穷小，与自变量的趋向有关

$$\alpha = 3(x-1)^2$$

$$x\rightarrow1时为无穷小$$

$$x\rightarrow2时为不是无穷小$$

1、$$无穷小： 若\lim\limits_{x \rightarrow a}\alpha(x) = 0,则称\alpha(x)当x\rightarrow时为无穷小$$

2、性质：
- $$\alpha\rightarrow0,\beta\rightarrow0 \Rightarrow \alpha\pm\beta\rightarrow0$$

$证：设\lim\limits_{x \rightarrow a}\alpha=0,\lim\limits_{x \rightarrow a}\beta=0$

$$\forall\epsilon>0,\exists\delta1>0,当0<|x-a|<\delta1时$$

$$|\alpha-0|<\epsilon(*)$$

$$\exists\delta2>0,当0<|x-a|<\delta2时$$

$$|\beta-0|<\epsilon(**)$$

$$取\delta=min\{\delta1,\delta2\},当0<|x-a|<\delta时,(*)(**)成立$$

$$当0<|x-a|<\delta时$$

$$|(\alpha\pm\beta)-0|\leq|\alpha|+|\beta|=|a-0|+|\beta-0|<2\epsilon$$

$$即|(\alpha\pm\beta)-0|<2\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}(\alpha\pm\beta)=0$$

- $$\alpha\rightarrow0,\beta\rightarrow0 \Rightarrow \alpha\beta\rightarrow0$$

$$证：设\lim\limits_{x \rightarrow a}\alpha=0,\lim\limits_{x \rightarrow a}\beta=0$$

$$取\epsilon0=1,\exists\delta1>0,当0<|x-a|<\delta1时$$

$$|\alpha-0|<1,即|\alpha|<1(*)$$

$$\forall\epsilon>0,\exists\delta2>0,当0<|x-a|<\delta2时$$

$$|\beta-0|<\epsilon(**)$$

$$取\delta=min\{\delta1,\delta2\},当0<|x-a|<\delta时,(*)(**)成立$$

$$|\alpha\beta-0|=|\alpha||\beta-0|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}\alpha\beta=0$$

- $$|\alpha|\leq M,\beta\rightarrow0,则\alpha\beta\rightarrow0$$

$$证：设\lim\limits_{x \rightarrow a}\beta = 0$$

$$\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta时$$

$$|\beta-0|<\epsilon$$

$$当0<|x-a|<\delta时$$

$$|\alpha\beta-0| = |\alpha||\beta-0|<M\epsilon$$

- $$\lim\limits_{x \rightarrow a}f(x)=A\Rightarrow f(x)=A+\alpha,其中\alpha\rightarrow0(x\rightarrow a)$$

$$证：从左往右(必要性证明)，设\lim\limits_{x \rightarrow a}f(x)=A$$

$$\forall\epsilon,\exists\delta>0,当0<|x-a|<\delta时$$

$$|f(x)-A|<\epsilon$$

$$\alpha = f(x)-A \Rightarrow f(x) =A+\alpha$$

$$\because\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta时$$

$$|\alpha|<\epsilon或|\alpha-0|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}\alpha=0$$

$$证：从右往左(充分性证明)，设f(x)=A+\alpha,\alpha\rightarrow0(x\rightarrow a)$$

$$\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta时$$

$$|\alpha-0|<\epsilon,即|f(x)-A|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}f(x)=A$$

2、无穷大就是无穷小的倒数

#### 极限的运算法则

1、四则  
$$设\lim f(x)=A,\lim g(x)=B,则$$
- $$\lim[f(x)\pm g(x)] = \lim f(x)\pm \lim g(x)$$
- $$\lim f(x)g(x) = \lim f(x)\lim g(x)=AB$$
- $$\lim\frac{f(x)}{g(x)} = \frac{\lim f(x)}{\lim g(x)} = \frac{A}{B}(B\not=0)$$

1.

$$证：\lim f(x)=A \Rightarrow f(x)=A+\alpha,\alpha\rightarrow0$$

$$\lim g(x)=B \Rightarrow f(x)=B+\beta,\beta\rightarrow0$$

$$f(x)\pm g(x) = (A\pm B)+(\alpha\pm\beta)$$

$$\because\alpha\pm\beta\rightarrow0$$

$$\therefore\lim[f(x)\pm g(x)]=A\pm B$$

2.

$$证：\lim f(x)=A \Rightarrow f(x)=A+\alpha,\alpha\rightarrow0$$

$$f(x)g(x)=AB+(A\beta+B\alpha+\alpha\beta)$$

$$\because A\beta+B\alpha+\alpha\beta\rightarrow0$$

$$\therefore f(x)g(x)=AB$$

3.

$$证：\lim f(x)=A \Rightarrow f(x)=A+\alpha,\alpha\rightarrow0(B\not=0)$$

$$取\epsilon0=\frac{|B|}{2}>0,\exists\delta1>0,当0<|x-a|<\delta1时$$

$$|g(x)-B|<\frac{|B|}{2}\Rightarrow||g(x)|-|B||<\frac{|B|}{2}\Rightarrow|g(x)|>\frac{|B|}{2}$$

$$|\frac{f(x)}{g(x)}-\frac{A}{B}| = |\frac{A+\alpha}{B+\beta}-\frac{A}{B}|=\frac{|B\alpha-A\beta|}{|B||g(x)|}$$

$$\because B\alpha-A\beta\rightarrow0$$

$$\therefore\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta1时,|B\alpha-A\beta|<\epsilon$$

$$取\delta=min\{\delta1,\delta2\},当0<|x-a|<\delta时$$

$$|\frac{f(x)}{g(x)}-\frac{A}{B}|<\frac{2}{|B|^2}\epsilon$$

$$\lim\limits_{x \rightarrow a}\frac{f(x)}{g(x)}=\frac{A}{B}$$

例1🌰.$$\lim\limits_{x \rightarrow 2}(x^2+3x)$$

$$解：\lim\limits_{x \rightarrow 2}(x^2+3x)=\lim\limits_{x \rightarrow 2}x^2+\lim\limits_{x \rightarrow 2}3x=4+6=10$$

例2🌰.$$\lim\limits_{x \rightarrow 1}\frac{x^3-1}{x^2-3x+2}$$

$$解:\lim\limits_{x \rightarrow 1}\frac{x^3-1}{x^2-3x+2} = \lim\limits_{x \rightarrow 1}\frac{(x-1)(x^2+x+1)}{(x-1)(x-2)}$$

$$=\lim\limits_{x \rightarrow 1}\frac{x^2+x+1}{x-2}=\frac{\lim\limits_{x \rightarrow 1}(x^2+x+1)}{\lim\limits_{x \rightarrow 1}(x-2)}=-3$$
