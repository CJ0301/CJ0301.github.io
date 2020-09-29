---
layout: 		post
title: 			"Volley"
subtitle: 		'使用与源码解析'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## 源码解析
#### Volley
首先Volley的请求发送需要创建一个RequestQueue队列，创建它的方法一般用`Volley.newRequestQueue(Context)`