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
```java
PathMeasure(Path path,boolean forceClosed);
```

forceClosed参数为true时，路径会被强制闭合。

简单函数使用  
```java
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

由此可看出，isClosed和getLength函数都是判断当前曲线。  nextContour得到的曲线顺序与添加顺序一致。  

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
```java
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
```java
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

getPosTan()函数用于得到路径上某一长度位置以及该位置的正切值  
```java
boolean getPosTan(float distance,float[] pos,float[] tan)
```
参数：  
- float distance：距离Path起始点的长度，取值范围为[0,getLength]。    
- float[] pos：该点的坐标值。当前点在画布上的位置有两个数值，pos[0]表示x坐标，pos[1]表示y坐标。  
- float[] tan：该点的正切值。  
 

```java
public class MyView extends View {
    private Paint mPaint;
    private Path mDstPath,mCirclePath;
    private PathMeasure mPathMeasure;
    private Float mCurAnimValue;
    private Bitmap mArrawBmp;
    private float[] pos = new float[2];
    private float[] tan = new float[2];

    public MyView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        setLayerType(LAYER_TYPE_SOFTWARE,null);

        mArrawBmp = BitmapFactory.decodeResource(getResources(),R.drawable.plant);

        mPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
        mPaint.setStyle(Paint.Style.STROKE);
        mPaint.setStrokeWidth(16);
        mPaint.setColor(Color.BLACK);

        mDstPath = new Path();
        mCirclePath = new Path();
        mCirclePath.addCircle(260,260,200,Path.Direction.CW);

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

        //plant
        mPathMeasure.getPosTan(stop,pos,tan);
        float degrees = (float) (Math.atan2(tan[1],tan[0])*180.0/Math.PI);
        Matrix matrix = new Matrix();
        matrix.postRotate(degrees,mArrawBmp.getWidth()/2,mArrawBmp.getHeight()/2);
        matrix.postTranslate(pos[0]-mArrawBmp.getWidth()/2,pos[1]-mArrawBmp.getHeight()/2);
        canvas.drawBitmap(mArrawBmp,matrix,mPaint);
    }
}
```

getMatrix()函数用于得到路径上某一长度的位置以及该位置的正切值矩阵。
```java
boolean getMatrix(float distance,Matrix matrix,int flags)
```
- distance：距离Path起始点的长度。  
- matrix：根据flags封装好的matrix会根据flag的设置存入不同的内容。  
- flags：用于指定哪些内容会存入matrix中。有两个值：  PathMeasure.POSITION_MATRIX_FLAG表示获取位置信息；  PathMeasure.TANGENT_MATRIX_FLAG表示获取切边信息。  


用getMatrix()函数来代替getPosTan()
```java
//plant
Matrix matrix = new Matrix();
mPathMeasure.getMatrix(stop,matrix,PathMeasure.POSITION_MATRIX_FLAG|
	PathMeasure.TANGENT_MATRIX_FLAG);
canvas.drawBitmap(mArrawBmp,matrix,mPaint);
```

## SVG动画
Android没有对原生的SVG语法支持，但可以使用path标签来实现。

#### 配置
AndroidX之后是不需要配置的，之前的版本需要配置一下。
```xml
compile 'com.android.support:appcompat-v7:23.2.0' //要求 appcompat-v7库的版本要在23.2.0+
```

修改gradle配置文件(gradle插件版本是2.0+)。
```
android {
  defaultConfig {
    vectorDrawables.useSupportLibrary = true
  }
}
```

#### vector标签与图像显示
vector标签有四个属性：  
- width、height：指定SVG图像高宽。  
- viewportWidth、viewportHeight：给图像画布划分坐标轴。  
🌰:  

```xml
<?xml version="1.0" encoding="utf-8"?>
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="200dp"
    android:height="100dp"
    android:viewportWidth="100"
    android:viewportHeight="50">
    <path
        android:name="bar"
        android:pathData="M50,23 L100,25"
        android:strokeWidth="2"
        android:strokeColor="@color/colorPrimary"/>
</vector>
```

#### path标签
1)常用属性
- android:name：声明一个标记，做动画的时候方便找。  
- android:pathData：对SVG矢量图的描述。  
- android:strokeWidth：画笔宽度。  
- android:fillColor：填充颜色。  
- android:fillAlpha：填充颜色的透明度。  
- android:strokeColor：描边颜色。  
- android:strokeWidth：描边宽度。  
- android:strokeAlpha：描边透明度。  
- android:strokeLineJoin：用于指定拐角形状，有miter(锐角)、round(圆弧)、bevel(直线)。  
- android:strokeMiterLimit：斜角上限。在strokeLineJoin为miter的时候有效，表示斜面长度与线条长度的比值，默认为10。  

2)android:trimPathStart属性  
该属性用于指定路径从哪开始，取值为0~1，表示路径开始位置的百分比。

3)android:trimPathEnd属性  
该属性用于指定路径从哪开始，取值为0~1，表示路径结束位置的百分比。

4)android:trimPathOffset属性  
该属性用于指定结果路径的位移距离，取值为0~1。取0不位移，取1位移整条路径长度。

5)android:pathData属性  
- M=moveto(M X,Y)：将画笔移动到指定的坐标位置。  
- L=lineto(L X,Y)：画直线到指定坐标位置。  
- H=horizontal lineto(H X)：画水平线到指定的X坐标位置。  
- V=vertical lineto(V Y)：画垂直线到指定的Y坐标位置。  
- C=curveto(C X1,Y1,X2,Y2,ENDX,ENDY)：三阶贝济埃曲线。  
- S=smooth curveto(S X2,Y2,ENDX,ENDY)：三阶贝济埃曲线，将上一个指令的终点作为起始点。  
- Q=quadratic Belzier curve(Q X,Y,ENDX,ENDY)：二阶贝济埃曲线。  
- T=smooth quadratic Belzier curve(T ENDX,ENDY)：映射前面路径后的终点。  
- A=elliptical Arc(A RX,RY,XROTATION,FLAG1,FLAG2,X,Y)：弧线。  
- Z=closepath()：关闭路径。  

A指令用来绘制一条弧线，且允许弧线不闭合。参数：    
- RX,RY指所有椭圆的半轴大小。  
- XROTATION指椭圆X轴和水平方向顺时针方向的夹角，可以想象成一个水平的椭圆绕中心点顺时针旋转XROTATION角度。  
- FLAG1只有两个值，1表示大角度弧度，0表示小角度弧度。  
- FLAG2只有两个值，确定从起始点到终点的方向，1表示顺时针，0表示逆时针。  
- X,Y为终点坐标。  

注意：
- 坐标轴以(0,0)为中心，X轴水平向右，Y轴水平向下。
- 所有指令大小写均可。大写表示绝对定位，参照全局坐标系，小写表示相对定位，参照父容器坐标系。
- 指令和数据之间的空格可以省略。
- 同一个指令出现多次可只用一个。

#### group标签
group标签可用于定义一系列路径或对路径进行分组。属性：  
- android:name：组的名字，用于与动画关联。  
- android:rotation：指定该组图像的旋转度数。  
- android:pivotX：定义缩放和旋转时的X参考点。相对于vector的viewport。  
- android:pivotY：定义缩放和旋转时的Y参考点。相对于vector的viewport。  
- android:scaleX：指定该组X缩放大小。  
- android:scaleY：指定该组Y缩放大小。  
- android:translateX：指定该组沿X轴平移的距离。  
- android:translateY：指定该组沿Y轴平移的距离。  

引入SVG图像的方法：    
1）在线转换  
[传送门](http://inloop.github.io/svg2android/)，如果404可能是更新了，工具在[传送门](http://inloop.github.io/)里有开源的。

2）Android Stdio引入(Android2.0以上)  
在drawable资源文件下右键，依次点击new->Vector Asset
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-05-23-svgToXml.png)

Clip Art就是Android自带的，Local file就是本地文件。其他属性就不细说了，反正英语也能看懂。

SVG图像使用：  
```xml
<ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:srcCompat="@drawable/ic_icon"/>
```

注意：  
- 如果ImageView使用不了，就看看继承的是否是AppCompatActivity。
- Button这类带状态的控件使用时注意要用selector去设置，然后属性为background。

添加动画：  
anim.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    android:propertyName="trimPathStart"
    android:valueFrom="0"
    android:valueTo="1"
    android:duration="2000" />
```

vector.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/ic_icon">

    <target
        android:animation="@animator/anim"
        android:name="icon"/>
</animated-vector>
```

target标签：  
- name：指定path名
- animation：指定动画

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ImageView imageView = (ImageView)findViewById(R.id.image);
        AnimatedVectorDrawableCompat compat = AnimatedVectorDrawableCompat
                .create(MainActivity.this,R.drawable.vector);
        imageView.setImageDrawable(compat);
        ((Animatable)imageView.getDrawable()).start();
    }
}
```

#### 输入搜索动画
activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/edit"
        android:hint="点击输入"
        android:layout_width="150dp"
        android:layout_height="24dp"
        android:background="@null"/>
    <ImageView
        android:id="@+id/anim_image"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</FrameLayout>
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        final ImageView imageView = (ImageView)findViewById(R.id.anim_image);

        //将焦点放在ImageView
        imageView.setFocusable(true);
        imageView.setFocusableInTouchMode(true);
        imageView.requestFocus();
        imageView.requestFocusFromTouch();
        EditText editText = findViewById(R.id.edit);

        editText.setOnFocusChangeListener(new View.OnFocusChangeListener() {
            @Override
            public void onFocusChange(View v, boolean hasFocus) {
                if(hasFocus){
                    AnimatedVectorDrawableCompat compat = AnimatedVectorDrawableCompat
                            .create(MainActivity.this,R.drawable.animated_vector);
                    imageView.setImageDrawable(compat);
                    ((Animatable)imageView.getDrawable()).start();
                }
            }
        });
    }
}
```

bar_anim.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    android:propertyName="trimPathStart"
    android:valueFrom="0"
    android:valueTo="1"
    android:valueType="floatType"
    android:duration="1500" />

```

search_anim.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    android:duration="1500"
    android:propertyName="trimPathEnd"
    android:valueFrom="0"
    android:valueTo="1"
    android:valueType="floatType"/>

```

animated-vector.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/ic_icon">

    <target
        android:animation="@animator/bar_anim"
        android:name="bar"/>
    <target
        android:animation="@animator/search_anim"
        android:name="search"/>
</animated-vector>
```

ic_icon.xml
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="150dp"
    android:height="24dp"
    android:viewportWidth="150"
    android:viewportHeight="24">

  <!--搜索图形-->
  <path
      android:name="search"
      android:pathData="M141,17 A9,9 0 1,1 142,16 L149,23"
      android:strokeWidth="2"
      android:strokeColor="@color/colorPrimary"/>

  <!--底部横线-->
  <path
      android:name="bar"
      android:trimPathStart="1"
      android:pathData="M0,23 L149,23"
      android:strokeWidth="2"
      android:strokeColor="@color/colorPrimary"/>
  </vector>

```

注意：  
- 使用objectAnimator加动画的时候注意是加给路径还是加给了组，有些属性是二者各自独有的。  
- 向下兼容问题：Android pre-L之前不能使用路径变换动画，不能自定义插值器。  

路径变换动画：
svg_apple.xml  
```xml
<?xml version="1.0" encoding="utf-8"?>
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="128dp"
    android:height="128dp"
    android:viewportWidth="520"
    android:viewportHeight="520">
    <group
        android:name="rotationGroup"
        android:pivotX="260"
        android:pivotY="260"
        android:rotation="0.0">

        <path
            android:name="v"
            android:strokeColor="#000000"
            android:strokeWidth="6"
            android:pathData="@string/svg_apple" />
    </group>
</vector>

```

svg_droid_for_apple.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="128dp"
    android:height="128dp"
    android:viewportWidth="520"
    android:viewportHeight="520">
    <group
        android:name="rotationGroup"
        android:pivotX="260"
        android:pivotY="260"
        android:rotation="0.0">

        <path
            android:name="v"
            android:strokeColor="#000000"
            android:strokeWidth="6"
            android:pathData="@string/svg_droid_for_apple" />
    </group>
</vector>

```

morph_apple_to_droid.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<objectAnimator
    xmlns:android="http://schemas.android.com/apk/res/android"

    android:duration="3500"
    android:propertyName="pathData"
    android:valueFrom="@string/svg_apple"
    android:valueTo="@string/svg_droid_for_apple"
    android:repeatMode="reverse"
    android:repeatCount="infinite"
    android:valueType="pathType" />
```

animated_vector_apple.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/svg_apple">


    <target
        android:name="v"
        android:animation="@animator/morph_apple_to_droid" />

</animated-vector>
```

activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    tools:context=".MainActivity">
    
    <ImageView
        android:id="@+id/image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:srcCompat="@drawable/animated_vector_apple"/>
</LinearLayout>
```

```java
ImageView imageView = findViewById(R.id.image);
Drawable drawable = imageView.getDrawable();

if(drawable instanceof Animatable)
	((Animatable) drawable).start();

```
问题1.Can't morph    
这个问题是因为两图复杂度不统一，无法相互转化。  
解决方法就是去下一个vectalign，统一一下路径。

低版本会有各种各样的问题，我这里最小sdk设置的是21，Android5.0以下的设备这种动画无法使用。

这里是Android官方的讲解[传输门](https://developer.android.com/studio/write/vector-asset-studio)和其中一个问题[传送门](https://stackoverflow.com/questions/27626831/error-while-trying-to-test-animatedvectordrawable-cant-morph-from-x-to-z)

总结：  
1. Bitmap的绘制效率并不一定会比Vector高 ，它们有-定的平衡点.当Vector比较简单时,其效率是一定比Bitmap高的,所以,为了保证Vector的高效率, Vector需要更加简单，PathData更加标准、精简,当Vector图像变得非常复杂时,就需要使用Bitmap来代替了  
2. Vector适用于ICON、Button. lmageView的图标等小的ICON .或者是需要的动画效果，由于Bitmap在GPU中有缓存功能,而Vector并没有,所以Vector图像不能做频繁的重绘  
3. Vector图像过于复杂时,不仅仅要注意绘制效率,初始化效率也是需要考虑的重要因素。  
4. SVG加载速度会快于PNG ,但渲染速度会慢于PNG .毕竟PNG有硬件加速.但平均下来,加载速度的提升弥补了绘利的速度缺陷。  

