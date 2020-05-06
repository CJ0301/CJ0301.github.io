---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'绘图基础'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## 基本图形绘画
#### 概述
在图形绘制里有两个工具：Paint和Canvas。
🌰：  
```java
public class BasicView extends View {
    public BasicView(Context context) {
        super(context);
    }

    public BasicView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public BasicView(Context context,AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        Paint paint = new Paint();
        paint.setColor(Color.RED);//设置画笔颜色
        paint.setStyle(Paint.Style.STROKE);//设置填充样式
        paint.setStrokeWidth(50);//设置画笔宽度

        canvas.drawCircle(300,300,150,paint);//圆心的位置，半径和画笔
    }
}

```

#### 画笔使用基础
1.void setColor(int color)或setColor(long color)  
Color具体怎么用更新在下面。

2.void setstyle(Style style)    
style可选的取值有：  
- Paint.Style.FILL:仅填充内部。  
- Paint.Style.FILL_AND_STROKE:填充与描边。  
- Paint.Style.STROKE:仅描边。  

描边是原有半斤加上画笔宽度，填充是仅填充内部。  

3.void setSrokeWidth(float width)    
当样式有描边的时候有效。

#### Canvas使用基础
1.画布背景设置
```java
void drawColor(int color)
void drawARGB(int A,int r,int g,int b)
void drawRGB(int r,int g,int b)
```

2.直线  
```java
void drawLine(float startX,float startY,float stopX,float stopY,Paint paint)
```
参数分别为起点XY坐标与终点XY坐标。
粗细与Style无关。

3.点
```java
void drawPoint(float x,float y,Paint paint)
```
大小与Style无关。

4.矩形类工具RectF、Rect以及绘制
RectF的四个构造函数：
```java
RectF()
RectF(float left,float top,float right,float bottom)
RectF(RectF r)
RectF(Rect r)
```
Rect的三个构造函数：
```java
RectF()
Rect(float left,float top,float right,float bottom)
Rect(Rect r)
```

这两个构造函数基本相同，不同在于RectF保存的数值类型为float类型。

一般的矩形构建可通过下面两种方法实现：
```java
//方法一：直接构造
Rect rect = new Rect(10,10,100,100);
//方法二：间接构造
Rect rect = new Rect();
rect.set(10,10,100,100);
```

构造完就要进行绘制了：
```java
void drawRect(float left,float top,float right,float bottom,Paint paint)
void drawRect(RectF rect,Paint paint)
void drawRect(Rect r,Paint paint)
```

left、top、right、bottom四个参数的意义：左上角与右下角坐标。

#### 颜色
Color是Android中处理颜色的一个类
1.常量颜色
Color中定义了一部分能直接拿来用的颜色值
```
int BLACK
int BLUE
int CYAN
int DKGRAY
int GRAY
int GREEN
int LTGRAY
int MAGENTA
int RED
int TRANSPARENT
int WHITE
int YELLOW
```
2.构造颜色
1)带透明度的颜色
```java
static int argb(int alpha,int red,int green,int blue)
```
这个函数分别有A、R、G、B四个颜色分量，取值范围都是0~255。

argb的源码：
```java
public static int argb(int alpha,int red,int green,int blue){
	return (alpha << 24)|(red << 16)|(green << 8)|blue;
}
```
将四个色值移动到相应的位置组成颜色值。

2)不带透明度的颜色
```java
static int rgb(int red,int green,int blue)
```

3.提取颜色分量
Color可以用对应的方法设置以及提取alpha、red、green、blue四种分量。

#### 路径
Path是Android中的路径类。  
Canvas绘制路径的方法为：
```java
void drawPath(Path path,Paint paint)
```

1.直线路径
画一条直线需要三个步骤：
1)设定初始点  
```java
void moveTo(float x1,float y1)
```
2)绘制直线并挪动起点
```java
void lineTo(float x2,float y2)
```
3)如果没有形成闭环则用close进行首位相连  
```java
void close()
```

2.弧线路径
```java
void arcTo(RecF oval,float startAngle,float sweepAngle)
```
弧线是从椭圆上截取的一部分。  
参数：  
- RecF oval：生成椭圆的矩形。
- float startAngle：弧开始的角度，以x轴正方向为0°。
- float sweepAngle：弧持续的角度。

但当我们用这个代码画一个路径：
```java
Path path = new Path();
path.moveTo(50,50);
RectF rectF = new RectF(100,10,200,100);
path.arcTo(rectF,0,90);

canvas.drawPath(path,paint);
```

会发现弧线起点与原来的起点相连了，默认情况下路径是连贯的，可以用两个方法解决这个问题：  
- 调用addXXX系列函数，直接添加固定形状的路径。
- 调用moveTo()函数改变绘制起始位置
- 使用Path类的两个重载方法：
```java
void arcTo(float left,float top,float right,float bottom,float startAngle,float sweepAngle,boolean forceMoveTo)
void arcTo(RecF oval,float startAngle,float sweepAngle,boolean forceMoveTo)
```

#### 区域
Region是Android中的区域类。  

1.构造Region
1)直接构造
```java
public Region(Region region) //复制一个Region范围
public Region(Rect r) //创建一个矩形区域
public Region(int left,int top,int right,int bottom)//创建一个矩形区域
```

2)间接构造
间接构造由Region的空构造与set函数实现。  
空构造：  
```java
public Region()
```

set系列函数：  
```java
public void setEmpty() //置空
public boolean set(Region region) //用新区域替换原来区域
public boolean set(Rect r)//用矩形替换原来区域
public boolean set(int left,int top,int right,int bottom)//用矩形两个角点来构造新的区域
public boolean setPath(Path path,Region clip)
```

注意：无论set系列函数中的Region是否有区域值，调用set系列函数后都会被替换成set系列函数里的区域值。

在canvas中没有绘画Region的代码，只能自己写：  
```java
private void drawRegion(Canvas canvas,Region region,Paint paint){
	RegionIterator iterator = new RegionIterator(region);
	Rect r = new Rect();
	while(iterator.next(r)){
		canvas.drawRect(r,paint);
	}
}
```
不规则区域绘制：  
```java
boolean setPath(Path path,Region clip)
```
Path path:构造区域路径。  
Region clip:与原来的path构成的路径取交集。

```java
//弧线路径
RectF re = new RectF();
re.set(10,10,300,500);
Path path = new Path();
path.addOval(re,Path.Direction.CCW);

//取一个较小的区域
Region region = new Region();
//区域与路径取交集
region.setPath(path,new Region(10,10,300,150));

//绘制
drawRegion(canvas,region,paint);
```

2.区域相交  
1)union函数:将指定矩形加入区域。
```java
boolean union(Rect r)
```

🌰：  
```java
//取一个区域
Region region = new Region(10,10,200,100);
//将另一个区域合并
region.union(new Rect(10,10,50,300));
//将另一个区域合并
region.union(new Rect(160,10,200,300));
//绘制
drawRegion(canvas,region,paint);
```

2)区域操作  
除了union()函数以外，Region还提供了如下几个更加灵活的操作函数。
系统方法一：  
```java
boolean op(Rect r,Op op)
boolean op(int left,int top,int right,int bottom,Op op)
boolean op(Region region,Op op)
```

这些函数的用处就是用当前Region对象与指定Rect对象或者Region对象执行相交操作，并赋值给Region。计算成功返回true，否则返回false。

Op参数有六个：  
```java
public enum Op {
	DIFFERENCE(0),
	INTERSECT(1),
	UNION(2),
	XOR(3),
	REVERSE_DIFFERENCE(4)
}
```

🌰： 
```java
Paint paint = new Paint();
paint.setColor(Color.parseColor("#cccccc"));//设置画笔颜色
paint.setStyle(Paint.Style.STROKE);//设置填充样式
paint.setStrokeWidth(2);//设置画笔宽度

        
//构造两个矩形
Rect rect1 = new Rect(100,100,400,200);
Rect rect2 = new Rect(200,0,300,300);

canvas.drawRect(rect1,paint);
canvas.drawRect(rect2,paint);

//构造两个区域
Region region1 = new Region(rect1);
Region region2 = new Region(rect2);

//取两个区域的交集
region1.op(region2, Region.Op.INTERSECT);

Paint paint_fill = new Paint();
paint_fill.setColor(Color.GREEN);
paint.setStyle(Paint.Style.FILL);
drawRegion(canvas,region1,paint_fill);
```

系统方法二：
```
boolean op(Rect rect,Region region,Op op)
boolean op(Region region1,Region region2,Op op)
```

两个函数允许传入两块区域，操作后返回给Region对象。

#### 画布
Canvas是Android中的画布类。  
1.画布变换    
1）平移    
Canvas中有一个函数translate()用来实现画布平移。  
```java
void translate(float dx,float dy)
```
- dx:水平方向平移距离，正为右移，负为左移。
- dy:垂直方向平移距离，正为下移，负为上移。

注意：  
1. 每次调用drawXXX函数时，都会产生一个新的Canvas透明图层。
2. 调用drawXXX函数前调用平移等操作，则操作不可逆，每次产生的最新位置都是操作后的位置。
3. 在Canvas图层与屏幕合成时，超出部分图像不会显示。

2.裁剪画布
裁剪画布是指利用clip系列函数，通过与Rect、Path、Region取交、并、差等集合运算来获得最新的画布形状。除调用save()、restore()函数以外，这个操作是不可逆的，一旦Canvas被裁剪，就不能恢复。

注意：使用裁剪画布系列函数时，需要禁用硬件加速功能。
```
setLayerType(LAYER_TYPE_SOFTWARE,null);
```

裁剪系列函数：  
```java
boolean clipPath(Path path)
boolean clipPath(Path path,Region.Op op)
boolean clipRect(Rect rect,Region.Op op)
boolean clipRect(RectF rect,Region.Op op)
boolean clipRect(int left,int top,int right,int bottom)
boolean clipRect(float left,float top,float right,float bottom)
boolean clipRect(Rect rect)
boolean clipRect(RectF rect)
boolean clipRect(float left,float top,float right,float bottom,Region.Op op)
boolean clipRegion(Region region)
boolean clipRegion(Region region,Region.Op op)
```

🌰： 
```java
canvas.drawColor(Color.RED);
canvas.clipRect(new Rect(100,100,200,200));
canvas.drawColor(Color.GREEN);
```

3.画布的保存与恢复
1）save()与restore()  
```java
int save()
void restore()
```

save()：每次调用save()函数，保存当前画布状态，并放入栈中
restore()：每次调用restore()函数，都会把栈中顶层的画布状态取出来，并按照这个状态恢复画布。