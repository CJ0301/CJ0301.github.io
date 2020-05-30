---
layout: 		post
title: 			"算法"
subtitle: 		'回溯啊回溯'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---
> 回溯法是一种深度优先搜索的方法，发现结点不满足条件时就回溯，尝试其他路径。

## 回溯法
#### 算法要素
1）解空间  
- 解的组织形式：回溯法解的组织形式可以规范为一个n元组$$\{x_1,x_2,...,x_n\}$$。  
- 显约束：对解分量的取值范围的限定。  
例如三个物体的0-1背包问题，可能解为八种：{0,0,0},{0,0,1},{0,1,0},{1,0,0},{0,1,1},{1,0,1},{1,1,0},{1,1,1}  
- 解空间：所有解组成的二维空间，解空间越小，搜索效率越高。  

2）解空间的组织结构
解空间搜索最优解可以用其他组织形式表现，如上面的背包问题可以用树的形式表现。

3）搜索解空间
隐约束指能否得到问题的可行解或最优解做出的约束。  
如果不满足隐约束，就说明得不到问题的可行解或最优解，这时候就需要剪枝。因此，隐约束也称剪枝函数，即停止搜索该分支。  
如背包问题的超重，即可直接剪枝。

隐约束(剪枝函数)包括约束函数与限界函数。
对得到可行解的约束交约束函数，对得到最优解的约束称为限界约束。

解空间的大小和剪枝函数的好坏都直接影响搜索效率。

#### 解题思路
1)定义解空间  
- 解的组织形式
- 显约束

2)确定组织结构
根据解空间树不同，解空间分为子集树、排列树、m叉树等。

3)搜索解空间
根据需求设定隐约束，要求可行解只要设定约束函数，要求最优解则需要约束函数和限定函数。

#### 例题
例1🌰.全排列问题
全排列问题就是一个简单的选择问题，同时对已经存在的元素进行剪枝。
```java
public static List<List<Integer>> res = new LinkedList<>();

/* 主函数，输入一组不重复的数字，返回它们的全排列 */
public static List<List<Integer>> permute(int[] nums) {
	// 记录「路径」
	LinkedList<Integer> track = new LinkedList<>();
	backtrack(nums, track);
	return res;
}

// 路径：记录在 track 中
// 选择列表：nums 中不存在于 track 的那些元素
// 结束条件：nums 中的元素全都在 track 中出现
public static void backtrack(int[] nums, LinkedList<Integer> track) {
	// 触发结束条件
	if (track.size() == nums.length) {
		res.add(new LinkedList(track));
		return;
	}	

	for (int i = 0; i < nums.length; i++) {
		// 排除不合法的选择
		if (track.contains(nums[i]))
			continue;
		// 做选择
		track.add(nums[i]);
		// 进入下一层决策树
		backtrack(nums, track);
		// 取消选择
		track.removeLast();
	}
}

```

例2🌰.0-1背包问题

```java
public class Solution {

    public int[] weight;
    public int[] value;
    public int[] take;

    int curWeight = 0;
    int curValue = 0;

    int bestValue = 0;
    int[] bestChoice;
    int count;

    int maxWeight = 0;

    public static void main(String[] args) {
        Solution solution = new Solution();
        solution.init(new int[]{3,4,5,6},new int[]{2,3,4,5},8);
        int[] result = solution.maxValue(0);
        for(int r:result){
            System.out.println(r+" ");
        }
        System.out.println("最大价值为"+solution.bestValue);

    }

    public void init(int[] value,int[] weight,int maxWeight){
        this.value = value;
        this.weight = weight;
        this.maxWeight = maxWeight;
        count = value.length;
        take = new int[count];
        bestChoice = new int[count];
    }

    public int[] maxValue(int x) {
        //走到了叶子节点
        if (x > count - 1) {
            //更新最优解
            if (curValue > bestValue) {
                bestValue = curValue;
                for (int i = 0; i < take.length; i++) {
                    bestChoice[i] = take[i];
                }
            }
        } else {
            //遍历当前节点（物品）的子节点：0 不放入背包 1：放入背包
            for (int i = 0; i < 2; i++) {
                take[x] = i;
                if (i == 0) {
                    //不放入背包，接着往下走
                    maxValue(x + 1);
                } else {
                    //约束条件，如果小于背包容量
                    if (curWeight + weight[x] <= maxWeight) {
                        //更新当前重量和价值
                        curWeight += weight[x];
                        curValue += value[x];
                        //继续向下深入
                        maxValue(x + 1);
                        //回溯法重要步骤，个人感觉也是精华所在。
                        // 当从上一行代码maxValue出来后，需要回溯容量和值
                        curWeight -= weight[x];
                        curValue -= value[x];
                    }
                }
            }
        }
        return bestChoice;
    }

}
```