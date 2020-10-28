---
layout: 		post
title: 			"算法"
subtitle: 		'排序算法的整理'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---
## 冒泡排序与选择排序
冒泡顾名思义就是通过一轮一轮的对比保证把最大的数都放到最后(从小往大排序)。
```java
/*
* 冒泡排序
*
* 原理：第一层循环负责控制已排序好的数组部分的移动量
*      第二层循环控制移动每次交换的下标
*      通过下标的移动达到将最大(最小)值移动到最右端，然后通过第一层循环将最大下标向左移。
* */
public static void bubble(int[] nums) {
             
	int temp;
	for(int i=0;i<nums.length;i++) {
		for(int j=0;j<nums.length-i-1;j++) {
			if(nums[j]>nums[j+1]) {
				temp = nums[j];
				nums[j] = nums[j+1];
				nums[j+1] = temp;
			}
		}
		System.out.print("第"+i+"次排序:        ");
		out(nums);
	}
	System.out.print("Final result:         ");
	out(nums);
	System.out.println();
}
```

选择排序就是冒泡排序的反向过程，将最小的数选择到前面(从小到大排序)
```java
/*
* 选择排序
*
* 原理：选择最大值(或最小值)放在前面
* */
public static void selection(int[] nums) {
             
	int flag;
	int temp;
	for(int i=0;i<nums.length-1;i++) {
		flag = i;
		for(int j=i+1;j<nums.length;j++) {
			flag = nums[j]<nums[flag]?j:flag;
		}
		temp = nums[i];
		nums[i] = nums[flag];
		nums[flag] = temp;
                    
		System.out.print("第"+i+"次排序:        ");
                    out(nums);
		}
             
		System.out.print("Final result:         ");
		out(nums);
		System.out.println();
}
```

## 插入排序
插入排序的原理就和抽扑克一样，每次手里的牌都是有序的，将抽入的牌放入合适的位置即可。  
由于找到位置后会提前终止，所以效率会高于冒泡与选择。
```java
 /*
* 插入排序
*
* 原理：(1)取出无序区中的第1个数，并找出它在有序区对应的位置。(2)将无序区的数据插入到有序区；若有必要的话，则对有序区中的相关数据进行移位。
*
* 总结：从下标1开始遍历，遍历过后前面部分的元素一定是有序区
*           for(循环下标1之后的元素){
*                  for(查找之前所有元素){
*                         if(查找到之前的元素比他大（小）){
*                               通过跳出记录最远下标
*                         }
*                  }
*                  if(查找到的下标就是i-1){
*                         元素后移
*                  }
*           }
* */
public static void insertion(int[] nums) {
             
	int i, j, k;
	int n = nums.length;
	for (i = 1; i < n; i++){
		//将a[i]与之前元素做对比，找到相应位置记录
		for (j = i - 1; j >= 0; j--)
			if (nums[j] < nums[i])
				break;
			//找到的位置并非前一个位置(在前一个位置说明全部有序)
			if (j != i - 1){
				//将比a[i]大的数据向后移
				int temp = nums[i];
				for (k = i - 1; k > j; k--)
					nums[k + 1] = nums[k];
				//将a[i]放到正确位置上
				nums[k + 1] = temp;
			}
			System.out.print("第"+i+"次排序:        ");
			out(nums);
	}
             
	System.out.print("Final result:            ");
	out(nums);
	System.out.println();
             
}
```