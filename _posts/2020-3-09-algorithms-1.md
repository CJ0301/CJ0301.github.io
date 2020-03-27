---
layout: 		post
title: 			"算法"
subtitle: 		'贪心啊贪心'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
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

## 经典算法示例
例1🌰.Dijkstra算法(单源求最短路径)
思想：
1. 初始化：$$先找出源点V_0到各终点的直达路径(V_0,V_k)，即不经过其他源点。$$
2. 选择：$$从中选出一条最短路径(V_0,u)$$。
3. 更新：$$对其余各路径进行适当调整，若存在(u,V_k)，且(V_0,u)+(u,V_k)<(V_0,V_k),则以路径(V_0,u,V_k)代替(V_0,V_k)$$
4. 在调整后的各路径中再找长度最短的，依次类推。

步骤：$$初始化S={v_0},T={其余顶点}，D={对应的距离值}。(D[i]初始值，若<v_0,v_i>存在，则为权值，否则为\infty)$$

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200318-graph.png)
```java
public class Test {
	private static int mEdgNum;        // 边的数量
    private static char[] mVexs;       // 顶点集合
    private static int[][] mMatrix;    // 邻接矩阵
    private static final int INF = Integer.MAX_VALUE;   // 最大值
    public static void main(String[] args) {
    	char[] vexs = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        int matrix[][] = {
                 /*A*//*B*//*C*//*D*//*E*//*F*//*G*/
          /*A*/ {   0,  13,   8, INF, 30,  INF,  32},
          /*B*/ {  13,   0, INF, INF, INF,   9,   7},
          /*C*/ {   8, INF,   0,   5, INF, INF, INF},
          /*D*/ { INF, INF,   5,   0,   6, INF, INF},
          /*E*/ {  30, INF, INF,   6,   0,   2, INF},
          /*F*/ { INF,   9, INF, INF,   2,   0,  17},
          /*G*/ {  32,   7, INF, INF, INF,  17,   0}};
        createGraph(vexs, matrix);
        int[] prev = new int[mVexs.length];
        int[] dist = new int[mVexs.length];
        dijkstra(0, prev, dist);
	}
    
    /*
     * 创建图(用已提供的矩阵)
     *
     * 参数说明：
     *     vexs  -- 顶点数组
     *     matrix-- 矩阵(数据)
     */
    public static void createGraph(char[] vexs, int[][] matrix) {
        
        // 初始化"顶点数"和"边数"
        int vlen = vexs.length;

        // 初始化"顶点"
        mVexs = new char[vlen];
        for (int i = 0; i < mVexs.length; i++)
            mVexs[i] = vexs[i];

        // 初始化"边"
        mMatrix = new int[vlen][vlen];
        for (int i = 0; i < vlen; i++)
            for (int j = 0; j < vlen; j++)
                mMatrix[i][j] = matrix[i][j];

        // 统计"边"
        mEdgNum = 0;
        for (int i = 0; i < vlen; i++)
            for (int j = i+1; j < vlen; j++)
                if (mMatrix[i][j]!=INF)
                    mEdgNum++;
    }

    
    /*
     * Dijkstra最短路径。
     * 即，统计图中"顶点vs"到其它各个顶点的最短路径。
     *
     * 参数说明：
     *       vs -- 起始顶点(start vertex)。即计算"顶点vs"到其它顶点的最短路径。
     *     prev -- 前驱顶点数组。即，prev[i]的值是"顶点vs"到"顶点i"的最短路径所经历的全部顶点中，位于"顶点i"之前的那个顶点。
     *     dist -- 长度数组。即，dist[i]是"顶点vs"到"顶点i"的最短路径的长度。
     */
    public static void dijkstra(int vs, int[] prev, int[] dist) {
        // flag[i]=true表示"顶点vs"到"顶点i"的最短路径已成功获取
        boolean[] flag = new boolean[mVexs.length];

        // 初始化
        for (int i = 0; i < mVexs.length; i++) {
            flag[i] = false;          // 顶点i的最短路径还没获取到。
            prev[i] = 0;              // 顶点i的前驱顶点为0。
            dist[i] = mMatrix[vs][i];  // 顶点i的最短路径为"顶点vs"到"顶点i"的权。
        }

        // 对"顶点vs"自身进行初始化
        flag[vs] = true;
        dist[vs] = 0;

        // 遍历mVexs.length-1次；每次找出一个顶点的最短路径。
        int k=0;
        for (int i = 1; i < mVexs.length; i++) {
            // 寻找当前最小的路径；
            // 即，在未获取最短路径的顶点中，找到离vs最近的顶点(k)。
            int min = INF;
            for (int j = 0; j < mVexs.length; j++) {
                if (flag[j]==false && dist[j]<min) {
                    min = dist[j];
                    k = j;
                }
            }
            // 标记"顶点k"为已经获取到最短路径
            flag[k] = true;

            // 修正当前最短路径和前驱顶点
            // 即，当已经"顶点k的最短路径"之后，更新"未获取最短路径的顶点的最短路径和前驱顶点"。
            for (int j = 0; j < mVexs.length; j++) {
                int tmp = (mMatrix[k][j]==INF ? INF : (min + mMatrix[k][j]));
                if (flag[j]==false && (tmp<dist[j]) ) {
                    dist[j] = tmp;
                    prev[j] = k;
                }
            }
        }

        // 打印dijkstra最短路径的结果
        System.out.printf("dijkstra(%c): \n", mVexs[vs]);
        for (int i=0; i < mVexs.length; i++)
            System.out.printf("  shortest(%c, %c)=%d\n", mVexs[vs], mVexs[i], dist[i]);
    }

}
```

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

算法复杂度分析：
这里懒就没有用上排序了，方法里是对宝物进行了一次遍历，所以这个算法的时间复杂度是`O(n+排序算法复杂度)`，同时辅助空间没有参与循环等操作，所以空间复杂度为`O(1)`。

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
算法复杂度分析：时间复杂度与上题一样，因为只是遍历一次，所以算法的时间复杂度是`O(n+排序算法复杂度)`，这里用了list去存储性价比，所以空间复杂度为`O(n)`。

💡思考：如果宝物不可分割，会发生什么呢？
我有如下三件宝物：
<table>
<tr>
	<td>物品i</td>
	<td>1</td>
	<td>2</td>
	<td>3</td>
</tr>
<tr>
	<td>重量w[i]</td>
	<td>3</td>
	<td>4</td>
	<td>6</td>
</tr>
<tr>
	<td>价值v[i]</td>
	<td>15</td>
	<td>16</td>
	<td>18</td>
</tr>
<tr>
	<td>性价比p[i]</td>
	<td>5</td>
	<td>4</td>
	<td>3</td>
</tr>
</table>

同时我有10的载重量。如果无法分割，明显选23比选13的结果要好，这时按上面的算法选出的13就是最优解的近似解。  
可分割的装载问题我们称为`背包问题`，不可分割的我们称为`0-1背包问题`，不具备贪心选择性质，只有不要求得到最优解的情况下可以使用。如果要求`0-1背包问题`最优解，最好使用动态规划。