---
layout: 		post
title: 			"算法"
subtitle: 		'动态规划啊动态规划'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 动态规划
之前讲分治的时候提到过斐波那契数列，该数列的数学形式为：

$$F(n)=\begin{cases}
1 & n=1 \\
1 & n=2 \\
F(n-1)+F(n-2) & n>2
\end{cases}$$

在学编程初期讲到递归的时候，我们解决这类问题通常都是这样的👇：
```java
public static int Fibonacci(int n) {
	if(n==1||n==2) {
		return 1;
	}else {
		return Fibonacci(n-1)+Fibonacci(n-2);
	}
}
```

这种方法计算有个很致命的缺点👇：
![](/img/in-posts/20200315-tree.jpg)

可以明显的看到F(2)和F(1)的加和执行了三次，同时存在大量的结点重复。

#### 动态规划基础
> 动态规划也是一种分治思想，但是它会将子问题的结构进行存储，避免重复运算。

动态规划的两个条件：
1. 最优子结构
2. 子问题重叠

使用方式：
1. 分析最优解的结构特性
2. 建立最优值的递归式
3. 自底向上计算最优值并记录
4. 构造最优解

以斐波那契数列为例
1. 从n=3开始，F(n)的值为其前两项的加和,那么将F(n)看作一个最小子问题,那么求解F(n)包含了F(n-1)和F(n-2)两个子问题。
2. 建立递推式$$F(n)=\begin{cases}
1 & n=1 \\
1 & n=2 \\
F(n-1)+F(n-2) & n>2
\end{cases}$$
3. 自底而上计算最优值
![](/img/in-posts/20200315-tree-up.jpg)
4. 构造最优解

```java
public static int Fibonacci(int n) {
	if(n<1)
		return -1;
	int[] F = new int[n+1];
	F[1] = 1;
	F[2] = 1;
	for(int i=3;i<=n;i++)
		F[i] = F[i-1]+F[i-2];
	return F[n];
}
```

#### 例题
题目特点：
1. 计数
- 有多少种方式走到右下角
- 有多少种方法选出k个数使得和是Sum
2. 求最大最小值
- 从左上角走到右下角路径的最大数字和
- 最长上升子序列长度
3. 求存在性
- 取石子游戏
- 能不能选出k个数使得和是Sum

组成部分：  
一、确定状态  
- 动态规划首先要定义数组，数组是什么按题目设定。
- 两个意识：最后一步与子问题
二、转移方程
- f[x]=min{...}
三、初始条件与边界情况
根据转移方程判断，有一些需要手动定义的值与边界。

四、计算顺序
大部分从小到大。

例1🌰.找零钱(类型二)  
在贪心算法例二中提到过这么一个问题，如果宝物无法分割，就得不到最优的解法，只能得到近似解。现在小明👦就遇到了这样的问题。小明👦有足够多的2元，5元和7元纸币，而他需要买一包27块钱的板栗🌰。如何用最少的纸币数付清并不需要对方找钱？  
按之前的贪心策略，小明一定会先选7元，然后选5元，来达到纸币数量上的最优，然而按这个方法选出来的应该是三个7和一个5，离27还差1元。

按照组成部分分析： 
 
$$首先我们假设最优策略的纸币集合为\{a_1,a_2,...,a_k\}，这些纸币面值加起来为27$$

$$最后一张纸币为a_k$$

$$除去这张纸币的集合\{a_1,a_2,...,a_{k-1}\}加和为27-a_k$$

$$这时候的27-a_k就是一个规模更小的子问题$$

$$设状态f(x)=最少用多少张纸币拼出x$$

$$现在我们回到最初的时候，我们现在手上有2，5，7三种纸币可选$$

$$如果a_k为2，f(27)应该是f(27-2)+1$$

$$如果a_k为5，f(27)应该是f(27-5)+1$$

$$如果a_k为7，f(27)应该是f(27-7)+1$$

$$需要最少的硬币，所以转移方程为f(27)=min{f(27-2)+1,f(27-5)+1,f(27-7)+1}$$

$$对拼不出来的情况赋值为\infty,设置初始条件为f[0]=0$$


```java
public static int solution(int[] coins,int amount) {
	int[] f = new int[amount+1];
	int n = coins.length;
		
	f[0] = 0;
		
	int i,j;
		
	for(i=1;i<=amount;i++) {
		f[i] = Integer.MAX_VALUE;
		for(j=0;j<n;j++) {
			if(i>=coins[j] && f[i-coins[j]]!= Integer.MAX_VALUE) {
				f[i] = Math.min(f[i-coins[j]]+1,f[i]);
			}
		}
	}
		
	if(f[amount] == Integer.MAX_VALUE) {
		f[amount] = -1;
	}
		
	return f[amount];
}
```

例2🌰.有个(m,n)的表格，求左上角到右下角的路径种数。(类型一)
```java
public static int solution(int m,int n) {
	int[][] f = new int[m][n];
	int i,j;
	for(i=0;i<m;i++) {
		for(j=0;j<n;j++) {
			if(i==0 || j==0) {
				f[i][j]=1;
			}else {
				f[i][j] = f[i-1][j]+f[i][j-1];
			}
		}
	}
	return f[m-1][n-1];
}
```

例3🌰.有n块石头分别在x轴的0,1,...,n-1的位置，青蛙在石头0，想跳到石头n-1。如果跳到第i块石头，它最多可往右跳距离$$a_i$$,判断青蛙是否能跳到石头n-1。(类型三)
```java
public static boolean solution(int[] A) {
	int n = A.length;
	boolean[]f = new boolean[n];
	f[0] = true;
		
	for(int j=1;j<n;j++) {
		f[j]=false;
		//遍历前面的石子
		for(int i=0;i<j;i++) {
			//看前面的石子是不是之前能走，而且在该石子的跳跃距离足够
			if(f[i] && i+A[i]>=j) {
				f[j] = true;
				break;
			}
		}
	}
		
	return f[n-1];
}
```
另一种解法：  
上面那题用动态规划做效率并没有贪心高，动态规划的时间复杂度为$$O(n^2)$$，而贪心算法能做到O(n)。
```java
public static boolean solution(int[] A) {
	int n = A.length;
	int max=0;//能达到的极限点位
	
	//进行一次遍历	
	for(int i=0;i<n;i++) {
		//如果是能达到的点，判断此点是否能跳得更远
		if(max>=i) {
			max=max<=i+A[i]?i+A[i]:max;
		}
	}
	//如果没够到指定点位，就说明无效
	if(max<n-1) {
		return false;
	}
	return true;
}
```

例4🌰.0-1背包问题(类型二)   
之前在贪心算法那边讲过宝物不可分割的问题，现在就对那题做一个不可分割的优化。  
我们有如下几个物品：  
<table>
	<tr>
		<td>i</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
	</tr>
	<tr>
		<td>w(体积)</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
	</tr>
	<tr>
		<td>v(价值)</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
		<td>6</td>
	</tr>

</table>

首先假设在载重内的最大价值为$$\{v_1w_1,v_2w_2,...,v_kw_k\}$$，这时候我们就有了一个状态量$$e\in(0，1)$$来表示宝物是否装入，由此可得不等式{e_1w_1,e_2w_2,...,e_kw_k}<capacity。  
设状态f(x)=最大价值，则$$f(x)=max\{f(x-w_k)+v_k,f(x-w_k)\}$$  
我们根据不等式和状态可以将问题划分成k*capacity个子问题，然后画出这样的一个表格：
<table>
	<tr>
		<td>物品i\载重capacity</td>
		<td>1</td>
		<td>2</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
		<td>6</td>
		<td>7</td>
		<td>8</td>
	</tr>
	<tr>
		<td>1</td>
		<td>0</td>
		<td>3</td>
		<td>3</td>
		<td>3</td>
		<td>3</td>
		<td>3</td>
		<td>3</td>
		<td>3</td>
	</tr>
	<tr>
		<td>2</td>
		<td>0</td>
		<td>3</td>
		<td>4</td>
		<td>4</td>
		<td>7</td>
		<td>7</td>
		<td>7</td>
		<td>7</td>
	</tr>
	<tr>
		<td>3</td>
		<td>0</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
		<td>7</td>
		<td>8</td>
		<td>9</td>
		<td>9</td>
	</tr>
	<tr>
		<td>4</td>
		<td>0</td>
		<td>3</td>
		<td>4</td>
		<td>5</td>
		<td>7</td>
		<td>8</td>
		<td>9</td>
		<td>10</td>
	</tr>

</table>

```java
public static int FindMax(int w[], int[] v, int capacity) {
	int number = w.length;
	int[][] V = new int[number + 1][capacity + 1];
	int i, j;
	// 填表
	for (i = 1; i <= number; i++) {
		for (j = 1; j <= capacity; j++) {
			if (j < w[i - 1]) {// 包装不进
				V[i][j] = V[i - 1][j];
			} else {// 能装
				if (V[i - 1][j] > V[i - 1][j - w[i - 1]] + v[i - 1]) {// 不装价值大
					V[i][j] = V[i - 1][j];
				} else {// 前i-1个物品的最优解与第i个物品的价值之和更大
					V[i][j] = V[i - 1][j - w[i - 1]] + v[i - 1];
				}
			}
		}
	}
	return V[number][capacity];
}
```