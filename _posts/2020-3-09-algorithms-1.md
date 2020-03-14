---
layout: 		post
title: 			"算法"
subtitle: 		'贪心啊贪心'
author: 		"CJ"
header-img: 	"img/post-bg-fblog.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 贪心算法
> 一个贪心算法总是做出当前最好的选择，也就是说，它期望通过局部最优选择从而得到全局最优的解决方案。
&nbsp;&nbsp;&nbsp;——《算法导论》

贪心算法的三个注意点：
1. 做出选择不可以反悔
2. 得到的不是最优解，而是最优解的近似解
3. 选择什么样的贪心策略，直接决定算法的好坏

贪心算法的特性
1. 贪心选择：指原问题的整体最优解可以通过一系列局部最优的选择得到。
2. 最优子结构：指一个问题的最优解包含其子问题的最优解。

贪心算法的使用方式
1. 贪心策略：选择当前的最优方案。例如菜场买一个🍎，人们往往会挑选品质最优的🍎。
2. 局部最优解：一步一步得到局部最优解。再例如菜场买一斤🍎，挑选品质最好的🍎，然后挑选次好的，以此类推，直到🍎到一斤。
3. 全局最优解：把所有最优解合成位原来问题的最优解。最优解也就是上面挑出来的一斤🍎了。

稍微有点编程基础的也可以参考初识循环语句学习的冒泡排序，就是采用的贪心算法的思想。

## 例题
例1🌰.$$一艘海盗船🏴‍☠️的装载量为C，一次抢劫中，他们得到了若干件古董，每件古董的重量为w_i，带走的古董件数为n，海盗如何将尽可能多的古董装上船？$$

算法设计：
1. 载重C为固定值时，w_i越小，可装载的古董数量n越大。
2. 把所有古董进行从小到大排序，然后尽可能的选出前n件古董即可达到最优。

```java
public class Test {
	private static final int C = 30; 
	public static void main(String[] args) {
		int[] sortedArr = {2,3,4,6,7,9,10,11,15};
		System.out.println(Solution(sortedArr));
	}

	public static int Solution(int[] arr) {
		int res = C;
		int n = 0;
		for(int i:arr) {
			res-=i;
			if(res<0) {
				return n;
			}
			n++;
		}
		return 0;
	}
}
```
例2🌰.$$山洞中有n种宝物，每种宝物有一定的重量w和相应的价值v，毛驴的运载能力为m,一种宝物只能拿一样，宝物可以分割。如何使毛驴运走最多价值的宝物？$$

思路：选择性价比最高的宝物，最后分割拿的最后一样宝物。

```java
package com.zte.practice;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.Scanner;

public class Test {
	public static void main(String[] args) {
		List<Resource> resources = new ArrayList<>();
		Scanner s = new Scanner(System.in);
		int numOfRes = s.nextInt();
		float tWeight = s.nextInt();
		for(int i=0;i<numOfRes;i++) {
			resources.add(new Resource(s.nextFloat(), s.nextFloat()));
		}
		
		resources.sort(new Comparator<Resource>() {
			@Override
			public int compare(Resource o1, Resource o2) {
				return o1.getPerCost()-o2.getPerCost()<0?1:-1;
			}	
		});
		
		CaculateRes(resources,tWeight);
	}
	
	public static void CaculateRes(List<Resource> res,float tWeight){
		float cWeight,cPerValue,tValue = 0;
		for(Resource r:res) {
			cWeight = r.getWeight();
			cPerValue = r.getPerCost();
			if(tWeight>cWeight) {
				System.out.println("拿单位价值"+cPerValue+"的宝物,重量为"+cWeight);
				tWeight -= cWeight;
				tValue += r.getValue();
			}else {
				System.out.println("拿单位价值"+cPerValue+"的宝物,重量为"+tWeight);
				tValue += cPerValue*tWeight; 
				break;
			}
		}
		System.out.println("总价值"+tValue);
	}
}

class Resource{
	private float weight;  //重量
	private float value;   //价值
	private float perCost; //性价比
	public Resource(float weight, float value) {
		super();
		this.weight = weight;
		this.value = value;
		this.perCost = value/weight;
	}
	
	public float getPerCost() {
		return perCost;
	}
	
	public float getWeight() {
		return weight;
	}
	
	public float getValue() {
		return value;
	}
	
}
```
