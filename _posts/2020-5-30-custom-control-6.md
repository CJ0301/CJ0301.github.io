---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'Paint的基本使用'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---

## GPU加速
禁止方法：  
1）在AndroidManifest.xml文件重为application标签添加如下属性，即可为整个应用流程开启/关闭硬件加速。
```xml
<application android:hardwareAccelerated="true"...>
```

2）在activity标签下使用hardwareAccelerated属性来开启关闭硬件加速。
```xml
<activity android:hardwareAccelerated="false" />
```

3）在Window层级上使用如下代码开启硬件加速(不支持关闭)。
```java
getWindow().setFlags(
WindowManager.LayoutParams.FLAG_HARDWARE_ACCELERATED,
WindowManager.LayoutParams.FLAG_HARDWARE_ACCELERATED);
```

4）在View层级上使用如下代码关闭硬件加速(不支持开启)。
```java
setLayerType(View.LAYER_TYPE_SOFTWARE,null);
```
或者用layerType属性。
```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:layerType="software"
    tools:context=".MainActivity">
```

## 文字
#### drawText()
在Canvas中，drawText()是根据基线绘制的。
```java
 public void drawText(String text, float x, float y,Paint paint)
```

🌰:  
```java
@Override
protected void onDraw(Canvas canvas) {
	super.onDraw(canvas);

	int baseLineX = 20;
	int baseLineY = 200;

	//画基线
	Paint paint = new Paint();
	paint.setColor(Color.RED);
	canvas.drawLine(baseLineX,baseLineY,3000,baseLineY,paint);
		
	//写文字
	paint.setColor(Color.GREEN);
	paint.setTextSize(120);//px为单位
	canvas.drawText("Hello World",baseLineX,baseLineY,paint);
}
```

#### setTextAlign()函数  
这个函数用于指定从文字的哪一部分开始绘制。  
一共有Paint.Align.LEFT、Paint.Align.CENTER、Paint.Align.RIGHT

#### 绘图四线格与FontMetrics
除了基线以外，系统在绘制文字时还有四条线：  
- ascent：系统推荐的，在绘制单个字符时，字符的最高高度所在线。
- descent：系统推荐的，在绘制单个字符时，字符的最低高度所在线。
- top：可绘制的最高高度所在线。
- bottom：可绘制的最低高度所在线。

FontMetrics为这四条线的位置提供计算：
- ascent=ascent线的y坐标-baseline线的y坐标
- descent=descent线的y坐标-baseline线的y坐标
- top=top线的y坐标-baseline线的y坐标
- bottom=bottom线的y坐标-baseline线的y坐标

#### 常用函数
1）高度
```java
Paint.FontMetrics fm = paint.getFontMetrics();
int top = baseLineY + fm.top;
int bottom = baseLineY + fm.bottom;
int height = bottom - top;
```

2）宽度
```java
Paint paint = new Paint();
paint.setTextSize(120);
int width = (int)paint.measureText("Hello");
```

3）最小矩形
```java
/**
 * 获取指定字符串所对应的最小矩形，以(0,0)点所在位置为基线
 * @param text 要测量最小矩形的字符串
 * @param start 要测量起始字符在字符串中的索引
 * @param end 所测量字符串长度
 * @param bounds 接收测量结果
 */
public void getTextBounds(String text,int start,int end,Rect bounds);
```

🌰: 
```java
String text = "Hello";
Paint paint = new Paint();
paint.setTextSize(120);

Rect minRect = new Rect();
paint.getTextBounds(text,0,text.length(),minRect);
Log.i("result",minRect.toShortString());
```

这样能打印出来以baseLine为基线的矩形位置，实际的给两个点的y值向上baseLineY即可。
