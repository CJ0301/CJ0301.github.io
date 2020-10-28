---
layout: 		post
title: 			"OpenCV 3"
subtitle: 		'图像操作'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---

## 模糊
#### 卷积概念
(之后补上)

#### 均值模糊
基于相同系数的卷积核完成的卷积操作叫均值模糊。  
主要用于降低图像噪声、模糊图像、降低图像对比度

```java
//src表示输入图像
//dst表示输出图像
//ksize表示图像卷积核大小
//anchor表示卷积核的中心位置
//borderType边缘填充类型，默认用BORDER_DEFAULT
blur(Mat src,Mat dst,Size ksize,Point anchor,int borderType)
```

实现
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);

Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}

Mat dst = new Mat();
Imgproc.blur(src,dst,new Size(30,30),new Point(-1,-1),Core.BORDER_DEFAULT);

Utils.matToBitmap(dst,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

这里卷积核大小用的是30*30，如果想只在垂直或水平方向模糊，则改成：  
- new Size(30,1)：水平方向模糊
- new Size(1,30)：垂直方向模糊

#### 高斯模糊
```java
//src输入图像，常见CV_8UC3/CV_8UC4类型
//dst输出图像，类型通常与输入一致
//ksize表示图像卷积核大小
//sigmaX表示X方向的模糊程度
//sigmaY表示Y方向的模糊程度
//borderType边缘填充类型，默认用BORDER_DEFAULT
GaussianBlur(Mat src,Mat dst,Size ksize,double sigmaX,double sigmaY,int borderType)
```

ksize大小可以通过用户输入参数，或通过计算sigmaX得到。  
当ksize值非零，表示sigmaX将会通过ksize计算产生，无需填写；  
当ksize值为零，sigmaX必须为非零值，ksize大小将由sigmaX计算产生。

实现
```
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);

Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}

Mat dst = new Mat();
Imgproc.GaussianBlur(src,dst,new Size(55,55),15,0,Core.BORDER_DEFAULT);

Utils.matToBitmap(dst,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

```
//后面两参数可省略，写成  
Imgproc.GaussianBlur(src,dst,new Size(0,0),15);
//或
Imgproc.GaussianBlur(src,dst,new Size(15,15),0);
```

#### 滤波
#### 中值滤波
```java
Log.i("加载开始", "-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(), R.drawable.test);

Mat src = new Mat();
Utils.bitmapToMat(bitmap, src);
if (src.empty()) {
	return;
}

Mat dst = new Mat();
Imgproc.medianBlur(src,dst,3);

Utils.matToBitmap(dst, bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```