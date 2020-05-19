---
layout: 		post
title: 			"JavaScript基础"
subtitle: 		'数据类型'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - JavaScript
---
> 为某个猪猪更新的js基础，顺便自己也整理一下，有些东西快忘了。

## 数字
#### 整数
js里整数能直接表示的有十进制整数与十六进制整数，某些条件下能用八进制(最好不要用，ECMAScript不支持)。

#### 浮点型
有两种写法：  
1. 常规数学写法，如果整数部分是0，则0可省略。  
2. 科学计数法，形如1.452E-32(e大小写都可)。

#### 运算
正常运算有`+` 、`-`、 `*`、 `/`、 `%`五种。  
也有更复杂的类型：
```javascript
Math.pow(2,3)   //2的3次幂
Math.round(.6) 	//四舍五入
Math.ceil(.6) 	//向上取整
Math.floor(.6) 	//向下取整
Math.abs(-5)	//绝对值
Math.max(...n)  //最大值
Math.min(...n)  //最大值
Math.random()	//生成大于等于0小于1.0的伪随机数
Math.PI			//圆周率
Math.E			//自然数
Math.sqrt(3)	//3的平方根
Math.pow(3,1/3)	//3的立方根
Math.sin(0)		//三角函数正弦值，还有cos等
Math.log(10)	//10的自然对数
Math.log(100)/Math.LN10	//以10为底100的对数
Math.log(128)/Math.LN2	//以2为底128的对数
Math.exp(3)				//e的三次幂
```

JS在算术运算溢出、下溢和被0整除时不会报错
