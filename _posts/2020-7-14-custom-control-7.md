---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'绘图进阶'
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
## 贝塞尔曲线  
贝塞尔曲线的n次曲线表示为：  

$$p(t)= \sum_{i=0}^{n}  a_i f_{i,n}(t),0\Rightarrow t \Rightarrow 1$$  

其中系数矢量$a_i(i=0,1,...,n)顺序首尾相接$  
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-07-14-bezier-1.png)  
这条折线被称为控制多边形或贝塞尔多边形。

#### 定义
给定空间n+1个点的位置矢量$P_i(i=0,1,2,...,n)$，则贝塞尔曲线段的参数方程表示如下：  
  
$$p(t)= \sum_{i=0}^{n}  P_i B_{i,n}(t),0\Rightarrow t \Rightarrow 1$$  

$其中P_i(x_i,y_i,z_i),i=0,1,2,...,n是控制多边形的n+1个定点，即构成该曲线的特征多边形；B_{i,n}(t)是贝塞尔基函数，有如下形式：  $

$$B_{i,n} = \frac{n!}{i!(n-i)!}t^i(1-t)^{n-i}=C^i_nt^i(1-t)^{n-i}(i=0,1,...,n)$$

$P_i$代表空间的很多点，t在0到1之间，把t代进去可以算出一个数，即平面或空间的一个点。  
随着t值的变化，点也在变化。当t从0变到1时，就得到空间的一个图形，这个图形就是贝塞尔曲线。  
二阶贝塞尔曲线：
![二阶贝塞尔曲线](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-07-14-bezier-2.gif)

#### 举例
一次贝塞尔曲线  
$$B_{i,n}(t) = \frac{n!}{i!(n-i)!}t^i(1-t)^{n-i} \\
B_{i,n}(t) = \frac{1!}{0!(1-0)!}t^0(1-t)^{1-0} = 1-t \\
B_{i,n}(t) = \frac{1!}{1!(1-1)!}t^1(1-t)^{1-1} = t \\
p(t) = \sum_{i=0}^{n}  P_i B_{i,n}(t) = P_0B_{0,1}(t)+P_1B_{1,1}(t) \\
=(1-t)P_0+tP_1 \\
连起来恰好是连接P_0到终点P_1的直线段 $$
![一阶贝塞尔曲线](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-07-14-bezier-3.gif)

二次贝塞尔曲线  
$$当n=2时，有3个控制点p_0、p_1和p_2，贝塞尔多项式是二次多项式： \\
p(t)=\sum^2_{i=0}P_iB_{I,2}(t) = P_0B_{0,2}(t)+P_1B_{1,2}(t)+P_2B_{2,2}(t) \\
=(1-t)^2P_0+2t(1-t)P_1+t^2P_2 \\
矩阵形式：  
p(t)=\begin{bmatrix}
 t^2 & t & 1
\end{bmatrix}·\begin{bmatrix}
 1 & -2 & 1\\
 -2 & 2 & 0\\
 1& 0 & 0
\end{bmatrix}·\begin{bmatrix}
 P_0\\
 P_1\\
 P_2
\end{bmatrix}
$$
![二阶贝塞尔曲线](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-07-14-bezier-2.gif)

#### quadTo
Path类中有四个与贝塞尔曲线相关的函数。 
```java
//二阶贝塞尔曲线
public void quadTo(float x1,float y1,float x2,float y2)
public void rQuadTo(float dx1,float dy1,float dx2,float dy2)
//三阶贝塞尔曲线
public void cubicTo(float x1,float y1,float x2,float y2,float x3,float y3)
public void rCubicTo(float dx1,float dy1,float dx2,float dy2,float dx3,float dy3)
```

quadTo使用原理  
```java
public void quadTo(float x1,float y1,float x2,float y2)
```
这两组参数分别表示的是控制点坐标与终点坐标。

整条线的起始点并不通过该方法指定，而是通过Path.moveTo(x,y)函数指定，如果我们连续调用函数quadTo()，则上一个quadTo()函数的终点就是下一个的起始点，没有通过Path.moveTo(x,y)函数指定起始点则默认以控件左上角点(0,0)为起始点。
```java
//设置Paint
Paint paint = new Paint();
paint.setColor(Color.BLACK);
paint.setStrokeWidth(8);
paint.setStyle(Paint.Style.STROKE);

Path path = new Path();
path.moveTo(100,300);
path.quadTo(200,200,300,300);
path.quadTo(400,400,500,300);
canvas.drawPath(path,paint);
```

例1🌰.传统捕捉手势轨迹
```java
public class MyTextView extends View{
    private Path mPath = new Path();
    private Paint mPaint;

    public MyTextView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);

        mPaint = new Paint();
        mPaint.setColor(Color.BLACK);
        mPaint.setStyle(Paint.Style.STROKE);
        mPaint.setStrokeWidth(8);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawColor(Color.WHITE);
        canvas.drawPath(mPath,mPaint);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction()){
            case MotionEvent.ACTION_DOWN:{
                mPath.moveTo(event.getX(),event.getY());
                return true;
            }

            case MotionEvent.ACTION_MOVE:
                mPath.lineTo(event.getX(),event.getY());
                postInvalidate();
                break;

            default:
                break;
        }
        return super.onTouchEvent(event);
    }
}

```

例2🌰.优化曲线  
想看出效果得画的足够快，毕竟现在手机处理速度比之前快了不少
```java
public class MyTextView extends View{
    private Path mPath = new Path();
    private Paint mPaint;
    private float mPreX,mPreY;

    public MyTextView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);

        mPaint = new Paint();
        mPaint.setColor(Color.BLACK);
        mPaint.setStyle(Paint.Style.STROKE);
        mPaint.setStrokeWidth(8);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawColor(Color.WHITE);
        canvas.drawPath(mPath,mPaint);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction()){
            case MotionEvent.ACTION_DOWN:{
                mPreX = event.getX();
                mPreY = event.getY();
                mPath.moveTo(mPreX,mPreY);
                return true;
            }

            case MotionEvent.ACTION_MOVE:
                float endX = (mPreX+event.getX())/2;
                float endY = (mPreY+event.getY())/2;
                mPath.quadTo(mPreX,mPreY,endX,endY);
                mPreX = event.getX();
                mPreY = event.getY();
                invalidate();
                break;

            default:
                break;
        }
        return super.onTouchEvent(event);
    }
}
```

#### rQuadTo
```java
public void rQuadTo(float dx1,float dy1,float dx2,float dy2)
```
参数： 
- dx1:控制点x坐标，表示相对于上一个终点x坐标的位移坐标。可为负值，正值加负值减。
- dy1:控制点y坐标，表示相对于上一个终点x坐标的位移坐标。可为负值，正值加负值减
- dx2:终点x坐标，表示相对于上一个终点x坐标的位移坐标。可为负值，正值加负值减
- dy2:终点y坐标，表示相对于上一个终点x坐标的位移坐标。可为负值，正值加负值减

例1🌰.实现波浪线  
```java
Paint paint = new Paint();
paint.setColor(Color.BLACK);
paint.setStrokeWidth(8);
paint.setStyle(Paint.Style.STROKE);

Path path = new Path();
path.moveTo(100,300);
path.quadTo(200,200,300,300);
path.quadTo(400,400,500,300);
canvas.drawPath(path,paint);
``` 

例2🌰.实现波浪动画
```java
public class AnimateWaveView extends View {
    private Paint mPaint;
    private Path mPath;
    //设置波浪长度
    private int mItemWaveLength = 1200;
    //用于调整起点
    private int dx;

    public AnimateWaveView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        //初始化画笔
        mPath = new Path();
        mPaint = new Paint();
        mPaint.setColor(Color.BLUE);
        mPaint.setStyle(Paint.Style.FILL);

        startAnim();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        mPath.reset();
        int originY = 300;
        int halfWaveLen = mItemWaveLength/2;

        //通过移动起点实现动画
        mPath.moveTo(-mItemWaveLength+dx,originY);

        //在原屏幕基础上加上两个波长的距离
        for(int i=-mItemWaveLength;i<=getWidth()+mItemWaveLength;i+=mItemWaveLength){
            mPath.rQuadTo(halfWaveLen/2,-100,halfWaveLen,0);
            mPath.rQuadTo(halfWaveLen/2,100,halfWaveLen,0);
        }

        //路径闭合，涂颜色用的
        mPath.lineTo(getWidth(),getHeight());
        mPath.lineTo(0,getHeight());
        mPath.close();

        canvas.drawPath(mPath,mPaint);
    }

    public void startAnim(){
        ValueAnimator animator = ValueAnimator.ofInt(0,mItemWaveLength);
        animator.setDuration(2000);
        animator.setRepeatCount(ValueAnimator.INFINITE);
        animator.setInterpolator(new LinearInterpolator());
        animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
            @Override
            public void onAnimationUpdate(ValueAnimator animation) {
                dx = (int)animation.getAnimatedValue();
                postInvalidate();
            }
        });
        animator.start();
    }
}

```

例3🌰.三阶贝塞尔曲线
```java
public class BezierView extends View {
    private float startPointX,startPointY;
    private float endPointX,endPointY;
    private float fPointX,fPointY;
    private float sPointX,sPointY;
    private Paint paint,bezierPaint;
    private Path mPath;
    private boolean isSecondPoint = false;

    public BezierView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        bezierPaint = new Paint();
        paint = new Paint();
        bezierPaint.setStrokeWidth(10);
        bezierPaint.setColor(Color.BLACK);
        bezierPaint.setStyle(Paint.Style.STROKE);

        paint.setStrokeWidth(5);
        paint.setColor(Color.GRAY);
        paint.setStyle(Paint.Style.STROKE);
        paint.setTextSize(50);
        mPath = new Path();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        mPath.reset();

        mPath.moveTo(startPointX,startPointY);
        mPath.cubicTo(fPointX,fPointY,sPointX,sPointY,endPointX,endPointY);
        canvas.drawPath(mPath,bezierPaint);

        canvas.drawPoint(startPointX,startPointY,paint);
        canvas.drawText("起点",startPointX+10,startPointY+10,paint);
        canvas.drawPoint(fPointX,fPointY,paint);
        canvas.drawText("控制点1",fPointX+10,fPointY+10,paint);
        canvas.drawPoint(sPointX,sPointY,paint);
        canvas.drawText("控制点2",sPointX+10,sPointY+10,paint);
        canvas.drawPoint(endPointX,endPointY,paint);
        canvas.drawText("终点",endPointX+10,endPointY+10,paint);
        canvas.drawLine(startPointX,startPointY,fPointX,fPointY,paint);
        canvas.drawLine(fPointX,fPointY,sPointX,sPointY,paint);
        canvas.drawLine(sPointX,sPointY,endPointX,endPointY,paint);

    }

    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);
        startPointX = w/4;
        startPointY = h/2;
        endPointX = w-startPointX;
        endPointY = h/2;
        fPointX = (endPointX-startPointX)/3+startPointX;
        fPointY = h/4*3;
        sPointX = endPointX-fPointX+startPointX;
        sPointY = h/4;
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction() & MotionEvent.ACTION_MASK){
            //第二个手指触发
            case MotionEvent.ACTION_POINTER_DOWN:
                isSecondPoint = true;
                break;
            case MotionEvent.ACTION_POINTER_UP:
                isSecondPoint = false;
                break;
            case MotionEvent.ACTION_MOVE:
                fPointX = event.getX(0);
                fPointY = event.getY(0);
                if(isSecondPoint){
                    sPointX = event.getX(1);
                    sPointY = event.getY(1);
                }
                invalidate();
                break;
        }
        return true;
    }
}

```

例4.获取物体运动轨迹路径
先准备转换点工具
BezierUtil.java
```java
public class BezierUtil {
    /**
     * B(t) = (1-t)^2*P0+2t*(1-t)*P1+t^2*P2,t∈[0,1]
     *
     * @param t 曲线长度比例
     * @param p0 起始点
     * @param p1 控制点
     * @param p2 终止点
     * @return 对应点
     * */
    public static PointF CalculateBezierPointForQuadratic(float t,PointF p0,PointF p1,PointF p2){
        PointF point = new PointF();
        float temp = 1-t;
        point.x = p0.x*temp*temp+2*p1.x*t*temp+p2.x*t*t;
        point.y = p0.y*temp*temp+3*p1.y*t*temp+p2.y*t*t;
        return point;
    }

    /**
     * B(t) = (1-t)^3*P0+3t*(1-t)^2*P1+3t^2*(1-t)*P2+t^3*P3,t∈[0,1]
     *
     * @param t 曲线长度比例
     * @param p0 起始点
     * @param p1 控制点1
     * @param p2 控制点2
     * @param p3 终止点
     * @return 对应点
     * */
    public static PointF CalculateBezierPointForCubic(float t,PointF p0,PointF p1,PointF p2,PointF p3){
        PointF point = new PointF();
        float temp = 1-t;
        point.x = p0.x*temp*temp*temp+3*p1.x*t*temp*temp+3*p2.x*t*t*temp+p3.x*t*t*t;
        point.y = p0.y*temp*temp*temp+3*p1.y*t*temp*temp+3*p2.y*t*t*temp+p3.y*t*t*t;
        return point;
    }
}

```

再准备一个值变化器
BezierEvaluator.java
```java
public class BezierEvaluator implements TypeEvaluator<PointF> {
    //控制点
    private PointF fPoint;

    public BezierEvaluator(PointF fPoint) {
        this.fPoint = fPoint;
    }

    @Override
    public PointF evaluate(float fraction, PointF startValue, PointF endValue) {

        return BezierUtil.CalculateBezierPointForQuadratic(fraction,startValue,fPoint,endValue);
    }
}

```

BezierPathView.java
```java
public class BezierPathView extends View implements View.OnClickListener {
    private float mStartPointX,mStartPointY;
    private float mEndPointX,mEndPointY;
    private float fPointX,fPointY;
    private float mPointX,mPointY;
    private Path mPath;
    private Paint mPaint,mCirclePaint;

    public BezierPathView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        mStartPointX = 100;
        mStartPointY = 100;
        mEndPointX = 600;
        mEndPointY = 600;
        fPointX = 500;
        fPointY = 0;
        mPath = new Path();
        mPaint = new Paint();
        mPaint.setStyle(Paint.Style.STROKE);
        mPaint.setStrokeWidth(8);
        mPointX = mStartPointX;
        mPointY = mStartPointY;

        mCirclePaint = new Paint();
        mCirclePaint.setStyle(Paint.Style.FILL);
        mCirclePaint.setColor(Color.GREEN);

        setOnClickListener(this);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        mPath.reset();
        mPath.moveTo(mStartPointX,mStartPointY);
        mPath.quadTo(fPointX,fPointY,mEndPointX,mEndPointY);
        canvas.drawPath(mPath,mPaint);
        canvas.drawCircle(mPointX,mPointY,50,mCirclePaint);
    }

    @Override
    public void onClick(View v) {
        BezierEvaluator evaluator = new BezierEvaluator(new PointF(fPointX,fPointY));
        ValueAnimator animator = ValueAnimator.ofObject(evaluator,
                new PointF(mStartPointX,mStartPointY),
                new PointF(mEndPointX,mEndPointY));
        animator.setRepeatCount(ValueAnimator.INFINITE);
        animator.setDuration(1000);
        animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
            @Override
            public void onAnimationUpdate(ValueAnimator animation) {
                PointF pointF = (PointF)animation.getAnimatedValue();
                mPointX = (int)pointF.x;
                mPointY = (int)pointF.y;
                invalidate();
            }
        });
        animator.setInterpolator(new AccelerateDecelerateInterpolator());
        animator.start();
    }
}

```
## setShadowLayer与阴影效果
正常的Button添加阴影效果可使用layer-list的资源文件进行设置图层叠加： 
```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true">
        <!-- 灰色阴影 -->
        <layer-list>
            <item
                android:left="2dp"
                android:top="4dp">
                <shape>
                    <solid android:color="@android:color/darker_gray" />
                    <corners android:radius="4dp" />
                </shape>
            </item>

            <!-- 红色前景 -->
            <item
                android:bottom="4dp"
                android:right="2dp">
                <shape>
                    <solid android:color="#FF0000" />
                    <corners android:radius="4dp" />
                </shape>
            </item>
        </layer-list>

    </item>

    <item>

        <!-- 灰色阴影 -->
        <layer-list>
            <item
                android:left="2dp"
                android:top="4dp">
                <shape>
                    <solid android:color="@android:color/darker_gray" />
                    <corners android:radius="4dp" />
                </shape>
            </item>

            <!-- 白色前景 -->
            <item
                android:bottom="4dp"
                android:right="2dp">
                <shape>
                    <solid android:color="#FFFFFF" />
                    <corners android:radius="4dp" />
                </shape>
            </item>
        </layer-list>

    </item>
</selector>
```

然后在背景属性设置即可。  
而图片和文字的阴影效果需要借助Android的setShadowLayer()函数。  
setShadowLayer()函数能实现：  
- 定制阴影模糊程度  
- 定制阴影偏移距离  
- 清除和显示阴影  

#### setShadowLayer()构造函数
```java
public void setShadowLayer(float radius,float dx,float dy,int color)
```
参数:   
- float radius：模糊半径，radius越大越模糊，越小越清晰，如果为0，阴影消失。
- float dx：阴影横向偏移距离，正值向右，负值向左。
- float dy：阴影的纵向偏移距离，正值向下，赋值向上。
- int color：绘制阴影的画笔颜色(对图片阴影无效)

因为用的高斯模糊算法，产生阴影的算法受色彩影响，所以第四个参数对图片设置无效。  

注意：只有文字绘制阴影支持硬件加速，最好在自定义控件中禁止硬件加速。  
```java
public class ShadowLayerView extends View {
    private Paint mPaint = new Paint();
    private Bitmap syBmp;

    public ShadowLayerView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        setLayerType(LAYER_TYPE_SOFTWARE,null);
        mPaint.setColor(Color.BLACK);
        mPaint.setTextSize(25);
        mPaint.setShadowLayer(1,60,60,Color.GRAY);
        syBmp = BitmapFactory.decodeResource(getResources(),R.drawable.lxw);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawColor(Color.WHITE);
        canvas.drawText("LXW",100,100,mPaint);
        canvas.drawCircle(300,100,50,mPaint);
        canvas.drawBitmap(syBmp,null,
                new Rect(30,250,30+syBmp.getWidth(),250+syBmp.getHeight()),mPaint);
    }
}

```

清除阴影  
```java
public void clearShadowLayer()
```

文字添加阴影的其他方法  
XML
shadowColor属性  

代码  
```java
public void setShadowLayer(float radius,float dx,float dy,int color)
```