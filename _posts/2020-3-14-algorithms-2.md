---
layout: 		post
title: 			"算法"
subtitle: 		'分治啊分治'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 分治算法
> 分治的含义就是分而治之，将问题分成若干小块然后逐个解决。

分治法的三个条件：
1. 原问题可分解为若干个规模较小的相同子问题
2. 子问题相互独立
3. 子问题的解可以合并为原问题的解

分治法的使用方式：
1. 分解：将问题分解成若干个规模较小，相互独立，与原问题形式相同的子问题。
2. 治理：求解各个子问题。由于各个子问题与原问题形式相同，只是规模较小，可以用较为简单的方式解决。
3. 合并：按原问题的要求，将子问题的解逐层合并成原问题的解。

## 经典算法示例
#### 例1🌰.查找算法
有天小明👦要找书架上的一本书，他先走到了一个杂乱的书架找书。

```java
//小明从书架头找到书架尾
public int seqSearch(int[] a,int value) {
	for(int i=0;i<a.length;i++) {
		if(a[i] == value) {
			return i;
		}
	}
	return -1;
}
```

然后小明👦又去了另一个整齐的书架找，书按字母排好了顺序,他先从书架中间找，然后再去另一半的中间开始。

```java
//二分查找(非递归)
public int binarySearch_1(int[] a,int value) {
	int low = 0,high = a.length-1,mid;
	while(low != high-1) {
		mid = (low+high)/2;
		if(a[mid]<=value) {
			low = mid;
		}
		if(a[mid]>value) {
			high = mid;
		}
	}
	if(value == a[low]) {
		return low;
	}else if(value == a[high]) {
		return high;
	}
	return -1;
}
	
//二分查找(递归)
public int binarySearch_2(int[] a,int left,int right,int value) {
	int mid = (left+right)/2;
	int midval = a[mid];
	if(left>right) {
		return -1;
	}
		
	if(value>midval) {
		return binarySearch_2(a, mid+1, right, value);
	}else if(value< midval) {
		return binarySearch_2(a, left, mid-1, value);
	}else {
		return mid;
	}
}
	
//二分查找(递归)(多值查找)
public List<Integer> binarySearch_3(int[] a,int left,int right,int value) {
	int mid = (left+right)/2;
	int midval = a[mid];
	if(left > right) {
		return null;
	}
			
	if(value>midval) {
		binarySearch_3(a, mid+1, right, value);
	}else if(value< midval) {
		binarySearch_3(a, left, mid-1, value);
	}else{
		List<Integer> list = new ArrayList<>();
		int temp = mid-1;
		while(true) {
			if(temp<0 || a[temp] != value) {
				break;
			}
			list.add(temp);
			temp--;
		}
				
		list.add(mid);
				
		temp = mid+1;
		while(true) {
			if(temp>a.length-1 || a[temp] != value) {
				break;
			}
			list.add(temp);
			temp++;
		}
		return list;
	}
	return null;
}
```

然后小明👦发现上面两个方法都太麻烦，他想找一本B开头的书，讲道理他应该大概率在左侧。

```java
// 插入查找(递归)
//mid=low+(key-a[low])/(a[high]-a[low])*(high-low)
public int insertSearch(int[] a, int left, int right, int value) {
	if (left > right || a[a.length - 1] < value || a[0] > value) {
		return -1;
	}
	int mid = left + (right - left) * (a[right] - value) / (a[right] - a[left]);
	int midval = a[mid];
	if (value > midval) {
		return binarySearch_2(a, mid + 1, right, value);
	} else if (value < midval) {
		return binarySearch_2(a, left, mid - 1, value);
	} else {
		return mid;
	}
}
```

这时候小红👧出现了，她从书架的黄金分割点处开始找，然后再找另一边的黄金分割点。PS.斐波那契数列接近与黄金分割。


```java
//形成固定大小的斐波那契数列
public static int[] Fibonacci() {
	int[] f = new int[MAXSIZE];
	f[0] = 1;
	f[1] = 1;

	for (int i = 2; i < MAXSIZE; i++) {
		f[i] = f[i - 1] + f[i - 2];
	}
	return f;
}

public static int Fibonacci_Search(int[] a, int key) {
	int low, high, mid, len;

	low = 0;
	high = a.length - 1;
	len = a.length;

	int k = 0;
	int[] F = Fibonacci();

	// 查找临近的斐波那契数
	while (len > F[k] - 1) {
		k++;
	}

	// 创建临时数组
	int[] temp = new int[F[k] - 1];
	for (int i = 0; i < a.length; i++) {
		temp[i] = a[i];
	}

	// 补充不够的元素
	for (int i = len; i < F[k] - 1; i++) {
			temp[i] = temp[high];
	}

	// 判断
	while (low <= high) {
		mid = low + F[k - 1] - 1;

		if (key < temp[mid]) {
			high = mid - 1;
			k = k - 1;
		} else if (key > temp[mid]) {
			low = mid + 1;
			k = k - 2;
		} else {
			if (mid <= high) {
				return mid;
			} else
				return high;
		}
	}

	return -1;
}
```

总结：以上除了顺序查找都需要用到排序，如果数据分布均匀还是使用二分或者插值。斐波那契查找有点在于处理不均匀数据，较于上面二者不需要进行中间值的运算。

#### 例2🌰.排序算法
1、分治排序
```java
public static void mergeSort(int[] arr,int l,int r,int[] temp) {
	if(l < r) {
		int mid = (l+r)/2;
		//左递归进行分解
		mergeSort(arr,l,mid,temp);
		//右递归进行分解
		mergeSort(arr,mid+1,r,temp);
		//合并
		merge(arr,l, mid,r,temp);
	}
}
	
public static void merge(int[] arr,int l,int mid,int r,int[] temp) {
	int i=l;		//左序列初始索引
	int j=mid+1;	//右序列初始索引
	int t=0;        //指向temp数组的当前索引
		
	//将两个数组按规则合并
	while(i<=mid && j<=r) {
		if(arr[i]<=arr[j]) {
			temp[t] = arr[i];
			t++;
			i++;
		}else{
			temp[t] = arr[j];
			t++;
			j++;
		}
	}
		
	//在一边元素合并完，将另一边的剩余数据全部填充到temp
	while(i<=mid) {
		temp[t]=arr[i];
		t++;
		i++;
	}
		
	while(j<=r) {
		temp[t]=arr[j];
		t++;
		j++;
	}
		
	//将temp数组的元素拷贝到arr
	//并不是每次都拷贝所有
	t=0;
	int tempLeft = l;
	while(tempLeft <= r) {
		arr[tempLeft] = temp[t];
		t += 1;
		tempLeft += 1;
	}
}
```

分治排序的结构体系如下图：
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200314-mergeSort.png)

其原理就是利用二叉树结构进行分解，然后不断上升合并成一个新的有序集合。

2、快速排序
快速排序是基于分治策略的，其原理类似于分治排序，但是他的分解方法并非基于中间，而是借助于基准数划分两个子序列。

算法思想：
1. 分解：先从数列种取出一个元素作为基准元素，以大小为划分标准将数组分为两部分。
2. 对两个子序列进行快速排序(递归)
3. 合并将排好序的子序列合并

```java
public static void QuickSort(int a[], int s, int e){
	if (s < e){
		int i,j,x;
		i = s;
		j = e;
		x = a[i];
		while (i < j){
			while(i < j && a[j] > x)
				j--; // 从右向左找第一个小于x的数
			if(i < j)
				a[i++] = a[j];
 			while(i < j && a[i] < x)
				i++; // 从左向右找第一个大于x的数
			if(i < j)
				a[j--] = a[i];
		}
		a[i] = x;
		QuickSort(a, s, i-1); /* 递归调用 */
		QuickSort(a, i+1, e); /* 递归调用 */
	}
}
```

用按身高排队举个例子，先把队头的小明👦揪出来，这时候第一个位置是空缺的，我再从最后面开始找个比小明矮的塞到队头，如果找到了再换到队尾找，直到形成一个能依靠小明身高为基准划分的队伍。然后依次再对两队进行操作。

## 例题
#### 二分搜索变种  
例1🌰. leetcode35  
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
```java
public int searchInsert(int[] nums, int target) {
	int low = 0;
	int high = nums.length; 
	int mid;
	if(target<=nums[low]) {
		return 0;
	}
	while(low+1 < high) {
		mid = low + (high-low) / 2;
		if(target <= nums[mid]) 
			high = mid;
			
		if(target > nums[mid]) 
			low = mid;
			
	}
		
	return high;
}
```

例2🌰. leetcode74  
编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。
```java
public static boolean searchInsert(int[][] matrix, int target) {
	int rowNum = matrix.length;
	if (rowNum == 0) {
		return false;
	}
	int colNum = matrix[0].length;
	if (colNum == 0) {
		return false;
	}
	int l = 1;
	int h = colNum * rowNum;
	int mid;
	int row, col;
	while (l + 1 < h) {
		mid = l + (h - l) / 2;
		row = (mid - 1) / colNum;
		col = (mid - 1) % colNum;
		if (target == matrix[row][col]) {
			return true;
		}
		if (target < matrix[row][col]) {
			h = row * colNum + col + 1;
		}
		if (target > matrix[row][col]) {
			l = row * colNum + col + 1;
		}
	}

	if (target == matrix[(l - 1) / colNum][(l - 1) % colNum]
			|| target == matrix[(h - 1) / colNum][(h - 1) % colNum]) {
		return true;
	}
	return false;
}
```

例3🌰.  leetcode240    
编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

```java
public static boolean searchInsert(int[][] matrix, int target) {
	int row = matrix.length - 1;
	int col = 0;

	while (row >= 0 && col < matrix[0].length) {
		if (matrix[row][col] > target) {
			row--;
		} else if (matrix[row][col] < target) {
			col++;
		} else {
			return true;
		}
	}

	return false;
}
```

例4🌰.  leetcode153   
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。
```java
public int findMin(int[] nums) {
	int h = nums.length - 1;
	int l = 0;
	int mid;
	while (l + 1 < h) {
		mid = l + (h - l) / 2;
		if (nums[mid] >= nums[h]) 
			l = mid;
		
		if (nums[mid] < nums[h]) 
			h = mid;
		
	}
	return Integer.min(nums[l], nums[h]);
}
```