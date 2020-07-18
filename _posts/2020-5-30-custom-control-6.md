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


#### 计算获得基线位置  
例1🌰.定点写字    
给定左上角坐标(left,top)，要写字必然要确定左基线与下基线的位置，下基线的位置需要通过文字大小以及上基线位置进行计算：  
Paint.FontMetricsInt.top = top - baseline  
可得  
baseline = top - FontMetricsInt.top

MyTextView.java
```java
public class MyTextView extends View {

    public MyTextView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);

    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        String text = "SomeWords";
        int top = 400;
        int baseLineX = 90;

        //设置Paint
        Paint paint = new Paint();
        paint.setTextSize(120);
        paint.setTextAlign(Paint.Align.LEFT);

        //画top线
        paint.setColor(Color.YELLOW);
        paint.setStrokeWidth(3);
        canvas.drawLine(baseLineX,top,300,top,paint);

        //计算出baseline线的位置
        Paint.FontMetricsInt fm = paint.getFontMetricsInt();
        int baseLineY = top-fm.top;

        //画基线
        paint.setColor(Color.RED);
        canvas.drawLine(baseLineX,baseLineY,300,baseLineY,paint);

        //写文字
        paint.setColor(Color.BLACK);
        canvas.drawText(text,baseLineX,baseLineY,paint);
    }
}
```

例2🌰.给定中间线写字  
center线是矩形的中线，正好在top线与bottom线之间，可以根据公式推得：  
baseline = center+(FontMetricsInt.bottom-FontMetricsInt.top)/2-FontMetricsInt.bottom  

## Paint常用函数  
#### 基本设置函数
重置画笔
```java
reset()
```

给画笔设置颜色值
```java
setColor(int color)
```

给画笔设置颜色值
```java
setARGB(int a,int r,int g,int b)
```

设置画笔透明度
```java
setAlpha(int a)
```

设置画笔样式
```java
setStyle(Paint.Style style)
```
- Paint.Style.FILL：填充内部。
- Paint.Style.FILL_AND_STROKE：填充内部和描边。
- Paint.STROKE：仅描边。
```java
//画笔宽度
setStrokeWidth(float width)
//抗锯齿
setAntiAlias(boolean aa)
//设置画笔倾斜度(没啥区别)
setStrokeMiter(float miter)
//设置路径样式，取值是PathEffect的子类
set PathEffect(PathEffect effect)
//设置线帽样式取值有三个，线帽是多出来的一部分
setStrokeCap(Paint.Cap cap)
//设置转角样式取值有三个MITER(锐角)、Join.ROUND(圆弧)、BEVEL(直线)
setStrokeJoin(Paint.Join join)
//绘制图像设置抗抖动
setDither(boolean dither)
```

#### 字体相关函数 
```java
//设置文字大小
setTextSize(float textSize)
//设置是否是粗体文字
setFakeBoldText(boolean fakeBoldText)
//设置带有删除线效果
setStrikeThruText(boolean strikeThruText)
//设置下划线
setUnderlineText(boolean underlineText)
//设置开始绘图点位置
setTextAlign(Paint.Align align)
//设置水平拉伸
setTextScaleX(float scaleX)
//设置字体水平倾斜度。普通斜体字设置为-0.25，向右倾斜
setTextSkewX(float skewX)
//设置字体样式
setLinearText(boolean linearText)
```