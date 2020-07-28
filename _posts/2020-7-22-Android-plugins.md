---
layout: 		post
title: 			"Android的一些代码插件"
subtitle: 		'比赛要用，其实对这些插件不是很感兴趣'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## LayoutCreator
可以让你在Activity/Fragment中自动生成findViewById等布局相关初始化代码
或者在Adapter中自动生成ViewHolder代码

好处就是：  
1. 节约时间  
2. 命名更容易统一  

生成规则：  
- 自动实现findViewById方法：目标布局中所有包含id属性的控件  
- 自动实现OnClickListener接口：目标布局中所有clickable属性为true的控件  
- 自动识别include标签， 读取对应布局中的控件  

使用：  
1. 选中代码中setContentView中的布局文件名称部分  
2. 选中Code-LayoutCreator
3. 选择自动生成的控件与命名格式  

注意：
1. xml定义控件id时，使用`控件简称+_+功能叙述`的命名方式。

![原作链接](https://github.com/boredream/BorePlugin)

## GsonFormat
根据Json数据生成Java对象

使用：  
1. alt+s弹出输入框  
2. 复制一段json数据

![原作链接](https://github.com/zzz40500/GsonFormat)
