---
layout: 		post
title: 			"Android高级UI_1"
subtitle: 		'UI核心'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## UI的绘制
#### View添加到屏幕
View添加到屏幕窗口上的过程大致分为三步  
1. 创建顶层布局容器DecorView  
2. 在顶层布局中加载基础布局ViewGroup
3. 将ContentView添加到基础布局中的FrameLayout中

首先来看一下布局在Activity加载时所执行的一些代码。  

先创建一个Activity，注意要继承Activity，AppCompat那个会不太一样。

进入setContentView方法，这时候看到方法里将layout的id给了Window对象，进入Window对象后可发现最上方的注释写着唯一的实现类是PhoneWindow。搜索PhoneWindow源码，找到实现的setContentView方法。  
这个方法主要做了两件事，创建顶级容器DecorView，将布局资源放入容器。  
如果DecorView不存在，则在installDecor方法里的generateDecor中顶级容器被创建并赋值。创建完成之后判断mContentParent是否存在，不存在则在generateLayout中将DecorView传入，进行初始化。   
generateLayout中会读取style的资源文件，创建完成后将DecorView放入。其中有一行注释标明Inflate the window decor，下面就是对DecorView的处理，其中调用的onResourcesLoaded解析基础布局并添加至顶层容器DecorView。

从类关系层面看，Window作为抽象类，提供了一系列绘制窗口的通用API。  
PhoneWindow是Window的具体继承实现类，且内部包含了一个DecorView对象，该对象是所有应用窗口(Activity)的根View。    
DecorView是PhoneWindow的内部类，是FrameLayout的子类，是所有应用窗口的根View。
  
从视图结构看，DecorView作为父容器先进行创建。  
然后在generateLayout加载里面的布局，在onResourcesLoaded调用的上方可看到提前加载的layoutResource参数包含的一个根据主题渲染好的布局id。以screen_simple举例，他是一个垂直线性布局，上面是ViewStub，下面是一个id为content的FrameLayout，也就是在generateLayout最后生成返回的那个contentParent。  

现在重新来看PhoneWindow的setContentView方法就很清楚的知道流程了，如果装载layout资源的mContentParent不存在，说明顶级容器不存在，先创建DecorView，根据style生成相应的样式，再装入DecorView，并将生成样式中的内容部分生成ViewGroup赋值给mContentParent参数，然后再将mContentParent和之前传入的layout进行处理。

#### 

