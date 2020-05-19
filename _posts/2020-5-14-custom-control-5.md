---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'动画进阶'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
> PathMeasure类能通过对Path路径的坐标追踪实现复杂动画效果。
## PathMeasure实现路径动画

#### 常用函数
初始化：
1）空参初始化
创建对象
```java
PathMeasure pathMeasure = new PathMeasure();
```

路径绑定
```java
setPath(Path path,boolean forceClosed)
```

2）带参初始化
```
PathMeasure(Path path,boolean forceClosed);
```

forceClosed参数为true时，路径会被强制闭合。

简单函数使用  
```
//获取计算的路径长度
public float getLength()
//是否闭合
public boolean isClosed()
//跳转到下一条曲线，成功返回true
public boolean nextContour()
//截取范围内路径
public boolean getSegment(float startD,float stopD,Path dst,boolean startWithMoveTo)
```

1）路径长度与闭合
```java
canvas.translate(50,50);

Paint paint = new Paint();
paint.setColor(Color.RED);//设置画笔颜色
paint.setStyle(Paint.Style.STROKE);//设置填充样式
paint.setStrokeWidth(50);//设置画笔宽度

Path path = new Path();
path.moveTo(0,0);
path.lineTo(0,100);
path.lineTo(100,100);
path.lineTo(100,0);

PathMeasure measure1 = new PathMeasure(path,false);
PathMeasure measure2 = new PathMeasure(path,true);

Log.i("getLength()","forceClosed=false---> Length "+measure1.getLength()+"  isClosed "+measure1.isClosed());
Log.i("getLength()","forceClosed=true--->Length "+measure2.getLength()+"  isClosed "+measure2.isClosed());

canvas.drawPath(path,paint);
```

Log
```
2020-05-15 10:10:54.846 16395-16395/com.fb.test I/getLength(): forceClosed=false---> Length 300.0  isClosed false
2020-05-15 10:10:54.846 16395-16395/com.fb.test I/getLength(): forceClosed=true--->Length 400.0  isClosed true
```

上面画了一个未闭合的矩形，当forceClosed为true时，路径长度为闭合时的长度。isClosed函数在forceClosed为true时返回值一定为true。

2）跳转下一条曲线
```java
canvas.translate(150,150);

Paint paint = new Paint();
paint.setColor(Color.RED);//设置画笔颜色
paint.setStyle(Paint.Style.STROKE);//设置填充样式
paint.setStrokeWidth(10);//设置画笔宽度

Path path1 = new Path();
path1.moveTo(200,200);
path1.lineTo(200,300);
path1.lineTo(300,300);

Path path = new Path();
path.addRect(-50,-50,50,50,Path.Direction.CW);
path.addRect(-100,-100,100,100,Path.Direction.CW);
path.addRect(-120,-120,120,120,Path.Direction.CW);
path.addPath(path1);

PathMeasure measure1 = new PathMeasure(path,false);

do {
	Log.i("getLength()","forceClosed=false---> Length "+measure1.getLength()+"  isClosed "+measure1.isClosed());
}while (measure1.nextContour());

canvas.drawPath(path,paint);
```

Log
```
2020-05-15 10:08:45.129 16018-16018/com.fb.test I/getLength(): forceClosed=false---> Length 400.0  isClosed true
2020-05-15 10:08:45.129 16018-16018/com.fb.test I/getLength(): forceClosed=false---> Length 800.0  isClosed true
2020-05-15 10:08:45.129 16018-16018/com.fb.test I/getLength(): forceClosed=false---> Length 960.0  isClosed true
2020-05-15 10:08:45.130 16018-16018/com.fb.test I/getLength(): forceClosed=false---> Length 200.0  isClosed false
```

由此可看出，isClosed和getLength函数都是判断当前曲线。nextContour得到的曲线顺序与添加顺序一致。

3）截取
参数：  
- float startD：开始截取位置距离Path起始点长度。
- float stopD：结束截取位置距离Path起始点的长度。
- Path dst：截取的Path将会被添加到dst中。注意是添加。
- boolean startWithMoveTo：起始点是否使用moveTo,就是将起始点移动到结果Path的起始点，通常为true。

注意：  
- 如果startD、stopD不在取值范围[0,getLength]内，或二者相等，则返回值为false，且不改变dst中的内容。
- 开启硬件加速后会出问题。
- 截取路径会与绘制方向有关。

🌰startWithMoveTo：
```
canvas.translate(450,450);

Paint paint = new Paint();
paint.setColor(Color.RED);//设置画笔颜色
paint.setStyle(Paint.Style.STROKE);//设置填充样式
paint.setStrokeWidth(50);//设置画笔宽度

Path path = new Path();
path.addRect(-150,-150,150,150,Path.Direction.CW);
Path dst = new Path();
dst.lineTo(30,300);
PathMeasure measure = new PathMeasure(path,false);
measure.getSegment(0,450,dst,false);
canvas.drawPath(dst,paint);
```
startWithMoveTo是flase后，上一条路径的终点变成下一条路径的起点。

🌰刷新界面：
```
public class MyView extends View {
    Paint mPaint;
    Path mDstPath,mCirclePath;
    PathMeasure mPathMeasure;
    Float mCurAnimValue;

    public MyView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        setLayerType(LAYER_TYPE_SOFTWARE,null);

        mPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        mPaint.setStyle(Paint.Style.STROKE);
        mPaint.setStrokeWidth(16);
        mPaint.setColor(Color.BLACK);

        mDstPath = new Path();
        mCirclePath = new Path();
        mCirclePath.addCircle(100,100,50,Path.Direction.CW);

        mPathMeasure = new PathMeasure(mCirclePath,true);

        ValueAnimator animator = ValueAnimator.ofFloat(0,1);
        animator.setRepeatCount(ValueAnimator.INFINITE);
        animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
            @Override
            public void onAnimationUpdate(ValueAnimator animation) {
                mCurAnimValue = (Float)animation.getAnimatedValue();
                invalidate();
            }
        });
        animator.setDuration(2000);
        animator.start();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        float length = mPathMeasure.getLength();
        float stop = length * mCurAnimValue;
        float start = (float)(stop-((0.5-Math.abs(mCurAnimValue - 0.5))*length));

        mDstPath.reset();
        canvas.drawColor(Color.WHITE);
        mPathMeasure.getSegment(start,stop,mDstPath,true);
        canvas.drawPath(mDstPath,mPaint);
    }
}

```