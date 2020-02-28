---
layout: 		post
title: 			"Markdown语法整理"
subtitle: 		"为了以后自己能养好更新博客的好习惯，还是先把Markdown语法重新学习一下比较好"
author: 		"CJ"
header-img: 	"img/post-bg-test.jpg"
header-mask: 	0.3
catalog: 		true
mathjax: 		true
tags:
  - BlogBuild
---

> [Markdown](https://zh.wikipedia.org/wiki/Markdown)是一款轻量级的标记语言，他使得人们能够用易读易写的纯文本格式编写文档，然后转换成有效的XHTML（或者HTML）文档

### 1、标题
# 一级标题  
## 二级标题  
### 三级标题  
#### 四级标题  
##### 五级标题  
###### 六级标题  

## 2、列表
### 无序列表

* 1
* 2
* 3 

### 有序列表

1. 1
2. 2
3. 3

## 3、引用格式
引用文字：`>+空格`（后面内容一定要另起一行）
引用图片：`![]()`
引用链接：`[]()`
> 此处放引用的内容

![Hero](/img/hero.png)
[友情链接](www.cjcjcj.top)


## 4、文字样式
*斜体*
**粗体**
***斜粗体***


## 5、代码区块
	 public static int[] add(int[] arr,int target) {
             Map<Integer,Integer> nums = new HashMap<>();
             for(int i=0;i<arr.length;i++) {
                    if(nums.containsKey(target-arr[i])) {
                           return new int[] {nums.get(target-arr[i]),i};
                    }
                    nums.put(arr[i], i);
             }
             return new int[] {};
       }
       
       public static void main(String[] args) {
             int[] numbers = new int[]{2,7,9,11};
             int[] arr = add(numbers,16);
             for(int i:arr) {
                    System.out.println(i+"");
             }
       }


```
public static int[] add(int[] arr,int target) {
             Map<Integer,Integer> nums = new HashMap<>();
             for(int i=0;i<arr.length;i++) {
                    if(nums.containsKey(target-arr[i])) {
                           return new int[] {nums.get(target-arr[i]),i};
                    }
                    nums.put(arr[i], i);
             }
             return new int[] {};
       }
       
       public static void main(String[] args) {
             int[] numbers = new int[]{2,7,9,11};
             int[] arr = add(numbers,16);
             for(int i:arr) {
                    System.out.println(i+"");
             }
       }

```

## 6、分割线
---

## 7、注释
某专业名词<sup>[1](#ref1)</sup>

<a id="ref1">[注释内容]

## 8、表格
`-`左对齐 `:-:`中对齐 `-:`右对齐

| N/A      | 简单体验（页面）  | 中等体验（mini-app） | 核心体验（app） |
| :--------: | :--------: | :--------: | :--------: |
| 纯微信流 | 公众号 小程序     | 小程序               | 我想要个原生啊  |
| 创业公司 | 公众号 Web 小程序 | Web 小程序           | 拉回原生啊      |
| 中大公司 | 公众号 Web 小程序 | Web 小程序           | 拉回原生啊      |
| 巨头公司 | 公众号 Web        | 不跟微信玩           | 不跟微信玩      |

## 视频嵌入
<iframe src="//player.bilibili.com/player.html?aid=75978628&amp;cid=129963854&amp;page=1" width="700px" height="500px" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

## 音乐嵌入
<p>http://q6ba0cez9.bkt.clouddn.com/离开你的城市后.mp3</p>
