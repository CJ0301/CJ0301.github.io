---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'属性动画'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## ValueAnimator
在Android中，动画分为两类：视图动画(View Animation)和属性动画(Property Animation)。其中视图动画包括补间动画与逐帧动画；属性动画中包括ValueAnimator和ObjectAnimator。

视图动画与属性动画的三点不同：
1. 引入时间不同：View Animation是在API Level 1引入的；而Property Animation是在API Level 11时引入的，即从Android3.0才有相关的API。
2. 包名不同：View Animation API在android.view.animation包中，而Property Animation API在android.animation包中。
3. 动画的命名不同，View Animation中的动画类都是XXXAnimation，而Property Animation中的动画类命名都是XXXAnimator。

区别：视图动画仅能对指定控件做动画，而属性动画是通过改变控件的某一属性来做动画的。

🌰：
给TextView附加平移的补间动画并加入单击弹出Toast的方法，动画结束后会发现，变换后的位置单击后没有反应，只有在原位置单击才有反应。

#### 简单使用
1）创建实例
```java
ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);
animator.start();
```

2）添加监听事件
```java
ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);

animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation) {
    	int curValue = (Integer)animation.getAnimatedValue();
        Log.i("xxxxx",curValue+"");
	}
});

animator.start();
```

从打印内容可以看到，ValueAnimator的功能是对指定区间进行动画运算，通过对运算过程的监听来自己操作控件，总结出来就两点：
- ValueAnimator只负责对指定值区间进行动画运算。
- 我们需要对运算过程进行监听，然后自己对控件执行动画操作。

使用案例：

```java
final ImageView imageView = findViewById(R.id.smile);
Button button = findViewById(R.id.click);
final ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);

animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation){
		int curValue = (Integer)animation.getAnimatedValue();
		imageView.layout(curValue,curValue,curValue+imageView.getWidth(),curValue+imageView.getHeight());
	}
});

imageView.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		Toast.makeText(MainActivity.this,"click",Toast.LENGTH_SHORT).show();
	}
});

button.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		animator.start();
	}
});
```

这样变换位置原组件的点击事件是有效的。

#### 常见函数
1）offInt()与ofFloat()函数
```java
public static ValueAnimator ofInt(int... values)
public static ValueAnimator ofFloat(float... values)
```
他们的参数都是可变长参数，传进去的值就是动画的变化范围，比如ofInt(2,90,45)就表示从2变到90再变到45。

2）获取监听点
```
Object getAnimatedValue();
```

因为返回值为Object类型，所以获取时得转换类型。

3）常用函数汇总
```java
//设置时长
ValueAnimator setDuration(long duration)

//开始动画
void start()

//设置循环次数，INFINITE表示无限循环。
void setRepeatCount(int value)

//设置循环模式，取值有RESTART和REVERSE
void setRepeatMode(int value)

//取消动画
void cancel()
```

#### 添加与移除监听器
1）添加监听器
ValueAnimator有两个监听器：
```java
/*
* 监听动画中值的变化
* 添加方法：public void addUpdateListener
*     (AnimatorUpdateListener listener)
*/
public static interface AnimatorUpdateListener{
	void onAnimationUpdate(ValueAnimator animation);
}

/*
* 监听动画变化的四个状态
* 添加方法：public void addListener
*     (AnimatorListener listener)
*/
public static interface AnimatorListener{
	void onAnimationStart(Animator animation);
	void onAnimationEnd(Animator animation);
	void onAnimationCancel(Animator animation);
	void onAnimationRepeat(Animator animation);
}

```

2）移除监听器
```java
//移除AnimatorUpdateListener
void removeUpdateListener(AnimatorUpdateListener listener);
void removeAllUpdateListeners();

//移除AnimatorListener
void removeListener(AnimatorListener listener);
void removeAllListeners();
```

#### 不常用函数
```java
//延时开始
public void setStartDelay(long startDelay)

//完全克隆一个ValueAnimator,包括所有设置与监听
public ValueAnimator clone()

```

#### 例子
```java
public class LoadingImageView extends AppCompatImageView {
    private int mTop;

    public LoadingImageView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    @Override
    protected void onLayout(boolean changed, int left, int top, int right, int bottom) {
        super.onLayout(changed, left, top, right, bottom);
        mTop = top;
    }

    //当前动画图片索引
    private int mCurImgIndex = 0;
    //动画图片总张数
    private static int mImageCount = 2;

    private void init(){
        ValueAnimator valueAnimator = ValueAnimator.ofInt(0,100,0);
        valueAnimator.setRepeatMode(ValueAnimator.RESTART);
        valueAnimator.setRepeatCount(ValueAnimator.INFINITE);
        valueAnimator.setDuration(2000);
        valueAnimator.setInterpolator(new AccelerateDecelerateInterpolator());

        valueAnimator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
            @Override
            public void onAnimationUpdate(ValueAnimator animation) {
                Integer dx = (Integer)animation.getAnimatedValue();
                setTop(mTop-dx);
            }
        });

        valueAnimator.addListener(new Animator.AnimatorListener() {
            @Override
            public void onAnimationStart(Animator animation) {

            }

            @Override
            public void onAnimationEnd(Animator animation) {

            }

            @Override
            public void onAnimationCancel(Animator animation) {

            }

            @Override
            public void onAnimationRepeat(Animator animation) {
                mCurImgIndex++;
                switch (mCurImgIndex % mImageCount){
                    case 0:
                        setImageDrawable(getResources().getDrawable(R.drawable.pic1));
                        break;

                    case 1:
                        setImageDrawable(getResources().getDrawable(R.drawable.pic2));
                        break;
                }
            }
        });

        valueAnimator.start();
    }
}
```

## 插值器
在视图动画中，我们可以通过setInterpolator()函数来设置插值器；而Animator不仅可以设置插值器，还可以设置Evaluator。

1)自定义插值器  
Interpolator  
自定义的插值器需继承TimeInterpolator接口，里面只有一个函数
```java
public interface TimeInterpolator{
	float getInterpolation(float input)
}
```  
- 参数input：input参数的取值为0~1，表示当前动画的进度，0表示开始，1表示结束。
- 返回值：当前实际想要显示的进度，取值可大于1小于0。

2)Evaluator  
在数值从ofInt到监听器返回时会经过四个步骤：  

<div class="mermaid">
graph LR
  A[OfInt 定义区间] --> B
  B[插值器 返回当前进度] --> C
  C[Evaluator 计算当前值] -->D[监听器返回]
</div>

因为返回值类型不同，Evaluator分为IntEvaluator和FloatEvaluator。  
IntEvaluator的内部实现：
```java
public class IntEvaluator implements TypeEvaluator<Integer> {
    public Integer evaluate(float fraction, Integer startValue, Integer endValue) {
        int startInt = startValue;
        return (int)(startInt + fraction * (endValue - startInt));
    }
}
```
evaluate方法的三个参数：  
- fraction参数就是插值器中的返回值，表示当前动画的数值进度，以百分制的小数表示。
- startValue和endValue分别对应ofInt(int start,int end)函数中的start和end的数值。
- 返回值就是我们在监听器中通过animation.getAnimatedValue()函数得到的数值。

3)ArgbEvaluator
ArgbEvaluator源码：
```java
public class ArgbEvaluator implements TypeEvaluator {
    private static final ArgbEvaluator sInstance = new ArgbEvaluator();

    @UnsupportedAppUsage
    public static ArgbEvaluator getInstance() {
        return sInstance;
    }

    public Object evaluate(float fraction, Object startValue, Object endValue) {
        int startInt = (Integer) startValue;
        float startA = ((startInt >> 24) & 0xff) / 255.0f;
        float startR = ((startInt >> 16) & 0xff) / 255.0f;
        float startG = ((startInt >>  8) & 0xff) / 255.0f;
        float startB = ( startInt        & 0xff) / 255.0f;

        int endInt = (Integer) endValue;
        float endA = ((endInt >> 24) & 0xff) / 255.0f;
        float endR = ((endInt >> 16) & 0xff) / 255.0f;
        float endG = ((endInt >>  8) & 0xff) / 255.0f;
        float endB = ( endInt        & 0xff) / 255.0f;

        // convert from sRGB to linear
        startR = (float) Math.pow(startR, 2.2);
        startG = (float) Math.pow(startG, 2.2);
        startB = (float) Math.pow(startB, 2.2);

        endR = (float) Math.pow(endR, 2.2);
        endG = (float) Math.pow(endG, 2.2);
        endB = (float) Math.pow(endB, 2.2);

        // compute the interpolated color in linear space
        float a = startA + fraction * (endA - startA);
        float r = startR + fraction * (endR - startR);
        float g = startG + fraction * (endG - startG);
        float b = startB + fraction * (endB - startB);

        // convert back to sRGB in the [0..255] range
        a = a * 255.0f;
        r = (float) Math.pow(r, 1.0 / 2.2) * 255.0f;
        g = (float) Math.pow(g, 1.0 / 2.2) * 255.0f;
        b = (float) Math.pow(b, 1.0 / 2.2) * 255.0f;

        return Math.round(a) << 24 | Math.round(r) << 16 | Math.round(g) << 8 | Math.round(b);
    }
}
```

## ofObject
ValueAnimator有一个函数ofObject()供我们自己定制任何类型的变量。
```java
public static ValueAnimator ofObject(TypeEvaluator evaluator,Object... values)
```

强制传入Evaluator是因为我们要做进度到值的转换过程。

#### 🌰从A~Z的加速动画：
CharEvaluator.java
```java
class CharEvaluator implements TypeEvaluator<Character>{

    @Override
    public Character evaluate(float fraction, Character startValue, Character endValue) {
        int startInt = (int)startValue;
        int endInt = (int)endValue;
        int curInt = (int)(startInt+fraction*(endInt-startInt));
        char result = (char)curInt;
        return result;
    }
}
```

MainActivity.java
```java
final TextView textView = findViewById(R.id.animate);
ValueAnimator animator = ValueAnimator.ofObject(new CharEvaluator(),new Character('A'),new Character('Z'));
animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation) {
	char text = (Character) animation.getAnimatedValue();
	textView.setText(String.valueOf(text));
	}
});
animator.setDuration(10000);
animator.setInterpolator(new AccelerateInterpolator());
animator.setRepeatMode(ValueAnimator.REVERSE);
animator.setRepeatCount(ValueAnimator.INFINITE);
animator.start();
```

#### 🌰自由落体动画：
```java
class FallEvaluator implements TypeEvaluator<Point>{
    private Point point = new Point();

    @Override
    public Point evaluate(float fraction, Point startValue, Point endValue) {
        point.x = (startValue.x+fraction*(endValue.x-startValue.x));
        float time = (float)Math.sqrt(endValue.y/5)*fraction;
        float y = 5*time*time;
        if(y<endValue.y){
            point.y = y;
        }else{
            point.y = endValue.y;
        }
        Log.i("point",point.x+"  "+point.y+"  "+time);
        return point;
    }
}


class Point{
    float x;
    float y;

    public Point() {
    }

    public Point(float x, float y) {
        this.x = x;
        this.y = y;
    }
}
```

```java
final ImageView imageView = findViewById(R.id.animate);
ValueAnimator animator = ValueAnimator.ofObject(new FallEvaluator(),new Point(0f,0f),new Point(500f,1600f));
animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation) {
	mCurPoint = (Point)animation.getAnimatedValue();
	imageView.layout((int)mCurPoint.x,(int)mCurPoint.y,(int)mCurPoint.x+imageView.getWidth(),(int)mCurPoint.y+imageView.getHeight());
	}
});
animator.setDuration(2000);
animator.start();

```

## ObjectAnimator
为了简化ValueAnimator的开发，使我们从监听动画过程中解法出来，谷歌在ValueAnimator的基础上派生了一个ObjectAnimator类。  
🌰改变透明度：
```java
ObjectAnimator animator1 = ObjectAnimator.ofFloat(imageView,"alpha",1,0,1);
animator1.setDuration(2000);
animator1.start();
```

从上面代码看，ObjectAnimator类少了添加监听的步骤。
- 第一个参数用于指定控件。
- 第二个参数用于指定操作属性。
- 第三个参数是可变长参数，指定属性值变化。

set函数  
ObjectAnimator的Of系列方法第二个参数本质上是去找相应控件中的set函数。同时每一个控件都从View继承了很多动画函数的set方法。
```java
//透明度
public void setAlpha(float alpha)

//旋转度数
public void setRotation(float rotation)
public void setRotationX(float rotationX)
public void setRotationY(float rotationY)

//平移
public void setTranslationX(float translateX)
public void setTranslationY(float translateY)

//缩放
public void setScaleX(float scaleX)
public void setScaleY(float scaleY)
```
1)旋转
- setRotation(float rotation)：绕z轴旋转，rotation表示旋转度数。
- setRotationX(float rotationX)：绕x轴旋转，rotationX表示旋转度数。
- setRotationY(float rotationY)：绕y轴旋转，rotationY表示旋转度数。

2)平移
- setTranslationX(float translationX)：x轴上的平移距离。
- setTranslationY(float translationY)：y轴上的平移距离。

3)缩放
- setScaleX(float scaleX)：在X轴上进行缩放，scaleX表示缩放倍数。
- setScaleY(float scaleY)：在y轴上进行缩放，scaleY表示缩放倍数。

#### 自定义ObjectAnimator属性
<div class="mermaid">
graph LR
  A[OfInt 定义区间] --> B
  B[插值器 返回当前进度] --> C
  C[Evaluator 计算当前值] -->D[调用set系列方法]
</div>
ObjectAnimator类与ValueAnimator类区别在于最后一步

🌰自由落体动画改写：  
小球
```java
public class Point{
    float x;
    float y;

    public Point() {
    }

    public Point(float x, float y) {
        this.x = x;
        this.y = y;
    }
}

```

插值器
```java
class FallEvaluator implements TypeEvaluator<Point>{
    private Point point = new Point();

    @Override
    public Point evaluate(float fraction, Point startValue, Point endValue) {
        point.x = (startValue.x+fraction*(endValue.x-startValue.x));
        float time = (float)Math.sqrt(endValue.y/5)*fraction;
        float y = 5*time*time;
        if(y<endValue.y){
            point.y = y;
        }else{
            point.y = endValue.y;
        }
        Log.i("point",point.x+"  "+point.y+"  "+time);
        return point;
    }
}
```

FallingBallImageView.java
```java
public class FallingBallImageView extends AppCompatImageView {
    public FallingBallImageView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
    }

    public void setFallingPos(Point pos){
        layout((int)pos.x,(int)pos.y,(int)pos.x+getWidth(),(int)pos.y+getHeight());
    }
}
```

```java
final FallingBallImageView imageView = findViewById(R.id.animate);
ObjectAnimator animator = ObjectAnimator.ofObject(imageView,"fallingPos",new FallEvaluator(),new Point(0f,0f),new Point(500f,1600f));
animator.setDuration(2000);
animator.setRepeatMode(ValueAnimator.RESTART);
animator.setRepeatCount(ValueAnimator.INFINITE);
animator.start();
```

注意：如果使用自定义属性的话，变长参数一定是两个，缺少一个值要定义一个getXXX函数作为默认值，而系统自带的旋转平移等操作都有默认值，只有一个参数的时候会调用。

常用函数和ValueAnimator一样，不多讲了。

## 组合动画
AnimatorSet类用来实现ValueAnimator和ObjectAnimator的组合动画。

#### playSequentially()和playTogether()
1)playSequentially()函数    
依次播放动画  
playSequentially()函数的声明如下：  
```java
public void playSequentially(Animator... items);
public void playSequentially(List<Animator> items);
```

2)playTogether()函数  
一起播放动画  
playTogether()函数的声明如下：
```java
public void playTogether(Animator... items);
public void playTogether(List<Animator> items);
```

注意：AnimatorSet没有设置循环的方法，只能在每个动画上自己设置。

#### AnimatorSet.Builder
这个类的存在是为了实现动画更自由的组合。  
🌰:
```java
AnimatorSet.Builder builder = animatorSet.play(animator1);
builder.with(animator2);
```

#### 常用函数
```java
//表示要播放哪个动画
public Builder play(Animator anim)
//和前面的动画一起执行
public Builder with(Animator anim)
//先执行这个动画，再执行前面的动画
public Builder before(Animator anim)
//在执行前面的动画后再执行该动画
public Builder after(Animator anim)
//延迟n毫秒之后执行动画
public Builder after(long delay)
```

```java
final FallingBallImageView imageView = findViewById(R.id.animate);
ObjectAnimator animator = ObjectAnimator.ofObject(imageView,"fallingPos",new FallEvaluator(),new Point(0f,0f),new Point(500f,1600f));
animator.setDuration(2000);

ObjectAnimator animator1 = ObjectAnimator.ofFloat(imageView,"alpha",1,0,1);
animator1.setDuration(2000);

ObjectAnimator animator2 = ObjectAnimator.ofFloat(imageView,"TranslationX",0f,200f);
animator2.setDuration(2000);
AnimatorSet animatorSet = new AnimatorSet();
AnimatorSet.Builder builder = animatorSet.play(animator);
builder.before(animator1).before(animator2);
animatorSet.start();
```

如果两个before两个before的动画会并到一起去，after也一样。

#### AnimatorSet监听器
监听器
```java
public static interface AnimatorListener{
	//AnimatorSet开始调用
	void onAnimationStart(Animator animation);

	//AnimatorSet结束时调用
	void onAnimationEnd(Animator animation);

	//Animator被取消时调用
	void onAnimationCancel(Animator animation);

	//当AnimatorSet重复调用时。由于Animator没设置重复函数，这个函数也不会被调用。
	void onAnimationRepeat(Animator animation);
}
```

添加方法：
```java
public void addListener(AnimatorListener listener);
```

注意：  
- AnimatorSet监听器只监听AnimatorSet的状态。  
- AnimatorSet监听器永远无法执行onAnimationRepeat函数。 


