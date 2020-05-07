---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'视图动画'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## 视图动画标签
Android的视图动画由5种类型组成:alpha、scale、translate、rotate、set。
#### 基本配置
1)配置XML动画文件  
- alpha:渐变透明度动画效果。
- scale:渐变尺寸伸缩动画效果。
- translate:画面变换位置移动动画效果。
- rotate:画面转移旋转动画效果。
- set:定义动画集。

2)存放位置
动画文件应存放在res/anim文件夹下，访问时使用R.anim.XXX，也可以存放在res/drawable文件夹下，访问时使用R.drawable.XXX。

🌰：
```java
textView.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
	Animation animation = AnimationUtils.loadAnimation(MainActivity.this,R.anim.text_anim);
	textView.startAnimation(animation);
	}
});
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android" android:duration="700">
    <scale
        android:fromXScale="0.0"
        android:toXScale="1.4"
        android:fromYScale="0.0"
        android:toYScale="1.4" />
</set>
```

#### scale标签  
scale标签用于缩放动画，可以实现动态调整控件尺寸的效果。

- android:fromXScale：动画起始时，控件在X轴方向上相对自身的缩放比例，浮点值。
- android:toXScale：动画结束时，控件在X轴方向上相对自身的缩放比例，浮点值。
- android:fromYScale：动画起始时，控件在Y轴方向上相对自身的缩放比例，浮点值。
- android:toYScale：动画结束时，控件在Y轴方向上相对自身的缩放比例，浮点值。
- android:pivotX：缩放起始点X轴坐标，可以是数值、百分数、百分数p三种样式，如50、50%、50%p。如果是数值，则表示在当前视图的原点处加上50px，作为缩放起始点X轴的坐标；如果是50%，则表示在当前控件的左上角加上自己宽度的50%作为缩放起始点X轴坐标；如果是50%p，则表示在当前控件左上角加上父控件宽度的50%作为缩放起始点X轴坐标
- android:pivotY:与android：pivotX相同。

注意：缩放是从缩放坐标为正中心向外进行缩放。

#### Animation 
所有的动画都继承自Animation类，是四种动画的基类，它没有自己的标签，但是它内部有四种动画的共有属性。

- android:duration：用于设置完成一次动画的持续时间，以毫秒为单位。
- android:fillAfter：如果设置为true，控件动画结束时，保持结束的状态。
- android:fillBefore：如果设置为true，则控件动画结束时，将还原到初始化状态。
- android:fillEnabled：与android:fillBefore相同
- android:repeatCount：用于指定动画的重复次数，取值为infinite时为无限循环。
- android:repeatMode：用于设定重复的类型，有reverse和restart两个值。其中，reverse表示倒序回放；restart表示重放，必须与repeatCount一起使用才能看到效果。
- android:interpolator：用于设定插值器，其实就是指定动画效果。

#### alpha标签
alpha标签用于实现透明度动画效果。

- android:fromAlpha：动画开始时的透明度，取值为0.0~1.0。0.0表示全透明。
- android:fromAlpha：动画结束时的透明度。

#### rotate标签
rotate标签用于实现画面转移旋转动画效果。

- android:fromDegrees：动画开始旋转时的角度位置，正值代表顺时针方向的度数。
- android:fromDegrees：动画结束旋转时的角度位置。
- android:pivotX
- android:pivotY

#### translate标签
translate标签用于实现画面变换位置移动动画效果。
- android:fromXDelta：起点X坐标，定义方式与pivotX相同
- android:fromYDelta：起点y坐标。
- android:toXDelta：终点x坐标。
- android:toYDelta：终点y坐标。

#### set标签
set标签是一个容器类标签，用于定义动画集。属性继承自Animation类。

注意：  
1.使用动画集合定义的属性会覆写子标签的一些属性，比如duration。
2.set标签中repeatCount无效，必须单个动画设置。

## 视图动画代码实现
XML形式添加动画提高了代码的复用性，但如果只是临时添加就没必要写动画文件了，可以使用代码实现动画操作。

标签对应类：
<table>
	<tr>
		<td>标签</td>
		<td>类</td>
	</tr>
	<tr>
		<td>scale</td>
		<td>ScaleAnimation</td>
	</tr>
	<tr>
		<td>scale</td>
		<td>ScaleAnimation</td>
	</tr>
	<tr>
		<td>alpha</td>
		<td>AlphaAnimation</td>
	</tr>
	<tr>
		<td>rotate</td>
		<td>RotateAnimation</td>
	</tr>
	<tr>
		<td>translate</td>
		<td>TranslateAnimation</td>
	</tr>
	<tr>
		<td>set</td>
		<td>SetAnimation</td>
	</tr>
</table>

Animation类的标签属性与方法的对应关系如下：
<table>
	<tr>
		<td>android:duration</td>
		<td>setDuration(long)</td>
	</tr>
	<tr>
		<td>android:fillAfter</td>
		<td>setFillAfter(boolean)</td>
	</tr>
	<tr>
		<td>android:fillBefore</td>
		<td>setFillBefore(boolean)</td>
	</tr>
	<tr>
		<td>android:fillEnable</td>
		<td>setFillEnabled(boolean)</td>
	</tr>
	<tr>
		<td>android:repeatCount</td>
		<td>setRepeatCount(int)</td>
	</tr>
	<tr>
		<td>repeatMode</td>
		<td>setRepeatMode(int)</td>
	</tr>
	<tr>
		<td>android:interpolator</td>
		<td>SetInterpolator(Interpolator)</td>
	</tr>
</table>

注意：setRepeatMode(int)取值为Animation.RESTART或者Animation.REVERSE,setRepeatCount(int)用于设置循环次数，当设置无限循环时参数为Animation.INFINITE。

#### ScaleAnimation
构造：
```java
ScaleAnimation(Context context,AttributeSet attrs)
ScaleAnimation(float fromX,float toX,float fromY,float toY)
ScaleAnimation(float fromX,float toX,float fromY,float toY,float pivotX,float pivotY)
ScaleAnimation(float fromX, float toX, float fromY, float toY,int pivotXType, float pivotXValue, int pivotYType, float pivotYValue)
```
第一个构造为从XML文件中加载动画，基本用不到。  
pivotX有三种取值样式，但在最后一个构造函数要具体指定三种取值类型：Animation.ABSOLUTE、Animation.RELATIVE_TO_SELF和Animation.RELATIVE_TO_PARENT。

#### AlphaAnimation
构造:
```java
AlphaAnimation(Context context,AttributeSet attrs)
AlphaAnimation(float fromAlpha,float toAlpha)
```

#### RotateAnimation
构造：
```java
RotateAnimation(Context context,AttributeSet attrs)
RotateAnimation(float fromDegrees,float toDegrees)
RotateAnimation(float fromDegrees,float toDegrees,float pivotX,float pivotY)
RotateAnimation(float fromDegrees, float toDegrees, int pivotXType, float pivotXValue,int pivotYType, float pivotYValue)
```

#### TranslateAnimation
构造：
```java
TranslateAnimation(Context context,AttributeSet attrs)
TranslateAnimation(float fromXDelta, float toXDelta, float fromYDelta, float toYDelta)
TranslateAnimation(int fromXType, float fromXValue, int toXType, float toXValue,int fromYType, float fromYValue, int toYType, float toYValue)
```

#### AnimationSet
```java
AnimationSet(Context context, AttributeSet attrs)
AnimationSet(boolean shareInterpolator)
```

shareInterpolator为true时，所有动画公用插值器，false则表示定义各自的插值器。

增加动画的函数：
```
public void addAnimation(Animation a)
```

#### Animation
Animation有一些函数：
取消动画
```java
void cancel()
```

重置控件到动画开始前状态
```
void reset()
```

设置动画监听
```java
animation.setAnimationListener(new Animation.AnimationListener() {
	@Override
	public void onAnimationStart(Animation animation) {
                
	}

	@Override
	public void onAnimationEnd(Animation animation) {

	}

	@Override
	public void onAnimationRepeat(Animation animation) {

	}
});
```

## 插值器
插值器用于控制动画的变化速率。  
系统提供了九个已经实现的插值器：
<table>
	<tr>
		<td>Interpolator class</td>
		<td>Resource ID</td>
	</tr>
	<tr>
		<td>AccelerateDecelerateInterpolator</td>
		<td>@android:anim/accelerate_decelerate_interpolator</td>
	</tr>
	<tr>
		<td>AccelerateInterpolator</td>
		<td>@android:anim/accelerate_interpolator</td>
	</tr>
	<tr>
		<td>AnticipateInterpolator</td>
		<td>@android:anim/anticipate_interpolator</td>
	</tr>
	<tr>
		<td>AnticipateOvershootInterpolator</td>
		<td>@android:anim/anticipate_overshoot_interpolator</td>
	</tr>
	<tr>
		<td>BounceInterpolator</td>
		<td>@android:anim/bounce_interpolator</td>
	</tr>
	<tr>
		<td>CycleInterpolator</td>
		<td>@android:anim/cycle_interpolator</td>
	</tr>
	<tr>
		<td>DecelerateInterpolator</td>
		<td>@android:anim/decelerate_interpolator</td>
	</tr>
	<tr>
		<td>LinearInterpolator</td>
		<td>@android:anim/linear_interpolator</td>
	</tr>
	<tr>
		<td>OvershootInterpolator</td>
		<td>@android:anim/overshoot_interpolator</td>
	</tr>
</table>

有两种引用方法，一种是直接用标签中的android:interpolator属性指定。另一种是通过setInterpolator()函数设置。

#### 动画示例
1.匀速加载动画
loading_anim.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android" 
    android:duration="2000" 
    android:repeatMode="restart" 
    android:interpolator="@android:anim/linear_interpolator">
    <rotate
        android:fromDegrees="0"
        android:toDegrees="360"
        android:pivotX="50%"
        android:pivotY="50%"
        android:repeatCount="infinite"/>
</set>
```

```java
ImageView imageView = findViewById(R.id.smile);
Animation animation = AnimationUtils.loadAnimation(this,R.anim.loading_anim);
imageView.setAnimation(animation);
animation.start();
```

## 逐帧动画
1）定义XML动画文件
XML需要定义在drawable文件夹下，根元素为animation-list。animation-list有一个android:onshot属性，true为执行一次。item元素代表一帧动画，android:duration为停留时间，单位为毫秒,android:drawable为图片资源。  
animations.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot="false">
    <item android:duration="200" android:drawable="@drawable/hanpi"/>
    <item android:duration="200" android:drawable="@drawable/hero"/>
</animation-list>
```

2）设置ImageView
```xml
<ImageView
        android:id="@+id/smile"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/animations"/>
```

3)开始动画
```java
ImageView imageView = findViewById(R.id.smile);
AnimationDrawable anim = (AnimationDrawable) imageView.getDrawable();
anim.start();
```

src设置的部分也可改成background，获取的时候方法就变成了imageView.getBackground()。

#### AnimationDrawable类
AnimationDrawable有以下几个常用函数：  
- void start()：开始播放逐帧动画。
- void stop()：停止播放逐帧动画。
- int getDuration(int index)：得到指定index的帧的持续时间。
- Drawable getFrame(int index)：得到指定index的帧所对应的Drawable对象。
- int getNumberOfFrames()：得到当前AnimationDrawable的所有帧数量。
- boolean isRunning()：判断当前AnimationDrawable是否正在播放。
- boolean isOneShot()：判断当前AnimationDrawable是否执行一次，true为执行一次。
- void addFrame(Drawable frame,int duration)：为AnimationDrawable添加一帧，并设置持续时间。

注：通过文件名拿到资源ID

```java
int id = getResources().getIdentifier("hero","drawable",getPackageName());
```

getIdentifier()完整声明如下：
```java
int getIdentifier(String name,String defType,String defPackage)
```

String name：资源id名。
String defType：资源所在文件类型。
String defpackage：应用包名。