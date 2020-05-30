---
layout: 		post
title: 			"高等数学_1"
subtitle: 		'极限与连续'
author: 		"CJ"
header-img: 	"img/post-bg-math.jpg"
outer-img:		"post-bg-math.jpg"
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
2. $$三角不等式：||a|-|b|| \leqslant |a \pm b| \leqslant |a|-|b|$$

1、定义：  
$$  
\{a_n\} \rightarrow 数列,   
A \rightarrow 常数  
$$

$$
若\forall\epsilon > 0,\exists N > 0,当n>N时,|a_n - A| < \epsilon,则\lim\limits_{n \rightarrow \infty}a_n = A 或称数列\{a_n\}收敛于A，\\
否则则称数列\{x_n\}是发散的 \\
通俗来讲就是要证明表达式与极限值的无限接近，即对任意大于0的距离都能找到对应比他小的第n项值 \\
减去极限值的绝对值的数(即第n项与极限的距离)
$$

方法：  
1. $$写|x_n-a|<\epsilon$$
2. $$反解出n>g(\epsilon)$$
3. $$取N=[g(\epsilon)]+1$$

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
$$若\lim\limits_{n \rightarrow \infty}a_n = A,\lim\limits_{n \rightarrow \infty}a_n = B,则A=B$$

$$证：设A>B$$

$$取\epsilon = \frac{A-B}{2}>0$$

$$\because\lim\limits_{n \rightarrow \infty}a_n = A$$

$$\therefore\exists N_1>0,当n>N_1时，|a_n-A|<\frac{A-B}{2}
\Rightarrow $$

$$\frac{A+B}{2}<a_n<\frac{3A-B}{2}(*)$$

$$\because\lim\limits_{n \rightarrow \infty}a_n = B$$

$$\therefore\exists N_2>0,当n>N_2时，|a_n-B|<\frac{A-B}{2}
\Rightarrow $$

$$\frac{3B-A}{2}<a_n<\frac{A+B}{2}(**)$$

$$取N = max\{N_1,N_2\},当n>N时,(*)(**)都成立，不等式矛盾，同理A<B矛盾$$

- 保号性：
$$\lim\limits_{n \rightarrow \infty}a_n = A\begin{cases}
& >0 \\
& <0 
\end{cases}\exists N>0,当n>N时，a_n\begin{cases}
& >0 \\
& <0 
\end{cases}$$

$$证：当A>0$$

$$取\epsilon=\frac{A}{2}>0$$

$$\because\lim\limits_{n \rightarrow \infty}a_n = A,\therefore\exists N>0,当n>N时，|a_n-A|<\frac{A}{2} \Rightarrow$$

$$a_n>\frac{A}{2}>0$$

- 有界性：
$$\lim\limits_{n \rightarrow \infty}a_n = A,则 \exists M>0，使|a_n| \leqslant M$$

$$取\epsilon=1>0$$

$$\because\lim\limits_{n \rightarrow \infty}a_n = A,\therefore N>0,当n>N时，|a_n-A|<1 \Rightarrow $$

$$||a_n|-|A||<1 \Rightarrow |a_n|<1+|A|$$

$$取M=MAX\{|a_1|,|a_2|,...|a_n|,1+|A|\}$$

$$\therefore\forall n,有|a_n|\leqslant M$$

#### 函数极限

Notes：
1. $$x \rightarrow a \Rightarrow x \neq a 
$$  
2. $$x \rightarrow a \Rightarrow \begin{cases}
x \rightarrow a^- & \\
x \rightarrow a^+ &
\end{cases}$$
3. $$a的去心邻域：0<|x-a|<\delta \Rightarrow x\in(a-\delta)\bigcup(a+\delta)  
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

$$\therefore\delta_1>0,当0<|x-a|<\delta_1时$$

$$|f(x)-A|<\frac{A-B}{2} \Rightarrow \frac{A+B}{2}<f(x)<\frac{3A-B}{2}(*)$$

$$又\because\lim\limits_{x \rightarrow a}f(x) = B$$

$$\therefore\delta_2>0,当0<|x-a|<\delta_2时$$

$$|f(x)-B|<\frac{A-B}{2} \Rightarrow \frac{3B-A}{2}<f(x)<\frac{A+B}{2}(**)$$

$$取\delta = min\{\delta_1,\delta_2\},当0<|x-a|<\delta时,(*)(**)都正确，矛盾$$

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

1、$$无穷小： 若\lim\limits_{x \rightarrow a}\alpha(x) = 0,则称\alpha(x)当x\rightarrow a时为无穷小$$

2、性质：
- $$\alpha\rightarrow0,\beta\rightarrow0 \Rightarrow \alpha\pm\beta\rightarrow0$$

$证：设\lim\limits_{x \rightarrow a}\alpha=0,\lim\limits_{x \rightarrow a}\beta=0$

$$\forall\epsilon>0,\exists\delta_1>0,当0<|x-a|<\delta_1时$$

$$|\alpha-0|<\epsilon(*)$$

$$\exists\delta_2>0,当0<|x-a|<\delta_2时$$

$$|\beta-0|<\epsilon(**)$$

$$取\delta=min\{\delta_1,\delta_2\},当0<|x-a|<\delta时,(*)(**)成立$$

$$当0<|x-a|<\delta时$$

$$|(\alpha\pm\beta)-0|\leqslant|\alpha|+|\beta|=|a-0|+|\beta-0|<2\epsilon$$

$$即|(\alpha\pm\beta)-0|<2\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}(\alpha\pm\beta)=0$$

- $$\alpha\rightarrow0,\beta\rightarrow0 \Rightarrow \alpha\beta\rightarrow0$$

$$证：设\lim\limits_{x \rightarrow a}\alpha=0,\lim\limits_{x \rightarrow a}\beta=0$$

$$取\epsilon_0=1,\exists\delta_1>0,当0<|x-a|<\delta_1时$$

$$|\alpha-0|<1,即|\alpha|<1(*)$$

$$\forall\epsilon>0,\exists\delta_2>0,当0<|x-a|<\delta_2时$$

$$|\beta-0|<\epsilon(**)$$

$$取\delta=min\{\delta_1,\delta_2\},当0<|x-a|<\delta时,(*)(**)成立$$

$$|\alpha\beta-0|=|\alpha||\beta-0|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow a}\alpha\beta=0$$

- $$|\alpha|\leqslant M,\beta\rightarrow0,则\alpha\beta\rightarrow0$$

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

$$取\epsilon_0=\frac{|B|}{2}>0,\exists\delta_1>0,当0<|x-a|<\delta_1时$$

$$|g(x)-B|<\frac{|B|}{2}\Rightarrow||g(x)|-|B||<\frac{|B|}{2}\Rightarrow|g(x)|>\frac{|B|}{2}$$

$$|\frac{f(x)}{g(x)}-\frac{A}{B}| = |\frac{A+\alpha}{B+\beta}-\frac{A}{B}|=\frac{|B\alpha-A\beta|}{|B||g(x)|}$$

$$\because B\alpha-A\beta\rightarrow0$$

$$\therefore\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta_1时,|B\alpha-A\beta|<\epsilon$$

$$取\delta=min\{\delta_1,\delta_2\},当0<|x-a|<\delta时$$

$$|\frac{f(x)}{g(x)}-\frac{A}{B}|<\frac{2}{|B|^2}\epsilon$$

$$\lim\limits_{x \rightarrow a}\frac{f(x)}{g(x)}=\frac{A}{B}$$

例1🌰.$$\lim\limits_{x \rightarrow 2}(x^2+3x)$$

$$解：\lim\limits_{x \rightarrow 2}(x^2+3x)=\lim\limits_{x \rightarrow 2}x^2+\lim\limits_{x \rightarrow 2}3x=4+6=10$$

例2🌰.$$\lim\limits_{x \rightarrow 1}\frac{x^3-1}{x^2-3x+2}$$

$$解：\lim\limits_{x \rightarrow 1}\frac{x^3-1}{x^2-3x+2} = \lim\limits_{x \rightarrow 1}\frac{(x-1)(x^2+x+1)}{(x-1)(x-2)}$$

$$=\lim\limits_{x \rightarrow 1}\frac{x^2+x+1}{x-2}=\frac{\lim\limits_{x \rightarrow 1}(x^2+x+1)}{\lim\limits_{x \rightarrow 1}(x-2)}=-3$$

例3🌰.$$\lim\limits_{x \rightarrow 2}\frac{x}{x^2-4}$$

$$解：\because\lim\limits_{x \rightarrow 2}\frac{x^2-4}{x}=\frac{\lim\limits_{x \rightarrow 2}(x^2-4)}{\lim\limits_{x \rightarrow 2}x}=0$$

$$\therefore\lim\limits_{x \rightarrow 2}\frac{x}{x^2-4}=\infty$$

例4🌰.$$\lim\limits_{x \rightarrow \infty}\frac{3x^2+2x-5}{x^2-x+4}$$

$$\lim\limits_{x \rightarrow \infty}\frac{3x^2+2x-5}{x^2-x+4}=\lim\limits_{x \rightarrow \infty}\frac{3+\frac{2}{x}-\frac{5}{x^2}}{1-\frac{1}{x}+\frac{4}{x^2}}=3$$

例5🌰.$$\lim\limits_{x \rightarrow \infty}\frac{x+2}{2x^2-x+1}$$

$$解：\lim\limits_{x \rightarrow \infty}\frac{x+2}{2x^2-x+1}=\lim\limits_{x \rightarrow \infty}\frac{\frac{1}{x}+\frac{2}{x^2}}{2-\frac{1}{x}+\frac{1}{x^2}}=0$$

例6🌰.$$\lim\limits_{x \rightarrow \infty}\frac{x^2-3x+4}{2x+1}$$

$$解：\because\lim\limits_{x \rightarrow \infty}\frac{2x+1}{x^2-3x+4}=0$$

$$\therefore\lim\limits_{x \rightarrow \infty}\frac{x^2-3x+4}{2x+1}=\infty$$

结论：

$$\lim\limits_{x \rightarrow \infty}\frac{a_m x^m+...+a_1 x+a_0}{b_n x^n+...+b_1 x+b_0}=\begin{cases}
\frac{a_m}{b_n} & m=n \\
0 & m<n \\
\infty & m>n 
\end{cases}$$

2、复合

$$y=f(u),\lim\limits_{u \rightarrow a}f(u)=A$$

$$u=\varphi(x)(\varphi(x)\not=a),\lim\limits_{x \rightarrow x_0}\varphi(x)=a$$

$$则\lim\limits_{x \rightarrow x_0}f[\varphi(x)]=A$$

$$证：\forall\epsilon>0$$

$$\because\lim\limits_{u \rightarrow a}f(u)=A,\therefore\exists\eta>0,当0<|u-a|<\eta时$$

$$|f(u)-A|<\epsilon(*)$$

$$对\eta>0$$

$$\because\lim\limits_{x \rightarrow x_0}\varphi(x)=a,\therefore\exists\delta>0,当0<|x-x_0|<\delta时$$

$$|\varphi(x)-a|<\eta(**)$$

$$\therefore\forall\epsilon>0,\exists\delta>0,当0<|x-x_0|<\delta时，|f[\varphi(x)]-A|<\epsilon$$

$$\therefore\lim\limits_{x \rightarrow x_0}f[\varphi(x)]=A$$

#### 极限存在准则 两个重要极限
一、极限存在准则  
1、准则一：夹逼定理（迫敛定理）
- 数列型

$$1.a_n \leqslant b_n \leqslant c_n 2.\lim\limits_{n \rightarrow \infty}a_n=\lim\limits_{n \rightarrow \infty}c_n=A$$

$$则\lim\limits_{n \rightarrow \infty}b_n=A$$

$$证：\forall\epsilon>0,\exists N_1>0,当n>N_1时,有|a_n-A|<\epsilon\Rightarrow A-\epsilon<a_n<A+\epsilon(*)$$

$$\exists N_2>0,当n>N_2时,有|c_n-A|<\epsilon\Rightarrow A-\epsilon<c_n<A+\epsilon(**)$$

$$N=max\{N_1,N_2\},当n>N时(*)(**)成立$$

$$A-\epsilon<a_n \leqslant b_n \leqslant c_n < A+\epsilon$$

$$A-\epsilon<b_n<A+\epsilon \Rightarrow |b_n-A|<\epsilon$$

$$即\forall\epsilon>0,\exists N>0,当m>N时,|b_n-A|<\epsilon$$

$$\therefore\lim\limits_{n \rightarrow \infty}b_n=A$$

- 函数型 
证明同上

例1🌰.$$\lim\limits_{n \rightarrow \infty}(2^n+3^n+4^n)^\frac{1}{n}$$

$$解：4^n\leqslant2^n+3^n+4^n\leqslant3*4^n$$

$$4\leqslant(2^n+3^n+4^n)^\frac{1}{n}\leqslant3^\frac{1}{n}*4$$

$$\because\lim\limits_{n \rightarrow \infty}左=4,\lim\limits_{n \rightarrow \infty}右=4$$

$$\therefore\lim\limits_{n \rightarrow \infty}(2^n+3^n+4^n)^\frac{1}{n}=4$$

$$一般来说：a>0,b>0,c>0$$

$$则\lim\limits_{n \rightarrow \infty}(a^n+b^n+c^n)^\frac{1}{n}=max\{a,b,c\}$$

例2🌰.$$\lim\limits_{n \rightarrow \infty}(\frac{1}{\sqrt{n^2+1}}+\frac{1}{\sqrt{n^2+2}}+...+\frac{1}{\sqrt{n^2+n}})（分母次数不齐）$$

$$解：令b_n=\frac{1}{\sqrt{n^2+1}}+\frac{1}{\sqrt{n^2+2}}+...+\frac{1}{\sqrt{n^2+n}}$$

$$\frac{n}{\sqrt{n^2+n}}\leqslant b_n \leqslant\frac{n}{\sqrt{n^2+1}}$$

$$\lim\limits_{n \rightarrow \infty}左=1,\lim\limits_{n \rightarrow \infty}右=1$$

2、准则二：单调有界的数列必定存在极限  
Notes:
1. $$如果\exists M>0,\forall n,有|a_n|\leqslant M,则{a_n}有界$$
2. $$\{a_n\}\uparrow\begin{cases}
无上界 & \Rightarrow \lim\limits_{n \rightarrow \infty}a_n=+\infty \\
\exists M,a_n\leqslant M & \Rightarrow \lim\limits_{n \rightarrow \infty}a_n \exists
\end{cases}$$

$$\{a_n\}\downarrow\begin{cases}
无下界 & \Rightarrow \lim\limits_{n \rightarrow \infty}a_n=-\infty \\
\exists M,a_n\geq M & \Rightarrow \lim\limits_{n \rightarrow \infty}a_n \exists
\end{cases}$$

例1🌰.$$0<a_1<\frac{\pi}{2},a_{n+1}=sin(a_n),证:\lim\limits_{n \rightarrow \infty}a_n\exists$$

$$解：由题得a_n>0$$

$$\because sinx<x(0<x<\frac{\pi}{2})$$

$$\therefore a_{n+1}=sin(a_n)<a_n \Rightarrow \{a_n\}\downarrow$$

$$\therefore\lim\limits_{n\rightarrow\infty}a_n\exists$$

$$由a_{n+1}=sin(a_n) \Rightarrow A=sinA$$

$$\therefore A=0$$

例2🌰.$$a_1=\sqrt{2},a_2=\sqrt{2\sqrt{2}},a_3=\sqrt{2\sqrt{2\sqrt{2}}},...证:\lim\limits_{n \rightarrow \infty}a_n\exists$$

$$a_{n+1} = \sqrt{2+a_n},由题得\{a_n\}\uparrow$$

$$假设a_n\leqslant 2$$

$$a_1=\sqrt{2}<2$$

$$设a_k \leqslant 2$$

$$a_{k+1}=\sqrt{2+a_k} \leqslant 2$$

$$\therefore\forall n,有a_n \leqslant 2$$

$$\therefore\lim\limits_{n \rightarrow \infty}a_n\exists$$

二、两个重要极限  
$$对0<x<\frac{\pi}{2}$$
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200229-circle.png)

$$S\Delta AOB=\frac{1}{2}OB*OAsinx=\frac{1}{2}sinx$$

$$S扇AOB=\frac{1}{2}OA*x = \frac{1}{2}x$$

$$S\Delta AOC = \frac{1}{2}OA*AC = \frac{1}{2}tanx$$

$$\Rightarrow\frac{1}{2}sinx<\frac{1}{2}x<\frac{1}{2}tanx$$

$$\therefore当0<x<\frac{\pi}{2}时,\Rightarrow\frac{1}{2}sinx<\frac{1}{2}x<\frac{1}{2}tanx$$

$$\Rightarrow 1<\frac{x}{sinx}<\frac{1}{cosx}$$

$$0<1-cosx=2sin^2\frac{x}{2}<2(\frac{x}{2})^2=\frac{1}{2}x^2$$

$$\because\lim\limits_{x \rightarrow 0^+}左=0,\lim\limits_{x \rightarrow 0^+}右=0$$

$$\therefore\lim\limits_{x \rightarrow 0^+}(1 - cosx)=0\Rightarrow\lim\limits_{x \rightarrow 0^+}cosx=1$$

$$\because\lim\limits_{x \rightarrow 0^+}左=1,\lim\limits_{x \rightarrow 0^+}右=1$$

$$对1<\frac{x}{sinx}<\frac{1}{cosx}$$

$$\therefore\lim\limits_{x \rightarrow 0^+}\frac{x}{sinx}=1$$

$$\because\frac{x}{sinx}为偶函数,\therefore\lim\limits_{x \rightarrow 0^-}\frac{x}{sinx}=1,\therefore\lim\limits_{x \rightarrow 0}\frac{x}{sinx}=1$$

重要极限1：$$\lim\limits_{x \rightarrow 0}\frac{x}{sinx}=1$$

$$一般地,\lim\limits_{\Delta \rightarrow 0}\frac{\Delta}{sin\Delta}=1$$

例1🌰.$$\lim\limits_{x \rightarrow 0}\frac{tanx}{x}$$

$$解：\lim\limits_{x \rightarrow 0}\frac{tanx}{x}=\lim\limits_{x \rightarrow 0}\frac{sinx}{x}*\frac{1}{cosx}=1*1=1$$

例2🌰.$$\lim\limits_{x \rightarrow 0}\frac{1-cosx}{x^2}$$

$$解：\lim\limits_{x \rightarrow 0}\frac{1-cosx}{x^2}=\lim\limits_{x \rightarrow 0}\frac{2sin^2\frac{x}{2}}{x^2}$$

$$=\lim\limits_{x \rightarrow 0}\frac{1}{2}*\frac{sin^2\frac{x}{2}}{(\frac{x}{2})^2}=\lim\limits_{x \rightarrow 0}\frac{1}{2}(\frac{sin\frac{x}{2}}{\frac{x}{2}})^2=\frac{1}{2}$$

例3🌰.$$\lim\limits_{x \rightarrow 0}\frac{arcsinx}{x}$$

$$解：\lim\limits_{x \rightarrow 0}\frac{arcsinx}{x}$$

$$设x=sint$$

$$\lim\limits_{t \rightarrow 0}\frac{t}{sint}=1$$

Notes:
1.二项式定理：$$(a+b)^n=\sum_{r=0}^{n} C_n^r a^nr b^r(n \in N^*)$$

重要极限2：$$\lim\limits_{\Delta \rightarrow 0}(1+\Delta)^{\frac{1}{\Delta}} =  e$$

$$a_n=(1+\frac{1}{n})^n$$

$$a_n=(1+\frac{1}{n})^n = C_n^0+C_n^1\frac{1}{n}+...+C_n^n\frac{1}{n^n}$$

$$a_{n+1} = (1+\frac{1}{n+1})^{n+1} = C_n^0+C_n^1\frac{1}{n+1}+...+C_n+1^{n+1}\frac{1}{n+1^{n+1}}$$

$$\Rightarrow a_{n+1}>a_n\Rightarrow \{a_n\}\uparrow$$

$$\because a_n \leqslant 1+1+\frac{1}{2!}+\frac{1}{3!}+...+\frac{1}{n!}\leqslant 1+1+\frac{1}{1*2}+\frac{1}{3*4}+...++\frac{1}{(n-1)*n} = 3-\frac{1}{n} \leqslant 3$$

$$\therefore\lim\limits_{n \rightarrow \infty}(1+\frac{1}{n})^n\exists$$

例1🌰.$$\lim\limits_{x \rightarrow 0}(1+3x)^\frac{1}{sinx}$$

$$解：\lim\limits_{x \rightarrow 0}[(1+3x)^{\frac{1}{3x}}]^{\frac{3x}{sinx}}$$

$$=e^{\lim\limits_{x \rightarrow 0}\frac{3x}{sinx}}$$

$$=e^3$$

例2🌰.$$\lim\limits_{x \rightarrow 0}(1-x^2)^{\frac{1}{xsinx}}$$

$$解：\lim\limits_{x \rightarrow 0}[(1-x^2)^{\frac{1}{-x^2}}]^{\frac{-x}{sinx}}$$

$$=e^{\lim\limits_{x \rightarrow 0}\frac{-x}{sinx}}$$

$$=\frac{1}{e}$$

#### 无穷小的比较
$$\alpha \rightarrow 0 , \beta \rightarrow 0$$

$$1.If \lim\frac{\beta}{\alpha}=0,则\beta为\alpha的高阶无穷小,记\beta=o(\alpha)$$

$$2.If \lim\frac{\beta}{\alpha}=l(\neq0,\infty),则\beta为\alpha的同阶无穷小,记作\beta=O(\alpha)$$

$$3.If \lim\frac{\beta}{\alpha}=1,则\beta为\alpha的等价无穷小,记\alpha \sim \beta$$

$$If \lim\frac{\beta}{\alpha^k}=l(\neq0,\infty)(k>0),则\beta为\alpha的k阶无穷小$$

$$🌰 如：\alpha = x,\beta = 4x^3+x^4$$

$$\lim\limits_{x \rightarrow 0}\frac{\beta}{x^3} = \lim\limits_{x \rightarrow 0}(4+x)=4$$

$$\beta为\alpha的3阶无穷小$$


性质  
一般性质：  

$$1.\alpha \rightarrow 0,\beta \rightarrow 0 \Rightarrow\begin{cases}
\alpha\pm\beta \rightarrow 0 \\
\alpha\beta \rightarrow 0\\
k\alpha \rightarrow 0
\end{cases}$$

$$2.|\alpha|\leqslant M,\beta \rightarrow 0 \Rightarrow \alpha\beta \rightarrow 0$$

$$3.\lim f(x)=A \Rightarrow f(x)=A+\alpha,\alpha\rightarrow 0$$

等价性质：  

$$1. \begin{cases}
\alpha\sim\alpha \\
\alpha\sim\beta \Rightarrow \beta \sim \alpha \\
\alpha\sim\beta,\beta\sim\gamma \Rightarrow \alpha\sim\gamma
\end{cases}$$

$$证：\alpha\sim\beta\Rightarrow\lim\frac{\beta}{\alpha}=1$$

$$\beta\sim\gamma\Rightarrow\lim\frac{\gamma}{\beta}=1$$

$$\because\frac{\gamma}{\alpha}=\frac{\beta}{\alpha}·\frac{\gamma}{\beta},\therefore\lim\frac{\gamma}{\alpha}=1$$

$$2. \alpha\sim\alpha',\beta\sim\beta'且\lim\frac{\beta'}{\alpha'}=A,则\lim\frac{\beta}{\alpha}=A$$

$$证：\frac{\beta}{\alpha}=\frac{\alpha'}{\alpha}·\frac{\beta'}{\alpha'}·\frac{beta}{beta'}$$

$$\because\lim\frac{\alpha'}{\alpha}=1,\lim\frac{\beta'}{\beta}=1$$

$$\lim\frac{\beta}{\alpha}=A$$

$$3. \alpha\sim\beta\Rightarrow\beta = \alpha+o(\alpha)$$

$$证：\alpha\sim\beta\Rightarrow\lim\frac{\beta}{\alpha}=1$$

$$\Rightarrow\frac{\beta}{\alpha}=1+\gamma,\gamma\rightarrow0$$

$$\beta=\alpha+\alpha\gamma$$

$$\because\lim\frac{\alpha\gamma}{\alpha}=\lim\gamma=0,\therefore\alpha\gamma=o(\alpha)$$

$$\therefore\beta=\alpha+o(\alpha)$$

$$\beta=\alpha+o(\alpha)$$

$$\Rightarrow\frac{\beta}{\alpha}=1+\frac{o(\alpha)}{\alpha}\Rightarrow\lim\frac{\beta}{\alpha}=1$$

$$\therefore\alpha\sim\beta$$

常见的等价无穷小  

$$\lim\limits_{x \rightarrow 0}\frac{sinx}{x}=1\Rightarrow x\sim sinx$$

$$\lim\limits_{x \rightarrow 0}\frac{tanx}{x}=1\Rightarrow x\sim tanx$$

$$\lim\limits_{x \rightarrow 0}\frac{arcsinx}{x}=1\Rightarrow x\sim arcsinx$$

$$\lim\limits_{x \rightarrow 0}\frac{arctanx}{x}=1,设x=tant\Rightarrow \lim\limits_{t \rightarrow 0}\frac{t}{tant}=1\Rightarrow x\sim arctanx$$

$$\lim\limits_{x \rightarrow 0}\frac{\ln(1+x)}{x} = \lim\limits_{x \rightarrow 0}\frac{1}{x}\ln(1+x) = \lim\limits_{x \rightarrow 0}\ln(1+x)^\frac{1}{x} = 1\Rightarrow x\sim \frac{\ln(1+x)}{x}$$

$$\lim\limits_{x \rightarrow 0}\frac{e^x-1}{x},设e^x-1=t\Rightarrow\lim\limits_{t \rightarrow 0}\frac{t}{\ln(1+t)}=1\Rightarrow x\sim e^x-1$$

$$综上,x\rightarrow0时,x \sim sinx \sim tanx \sim arcsinx \sim arctanx \sim e^x-1 \sim \ln(1+x)$$

$$\because\lim\limits_{x \rightarrow 0}\frac{1-cosx}{x^2}=\frac{1}{2}$$

$$\therefore x\rightarrow 0时,1-cosx\sim \frac{1}{2}x^2$$


例1🌰.$$\lim\limits_{x \rightarrow 0}\frac{(1+x)^a-1}{x}$$

$$=\lim\limits_{x \rightarrow 0}\frac{e^{a\ln(1+x)}-1}{x}$$

$$\because e^\Delta-1\sim\Delta(\Delta\rightarrow0)$$

$$=\lim\limits_{x \rightarrow 0}\frac{a\ln(1+x)}{x}=a$$


$$推得x\rightarrow0时 (1+x)^a-1\sim ax,一般地 (1+\Delta)^a-1\sim a\Delta(\Delta\rightarrow0)$$

$$总结：当x\rightarrow0时,常见的有x \sim sinx \sim tanx \sim arcsinx \sim arctanx \sim e^x-1 \sim \ln(1+x)$$

$$1-cosx\sim \frac{1}{2}x^2$$

$$(1+x)^a-1\sim ax$$

例1🌰.$$\lim\limits_{x\rightarrow0}\frac{(1+2x)^x-1}{xsinx}$$

$$=\lim\limits_{x\rightarrow0}\frac{e^{x\ln(1+2x)}-1}{x^2}$$

$$=\lim\limits_{x\rightarrow0}\frac{x\ln(1+2x)}{x^2}=\lim\limits_{x\rightarrow0}\frac{\ln(1+2x)}{x}=2$$

例2🌰.$$\lim\limits_{x\rightarrow0}\frac{\sqrt{1+tanx}-\sqrt{1+sinx}}{x^3}$$

$$=\lim\limits_{x\rightarrow0}\frac{1}{\sqrt{1+tanx}+\sqrt{1+sinx}}*\frac{tanx-sinx}{x^3}$$

$$=\frac{1}{2}\lim\limits_{x\rightarrow0}\frac{tanx-sinx}{x^3}$$

$$=\frac{1}{2}\lim\limits_{x\rightarrow0}\frac{tanx}{x}*\frac{1-cosx}{x^2}=\frac{1}{4}$$

例3🌰.$$\lim\limits_{x\rightarrow0}\frac{tan2x}{tan5x}$$

$$=\lim\limits_{x\rightarrow0}\frac{2x}{5x}=\frac{2}{5}$$

例4🌰.$$\lim\limits_{x\rightarrow0}\frac{(1+x^2)^{\frac{1}{3}}-1}{cosx-1}$$

$$=\lim\limits_{x\rightarrow0}\frac{\frac{x^2}{3}}{-\frac{x^2}{2}}=-\frac{2}{3}$$

#### 连续性与间断点

$$注：\lim\limits_{x\rightarrow a}f(x)与f(a)无关$$

$$如：f(x)=\frac{sin2x}{x},f(0)不存在$$

$$但\lim\limits_{x\rightarrow a}f(x)=2$$

$$又如：f(x)=\begin{cases}
\frac{\ln(1+x^2)}{1-cosx} & -1<x<0\\
1 & x=0 \\
\frac{e^{2x}-1}{sin2x} & 0<x<1
\end{cases}$$

$$f(0^-) = \lim\limits_{x\rightarrow 0^-}\frac{\ln(1+x^2)}{1-cosx}=2$$

$$f(0^+) = \lim\limits_{x\rightarrow 0^+}\frac{e^{2x}-1}{sin2x}=2$$

$$\therefore\lim\limits_{x\rightarrow 0}f(x)=2\neq f(0)$$

一、连续性  
定义：$$y=f(x)在x=x_0邻域内连续(邻域包括x_0,区别于去心邻域)$$

$$如果\lim\limits_{x\rightarrow x_0}f(x)=f(x_0),则f(x)在x=x_0连续$$

二、间断点  
定义：$$如果\lim\limits_{x\rightarrow x_0}f(x)\neq f(x_0),则x=x_0为f(x)的间断点$$

$$第一类：f(x_0^-),f(x_0^+)\exists
\begin{cases}
f(x_0^-)=f(x_0^+)(\neq f(x_0)) & x_0为可去间断点 \\
f(x_0^-) \neq f(x_0^+) & x_0为跳跃间断点 
\end{cases}$$


$$第二类：f(x_0^-),f(x_0^+)至少有一个不存在$$

$$例1🌰.f(x)=\frac{|x|}{x},求间断点与分类$$

$$解：x=0为间断点$$

$$f(0^-)=\lim\limits_{x\rightarrow 0^-}=\frac{|x|}{x}=-1$$

$$f(0^+)=\lim\limits_{x\rightarrow 0^+}=\frac{|x|}{x}=1$$

$$f(0^-)\neq f(0^+)$$

$$x=0为跳跃间断点$$

$$例2🌰.f(x)=\frac{x^2-3x+2}{x^2-1},求间断点与分类$$

$$解：x=\pm1为间断点$$

$$\lim\limits_{x\rightarrow-1}f(x)=\infty\Rightarrow x=-1为第二类间断点$$


$$\lim\limits_{x\rightarrow1}f(x)=-\frac{1}{2}\Rightarrow x=1为可去间断点$$

$$例3🌰.f(x)=\frac{2^{\frac{1}{x-1}}}{1+2^{\frac{1}{x-1}}}$$

$$解：x=1为间断点$$

$$f(1^-) = \lim\limits_{x\rightarrow1^-}\frac{2^{\frac{1}{x-1}}}{1+2^{\frac{1}{x-1}}}$$

$$\because x-1\rightarrow 0^-,则\frac{1}{x-1}\rightarrow-\infty$$

$$=0$$

$$f(1^+) = \lim\limits_{x\rightarrow1^+}\frac{2^{\frac{1}{x-1}}}{1+2^{\frac{1}{x-1}}}$$

$$=\lim\limits_{x\rightarrow 1^+}\frac{1}{\frac{1}{2^{\frac{1}{x-1}}}+1}=1$$

$$\because f(1^-)\neq f(1^+) $$

$$\therefore x=1为跳跃间断点$$

#### 连续函数的运算与初等函数的连续性

一、连续函数的运算性质  
1.$$f(x)、g(x)在x=x_0连续,则f(x)\pm g(x)、f(x)g(x)、\frac{f(x)}{g(x)}(g(x_0)\neq0),在x_0都连续$$

$$如：\lim\limits_{x\rightarrow x_0}f(x)=f(x_0),\lim\limits_{x\rightarrow x_0}g(x)=g(x_0)\Rightarrow\lim\limits_{x\rightarrow x_0}f(x)g(x)=f(x_0)g(x_0)$$

2.$$y=f(u)在u=a连续,u=\phi(x)且\lim\limits_{x\rightarrow x_0}\phi(x)=a则\lim\limits_{x\rightarrow x_0}f[\phi(x)]=f(a)$$

$$证：\because\lim\limits_{u\rightarrow a}f(u)=f(a)$$

$$\therefore\forall\epsilon>0,\exists\eta>0,当0<|u-a|<\eta时,|f(u)-f(a)|<\epsilon$$

$$\because\lim\limits_{x\rightarrow x_0}\phi(x)=a$$

$$\therefore对\eta>0,\exists\delta>0,当0<|x-x_0|<\delta时，|\phi(x)-a|<\eta$$

$$当0<|x-x_0|<\delta时$$

$$|f[\phi(x)]-f(a)|<\epsilon$$

$$\therefore\lim\limits_{x\rightarrow x_0}f[\phi(x)]=f(a)$$

$$即\lim\limits_{x\rightarrow x_0}f[\phi(x)]=f[\lim\limits_{x\rightarrow x_0}\phi(x)]$$

$$如：\lim\limits_{x\rightarrow0}(cosx)^{\frac{1}{x^2}}$$

$$\lim\limits_{x\rightarrow0}\{[1+(cosx-1)^{\frac{1}{cosx-1}}]\}^\frac{cosx-1}{x^2}$$

$$=\lim\limits_{x\rightarrow0}e^\frac{cosx-1}{x^2}$$

$$=e^{-\frac{1}{2}}$$

二、初等函数连续性  
1.基本初等函数-$$\begin{cases}
x^a \\
a^x (a>0且a\neq1) \\
\log_ax(a>0且a\neq1) \\
sinx、cosx、tanx、cotx...
\end{cases}$$

2.初等函数-$$由\begin{cases}
常数 \\
基本初等函数
\end{cases}经过有限次的\begin{cases}
四则 \\
复合
\end{cases}而成的式子$$

🌟初等函数在定义域内连续

$$例1🌰.\lim\limits_{x\rightarrow0}\frac{\log_a(1+x)}{x}$$

$$解：原式=\lim\limits_{x\rightarrow0}\frac{1}{x}\log_a(1+x)=\lim\limits_{x\rightarrow0}log_a(1+x)^{\frac{1}{x}}$$

$$=\log_a\lim\limits_{x\rightarrow0}(1+x)^{\frac{1}{x}}=\log_ae=\frac{1}{\ln a}$$

$$例2🌰.\lim\limits_{x\rightarrow0}\frac{a^x-1}{x}$$

$$法一：令a^x-1=t\Rightarrow x=\frac{1}{\ln a}·\ln(1+t)$$

$$原式=\lim\limits_{t\rightarrow0}\frac{t}{\frac{1}{\ln a}\ln(1+t)}=\ln a\lim\limits_{t\rightarrow0}\frac{t}{\ln(1+t)}=\ln a$$

$$法二：原式=\lim\limits_{x\rightarrow0}\frac{e^{x\ln a-1}}{x}=\lim\limits_{x\rightarrow0}\frac{x\ln a}{x}=\ln a$$

#### 闭区间上连续函数的性质
一、闭区间连续函数的定义
设f(x)在[a,b]上有定义
若  
1.f(x)在(a,b)内连续  
2.$$f(a)=f(a^+),f(b)=f(b^-)
则f(x)在[a,b]上连续,记f(x)\in c[a,b]$$

二、$$f(x)\in c[a,b]四大性质$$

1.最大值和最小值定理

$$设f(x)\in c[a,b],则f(x)在[a,b]一定取到最小值m和最大值M$$

$$即\exists x_1\in[a,b],f(x_1)=m$$

$$ \exists x_2\in[a,b],f(x_2)=M$$

2.有界定理

$$设f(x)\in c[a,b]则一定\exists k>0使|f(x)|\leqslant k$$

3.零点定理

$$设f(x)\in c[a,b],且f(a)f(b)<0,一定存在c\in(a,b),使f(c)=0$$

4.介值定理

$$设f(x)\in c[a,b],则\forall\eta\in[m,M],\exists\delta\in[a,b]使f(\delta)=\eta $$

例1🌰.$$f(x)\in c[0,1],f(0)=1,f(1)=0,证明\exists c\in(0,1),使f(c)=c$$

$$令\phi(x)=f(x)-x$$

$$\phi(x)\in c[0,1]$$

$$\phi(0)=1,\phi(1)=-1$$

$$\because\phi(0)\phi(1)<0$$

$$\therefore\exists c\in(0,1),使\phi(c)=0$$

$$\therefore f(c)-c=0\Rightarrow f(c)=c$$

例2🌰.$$f(x)\in c[0,2],且f(0)+2f(1)+3f(2)=6,证明\exists c\in[0,2],使f(c)=1$$

$$证：\because f(x)\in c[0,2]\therefore\exists m,M$$

$$6m\leqslant f(0)+2f(1)+3f(2) \leqslant 6M$$

$$m\leqslant1\leqslant M$$

$$\therefore c\in[0,2]使f(c)=1$$

#### 理论体系
Part1 极限  
一、定义  
(1)极限  
1. $$(\epsilon-N)If\forall\epsilon>0,\exists N>0,当n>N时,|a_n-A|<\epsilon,\lim\limits_{x\rightarrow\infty}a_n=A$$
2. $$(\epsilon-\delta)If\forall\epsilon>0,\exists\delta>0,当0<|x-a|<\delta时,|f(x)-A|<\epsilon,\lim\limits_{x\rightarrow a}f(x)=A$$
3. $$(\epsilon-x)\begin{cases}
x\rightarrow -\infty \\
x\rightarrow +\infty &If\forall\epsilon>0,\exists X>0,当x>X时,|f(x)-A|<\epsilon,\lim\limits_{x\rightarrow+\infty}f(x)=A\\
x\rightarrow \infty
\end{cases}$$

(2)无穷小  
$$If\lim\limits_{x\rightarrow a}\alpha(x)=0,则\alpha(x)当x\rightarrow a为无穷小$$

$$设\alpha\rightarrow0,\beta\rightarrow0\begin{cases}
\lim\frac{\beta}{\alpha}=0 & \beta=o(\alpha)高阶无穷小 \\
\lim\frac{\beta}{\alpha}=k(\neq0,\infty) & \beta=O(\alpha) 同阶无穷小\\
lim\frac{\beta}{\alpha}=1 & \alpha\sim\beta 等价无穷小
\end{cases}$$

二、性质  
(1)一般性质
1. 唯一性
2. 保号性
3. 有界性

(2)运算性质
1. 四则：$$\lim f(x)=A,\lim g(x)=B,则：$$

$$\lim[f(x)\pm g(x)]=A\pm B$$

$$\lim f(x)g(x)=AB$$

$$\lim\frac{f(x)}{g(x)}=\frac{A}{B}(B\neq0)$$

2. 复合：$$\lim\limits_{u\rightarrow a}f(u)=A,u=\phi(x)且\phi(x)\neq a,\lim\limits_{x\rightarrow x_0}\phi(x)=a,则\lim\limits_{x\rightarrow x_0}f[\phi(x)]=A$$

(3)存在性质
1. 迫敛定理
2. 单调有界数列必有极限

(4)无穷小的性质  
一般性质    
1. $$\alpha\rightarrow0,\beta\rightarrow0\Rightarrow\begin{cases}
\alpha\pm\beta\rightarrow0 \\
\alpha\beta\rightarrow0 \\
k\alpha\rightarrow0 \\
\end{cases}$$
2. $$|\alpha|\leqslant M,\beta\rightarrow0 \Rightarrow \alpha\beta\rightarrow0$$
3. $$\lim f(x)=A\Rightarrow f(x)=A+\alpha,\alpha\rightarrow0$$

等价性质  
$$\alpha\sim\alpha',\beta\sim\beta'且\lim\frac{\beta'}{\alpha'}=A\Rightarrow\lim\frac{\beta}{\alpha}=A$$

常见的等价无穷小$$(x\rightarrow0)$$  

$$x \sim sinx \sim tanx \sim arcsinx \sim arctanx \sim e^x-1 \sim \ln(1+x)$$

$$1-cosx\sim \frac{1}{2}x^2$$

$$(1+x)^a-1\sim ax$$

三、两个重要极限
1. $$\lim\limits_{\Delta\rightarrow0}\frac{sin\Delta}{\Delta}=1$$
2. $$\lim\limits_{\Delta\rightarrow0}(1+\Delta)^{\frac{1}{\Delta}}=e$$

Part2 连续与间断  
一、概念  
1. 连续-$$If\lim\limits_{x\rightarrow a}f(x)=f(a)则f(x)在x=a连续$$
2. 间断-$$If\lim\limits_{x\rightarrow a}f(x)\neq f(a)则f(x)在x=a间断$$

二、$$f(x)\in c[a,b]的四大性质$$

## 例题
例1🌰.$$a_1=2,a_{n+1}=\frac{1}{2}(a_n+\frac{1}{a_n}),证\lim\limits_{n\rightarrow\infty}a_n\exists$$

思路：证明有界性和单调性

$$证：由题的a_{n+1}\geq1,即{a_n}有下界$$

$$a_{n+1}-a_n=\frac{1}{2}(\frac{1}{a_n}-a_n)\leqslant0\Rightarrow a_{n+1}\leqslant a_n即\{a_n\}\downarrow$$

$$\therefore\lim\limits_{n\rightarrow\infty}a_n\exists$$

例2🌰.$$\lim\limits_{n\rightarrow\infty}(\frac{1}{n^2+1}+\frac{2}{n^2+2}+...+\frac{n}{n^2+n})$$

思路：夹逼定理

$$解：令b_n=\frac{1}{n^2+1}+\frac{2}{n^2+2}+...+\frac{n}{n^2+n}$$

$$\frac{1}{2}\leqslant b_n \leqslant \frac{\frac{1}{2}n(n+1)}{n^2+1}$$

$$\because\lim\limits_{n\rightarrow\infty}左=\frac{1}{2},\lim\limits_{n\rightarrow\infty}右=\frac{1}{2}\lim\limits_{n\rightarrow\infty}\frac{1+\frac{1}{n}}{1+\frac{1}{n^2}}=\frac{1}{2}$$

$$\therefore原式=\frac{1}{2}$$

🌟不定型：$$\begin{cases}
\frac{0}{0}、1^{\infty} \\
\frac{\infty}{\infty}、0*\infty、\infty-\infty、... \\
\end{cases}$$

$$\frac{0}{0}型：\begin{cases}
u(x)^{v(x)}\Rightarrow e^{v(x)\ln u(x)} \\
\ln()\Rightarrow\ln(1+\Delta)\sim\Delta(\Delta\rightarrow0) \\
()-1\Rightarrow\begin{cases}
e^{\Delta}\sim\Delta \\
(1+\Delta)^a-1\sim a\Delta 
\end{cases}(\Delta\rightarrow0)
\end{cases}$$

例3🌰.$$\lim\limits_{x\rightarrow0}\frac{x\ln(1+2x)}{\sqrt{1-x^2}-1}$$

$$解：原式=\lim\limits_{x\rightarrow0}\frac{2x^2}{\frac{1}{2}(-x^2)}=-4$$

例4🌰.$$\lim\limits_{x\rightarrow0}\frac{(\frac{1+cosx}{2})^x-1}{x^3}$$

$$解：原式=\lim\limits_{x\rightarrow0}\frac{e^{x\ln\frac{1+cosx}{2}}-1}{x^3}$$

$$=\lim\limits_{x\rightarrow0}\frac{x\ln\frac{1+cosx}{2}}{x^3}$$

$$=\lim\limits_{x\rightarrow0}\frac{\ln(1+\frac{cosx-1}{2})}{x^2}$$

$$=\lim\limits_{x\rightarrow0}\frac{\frac{cosx-1}{2}}{x^2}$$

$$=-\frac{1}{4}$$

$$1^\infty型\begin{cases}
凑(1+\Delta)^{\frac{1}{\Delta}} \\
恒等变型
\end{cases}$$

例5🌰.$$\lim\limits_{x\rightarrow0}(e^x+sin2x)^{\frac{1}{x}}$$

$$解：\lim\limits_{x\rightarrow0}(e^x+sin2x)^{\frac{1}{x}}$$

$$=\lim\limits_{x\rightarrow0}\{[1+(e^x-1+sin2x)]^{\frac{1}{e^x-1+sin2x}}\}^{\frac{e^x-1+sin2x}{x}}$$

$$e^{\lim\limits_{x\rightarrow0}(\frac{e^x-1}{x}+\frac{sin2x}{x})}=e^3$$

例6🌰.$$\lim\limits_{x\rightarrow0}(\frac{1+tanx}{1+sinx})^{\frac{1}{x^3}}$$

$$解：原式=\lim\limits_{x\rightarrow0}[(1+\frac{tanx-sinx}{1+sinx})^{\frac{1+sinx}{tanx-sinx}}]^{\frac{tanx-sinx}{x^3(1+sinx)}}$$

$$=e^{\lim\limits_{x\rightarrow0}\frac{1}{1+sinx}*\frac{tanx-sinx}{x^3}}$$

$$=e^{\lim\limits_{x\rightarrow0}\frac{tanx}{x}*\frac{1-cosx}{x^2}}=e^{\frac{1}{2}}$$

$$0*\infty\begin{cases}
\frac{0}{\frac{1}{\infty}} 即\frac{0}{0} \\
\frac{\infty}{\frac{1}{0}} 即\frac{\infty}{\infty}
\end{cases}$$

例7🌰.$$\lim\limits_{x\rightarrow+\infty}x(\sqrt{x^2+4}-x)$$

$$解：原式=\lim\limits_{x\rightarrow+\infty}\frac{4x}{\sqrt{x^2+4}+x}$$

$$=4\lim\limits_{x\rightarrow+\infty}\frac{1}{\sqrt{1+\frac{4}{x^2}}+1}=2$$

$$\infty-\infty$$:

例8🌰.$$\lim\limits_{x\rightarrow1}(\frac{1}{x-1}-\frac{3}{x^3-1})$$

$$解：原式=\lim\limits_{x\rightarrow1}\frac{(x-1)(x+2)}{(x-1)(x^2+x+1)}$$

$$=\lim\limits_{x\rightarrow1}\frac{x+2}{x^2+x+1}=1$$

例9🌰.$$\lim\limits_{x\rightarrow+\infty}(\sqrt{x^2+4x+1}-x)$$

$$解：原式=\lim\limits_{x\rightarrow+\infty}\frac{4x+1}{\sqrt{x^2+4x+1}+x}$$

$$=\lim\limits_{x\rightarrow+\infty}\frac{4+\frac{1}{x}}{\sqrt{1+\frac{4}{x}+\frac{1}{x^2}}+1}=2$$

例10🌰.$$f(x)=\frac{x^2-x-2}{x^2-1}e^{\frac{1}{x}},求f(x)间断点。$$

$$解：x=0,x=\pm1为间断点$$

$$\lim\limits_{x\rightarrow -1}f(x)=\lim\limits_{x\rightarrow -1}\frac{x-2}{x-1} e^{\frac{1}{x}}=\frac{3}{2} e^{-1}$$

$$\lim\limits_{x\rightarrow1}f(x)=\infty$$

$$f(0^-)=0,f(0^+)=\infty$$

$$\therefore x=-1为可去间断点 x=1为第二类间断点 x=0为第二类间断点$$

例11🌰.$$\lim\limits_{x\rightarrow0}\frac{\sqrt{1+tanx}-\sqrt{1+sinx}}{x\sqrt{1+sin^2x}-x}$$

$$解:原式=\lim\limits_{x\rightarrow0}\frac{tanx-sinx}{x(\sqrt{1+sin^2x}-1)(\sqrt{1+tanx}+\sqrt{1+sinx})} \\
=\lim\limits_{x\rightarrow0}(\frac{sinx}{x}·\frac{secx-1}{\sqrt{1+sin^2x}-1}·\frac{1}{\sqrt{1+tanx}+\sqrt{1+sinx}})\\
=\lim\limits_{x\rightarrow0}(\frac{sinx}{x}·\frac{\sqrt{1+sin^2x}+1}{cosx}·\frac{1-cosx}{sin^2x}·\frac{1}{\sqrt{1+tanx}+\sqrt{1+sinx}})\\
=\frac{1}{2}$$

由例题11可以得出一个小总结，数值的代入必须是分子分母一起代入的，不能只代入一侧。

$$\infty-\infty\begin{cases}
(1)有分母，则通分 \\
(2)没有分母，创造分母再通分，令x=\frac{1}{t}
\end{cases}$$

例12🌰.(类型一)$$\lim\limits_{x\rightarrow0}(\frac{1}{sin^2x}-\frac{cos^2x}{x^2}) \\
=\lim\limits_{x\rightarrow0}\frac{x^2-sin^2xcos^2x}{x^4} \\
=\lim\limits_{x\rightarrow0}\frac{x^2-\frac{sin^22x}{4}}{x^4} \\
=\lim\limits_{x\rightarrow0}\frac{2x-\frac{1}{4}·2·2sin2x·cos2x·2}{4x^3} \\
=\lim\limits_{x\rightarrow0}\frac{2x-\frac{1}{2}sin4x}{4x^3} \\
=\lim\limits_{x\rightarrow0}\frac{2-2cos4x}{12x^2} \\
=\frac{4}{3}
$$

例13🌰.(类型二)$$\lim\limits_{x\rightarrow+\infty}[x^2(e^{\frac{1}{x}}-1)-x] \\
令x=\frac{1}{t} \\
=\lim\limits_{x\rightarrow+\infty}(\frac{e^t-1}{t^2}-\frac{1}{t}) \\
=\lim\limits_{x\rightarrow+\infty}\frac{e^t-1-t}{t^2} \\
e^x=1+x+\frac{x^2}{2}+o(x^2) \\
\Rightarrow e^x-1-x\sim\frac{1}{2}x^2 \\
=\frac{1}{2}$$



幂指函数：  
$$\infty^0,0^0,1^{\infty} \\
转化:u^v=e^{v\ln u}$$

$$1^{\infty}$$型

$$\lim u^v=e^{\lim v\ln u} \\
=e^{\lim v(u-1)}$$

🌰：  
1）$$
\lim\limits_{x\rightarrow0^+}(\frac{tanx}{x})^{\frac{1}{x^2}} \\
=e^{\lim\limits_{x\rightarrow0^+}\frac{1}{x^2}·(\frac{tanx}{x}-1)} \\
=e^{\frac{1}{3}}$$

2）$$\lim\limits_{x\rightarrow0}(\frac{e^x+e^{2x}+...+e^{nx}}{n})^{\frac{e}{x}} \\
=e^{\lim\limits_{x\rightarrow0}\frac{e}{x}(\frac{e^x+e^{2x}+...+e^{nx}}{n}-1)} \\
=e^{\frac{e}{n}\lim\limits_{x\rightarrow0}\frac{e^x-1}{x}+\frac{e^{2x}-1}{x}+...+\frac{e^{nx}-1}{x}} \\
=e^{\frac{e(1+n)}{2}}$$

$$0·\infty$$    
$$0·\infty可转化为\frac{0}{0}或\frac{\infty}{\infty}$$

但同时要注意分母要尽量简化。
$$\begin{cases}
简单：x^{\alpha},e^{\beta x} \\
复杂：\ln x,三角函数
\end{cases}$$
🌰：  
1）$$
\lim\limits_{x\rightarrow 0^+}x\ln x \\
=\lim\limits_{x\rightarrow 0^+}\frac{\ln x}{\frac{1}{x}} \\
=\lim\limits_{x\rightarrow 0^+}\frac{x^{-1}}{-x^{-2}}=0
$$

2）$$
\lim\limits_{x\rightarrow1^-}\ln x\ln(1-x) \\ 
\ln x\sim x-1,x\rightarrow1^- \\
令1-x=t \\
-\lim\limits_{t\rightarrow0^+}t\ln t=0
$$

