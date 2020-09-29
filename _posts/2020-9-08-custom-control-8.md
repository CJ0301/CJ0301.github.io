---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'Canvas与图层'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
mathjax: 		true
tags:
  - Android
---
在自定义View中有两种方法获取Canvas对象
方法一：  
```java
protected void on Draw(Canvas canvas){
	super.onDraw(canvas);
}

protected void dispatchDraw(Canvas canvas){
	super.dispatchDraw(canvas);
}
```
两个方法区别在于，onDraw()函数用于绘制视图自身，dispatchDraw()函数用于绘制子视图。  
无论是View还是ViewGroup，这两个函数的调用顺序都是onDraw()到dispatchDraw()。  
ViewGroup只有在有背景时调用onDraw()，否则跳过，直接调用dispatchDraw()，在ViewGroup中绘图一般重写dispatchDraw()。  
View中一般重写onDraw()函数。

方法二：使用Bitmap创建  
构造  
```java
Canvas c = new Canvas(bitmap);
```
或  
```java
Canvas c = new Canvas();
c.setBitmap(bitmap);
```

Bitmap加载方式
```
//方法1：新建一个空白bitmap
Bitmap bmp = Bitmap.createBitmap(width,height,Bitmap.Config.ARGB_8888)；
//方法2：从图片加载
Bitmap bmp = BitmapFactory.decodeResource(getResource(),R.drawable.wave_bg,null);
```

用Bitmap构造的Canvas中，绘制的图像会保存在Bitmap上，如果要显示在View上需要在onDraw()函数使用传入的canvas绘制Bitmap。

```java
public class MyView extends View {
    private Bitmap bitmap;
    private Canvas mCanvas;
    private Paint mPaint;

    public MyView(Context context,AttributeSet attrs) {
        super(context, attrs);
        initView();
    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        int width = MeasureSpec.getSize(widthMeasureSpec);
        int widMode = MeasureSpec.getMode(widthMeasureSpec);
        int height = MeasureSpec.getSize(heightMeasureSpec);
        int heiMode = MeasureSpec.getMode(heightMeasureSpec);

        width = measureWidth(width,widMode);
        height = measureHeight(height,heiMode);
        setMeasuredDimension(width,height);
    }

    private int measureWidth(int width,int mode){
        switch (mode){
            case MeasureSpec.AT_MOST:
                width = bitmap.getWidth();
                break;
            case MeasureSpec.UNSPECIFIED:
                break;
            case MeasureSpec.EXACTLY:
                reSize(((float)width)/bitmap.getWidth(),1);
                break;
        }

        return width;
    }

    private void reSize(float scaleWidth,float scaleHeight){
        //获取想要缩放的matrix
        Matrix matrix = new Matrix();
        matrix.postScale(scaleWidth,scaleHeight);

        //获取新的bitmap
        bitmap=Bitmap.createBitmap(bitmap,0,0,bitmap.getWidth(),bitmap.getHeight(),matrix,true);
    }

    private int measureHeight(int height,int mode){
        switch (mode){
            case MeasureSpec.AT_MOST:
                height = bitmap.getHeight();
                break;
            case MeasureSpec.UNSPECIFIED:
                break;
            case MeasureSpec.EXACTLY:
                reSize(1,((float)height)/bitmap.getHeight());
                break;
        }

        return height;
    }

    public void initView(){
        mPaint = new Paint();
        bitmap = BitmapFactory.decodeResource(getResources(),R.drawable.beauty,null).copy(Bitmap.Config.ARGB_8888, true);
        mPaint.setTextSize(90);
        mPaint.setColor(Color.RED);

    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        mCanvas = new Canvas(bitmap);
        int width = canvas.getWidth();
        int height = canvas.getHeight();
        mCanvas.drawText("憨憨",width/2-60,height/5,mPaint);
        canvas.drawBitmap(bitmap,0,0,mPaint);
    }
}

```