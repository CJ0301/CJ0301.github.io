---
layout: 		post
title: 			"算法"
subtitle: 		'数组'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---
## 洗牌算法

方法一：
```java
public static void shuffle_1(int[] cards){
	Random r = new Random();
        int m,n,temp;
        for(int i=0;i<cards.length;i++){
            m = r.nextInt(cards.length-1);
            n = r.nextInt(cards.length-1);
            temp = cards[m];
            cards[m] = cards[n];
            cards[n] = temp;
	}
}
```

方法二：
```java
public static void shuffle_2(int[] cards){
	Random r = new Random();
	int n,temp;
	for(int i=0;i<cards.length;i++){
		n = r.nextInt(cards.length-1);
		temp = cards[i];
		cards[i] = cards[n];
		cards[n] = temp;
	}
}
```

方法三：
```java
public static void shuffle_3(int[] cards){
	Random r = new Random();
	int n,temp,length = cards.length;
	for(int i=0;i<cards.length;i++){
		n = i + r.nextInt(length-i);
		temp = cards[i];
		cards[i] = cards[n];
		cards[n] = temp;
	}
}
```

方法三有效性的证明：  
选第一张牌的概率是1/n  
选第二张牌的概率为第一次未被选中概率和第二次被选中的概率之积，概率也等于1/n

验证算法
```java
final static long TEST_NUM = 100000000;
public static void main(String[] args) {
	int[] cards = {0,1,2,3,4,5,6};
	int[][] result = new int[cards.length][cards.length];
	for(long i=0;i<TEST_NUM;i++){
		int[] tempArray = cards;
		shuffle_2(tempArray);
		for(int j=0;j<tempArray.length;j++)
			result[tempArray[j]][j] += 1;
		
	}
	for(int[] array:result){
		for(int i=0;i<array.length;i++)
			System.out.print(array[i]+"  ");
		
		System.out.println();
	}
}
```

## 寻找质数
求n以内的质数个数
方法一：  
判断2~n内的奇数  
```java
public static int prime_1(int n){
	int num=0;
	boolean sign;
	for(int i=2;i<n;i++){
		if(i % 2 == 0 && i != 2  )  continue; //偶数和1排除
		sign=true;
		for (int j=2;j<i;j++){
			if(i%j==0){
				sign=false;
				break;
			}
		}
		if (sign)
			num++;
            
	}
	return num;
}
```

方法二：  
判断2~$\sqrt{n}$内的奇数  
```java
public static int prime_2(int n){
	int num=0;
	int j;
	boolean sgin;
	for (int i = 2; i <= n; i++) {
		if(i % 2 == 0 && i != 2  )  continue; //偶数和1排除

		sgin= true;
		for (j = 2; j <= Math.sqrt(i) ; j++) {
			if (i % j == 0) {
				sgin = false;
				break;
			}
		}

		//打印
		if (sgin) 
			num++;
		
	}
	return num;
}
```

方法三：  
牺牲空间复杂度换取时间复杂度
```java
public static int prime_3(int n){
	//素数总和
	int sum = 0;
	//1000万以内的所有素数
	//用数组将1000万以内的数分为两大派系，素数用0代替数值，合数用1代替数值；
	//一开始默认全部为素数，所以值全部为0，等到开始筛选的时候再把为合数的赋值为1
	int num[] = new int[n];
	num[0] = 1;          //由于1规定不是素数，所以要提前用1标值
	//根据埃氏筛法的结论，要得到自然数  N 以内的全部素数，必须把不大于" 二次根号  N "的所有素数的倍数剔除，剩下的就是素数
	double prescription = Math.sqrt(n);
		for (int i = 2; i <= prescription; i++) {
		//开始把所有素数的倍数剔除，剩下的就是素数
			for (int j = i*i; j <= n; j+=i) {
			//从i*i开始去除，因为比i*i小的倍数，已经在前面去除过了
			//例如：i=5
			//5的2倍（10），3倍（15），在i=2的时候，已经去除过了

			num[j-1] = 1;   //把素数的倍数剔除，也就是赋值为1，不是素数就是合数
		}
	}
	//遍历数组，把值为0的数全部统计出来，得到素数之和
	for (int i = 0; i < num.length; i++) {
		if(num[i]==0)
			sum++;
	}
	return sum;
}
```

## 哥德巴赫猜想
```java
public static void goldBach(int n){
	boolean[] is_prime = new boolean[n+1];
	Arrays.fill(is_prime,true);
	int j,count=0,i = 2;
	while (i*i<=n){
		if(is_prime[i]){
			j = i;
			while (i*j<= n){
				is_prime[i*j] = false;
				j++;
			}
		}
		i++;
	}

	for(int m = 2;m<n+1;m++)
		if(is_prime[m])
			count++;

	int idx = 0;
	int[] primes = new int[count];
	for(int m = 2;m<n+1;m++){
		if(is_prime[m]){
		primes[idx] = m;
			idx++;
		}
	}

	int left=0,right = count-1;
	while (left<right){
		if(n == primes[left]+primes[right]){
			System.out.println(n+" = "+primes[left] + " + " +primes[right]);
			left++;
			right--;
		}else if(n>primes[left]+primes[right]){
			left++;
		}else{
			right--;
		}
	}
}
```