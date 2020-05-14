---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'属性动画进阶'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## 两个需要补充的类
ValueAnimator和ObejectAnimator的创建方法除了ofInt()、ofFloat()、ofObject()三个函数外，还有一个函数：
```java
//ValueAnimator的
public static ValueAnimator ofPropertyValuesHolder(PropertyValuesHolder... values)

//ObejectAnimator的
public static ObejectAnimator ofPropertyValuesHolder(Object target,PropertyValuesHolder... values)
```

#### PropertyValuesHolder
因为ValueAnimator，这里就不讲了。
PropertyValuesHolder类在Android中是用来保存动画过程中需要操作的属性与对应的值。ofFloat()之类的函数内部实现就是用PropertyValuesHolder来保存动画状态的。  

这里的方法适配API11以上的设备。   

创建PropertyValuesHolder实例的函数有四个：
```java
public static PropertyValuesHolder ofInt(String propertyName, int... values)
ublic static PropertyValuesHolder ofFloat(String propertyName, float... values)
public static PropertyValuesHolder ofObject(String propertyName, TypeEvaluator evaluator,
            Object... values)
public static PropertyValuesHolder ofKeyframe(String propertyName, Keyframe... values)
```

1）ofInt和ofFloat    
构造：  
```java
public static PropertyValuesHolder ofInt(String propertyName, int... values)
ublic static PropertyValuesHolder ofFloat(String propertyName, float... values)
```
- propertyName：表示ObjectAnimator需要操作的属性名。通过反射查找对应属性的set函数。  
- values：属性所对应的参数，同样是可变长参数，可指定多个。如果只指定了一个，就会从get函数获取初始值。

2）ofPropertyValuesHolder()  
ObjectAnimator给我们提供了一个设置ofPropertyValuesHolder实例的入口。
```java
public static ObejectAnimator ofPropertyValuesHolder(Object target,PropertyValuesHolder... values)
```
- target：需要执行动画的控件
- values：可变长参数，可以传入多个PropertyValuesHolder实例。

🌰文字抖动动画：
```java
TextView textView = findViewById(R.id.textView);
PropertyValuesHolder rotationHolder = PropertyValuesHolder.ofFloat("rotation",0f,60f,-60f,30f,-30f,0f);
PropertyValuesHolder alphaHolder = PropertyValuesHolder.ofFloat("alpha",1f,0f,1f,0f,1f);
ObjectAnimator objectAnimator = ObjectAnimator.ofPropertyValuesHolder(textView,rotationHolder,alphaHolder);
objectAnimator.setDuration(4000);
objectAnimator.setRepeatMode(ValueAnimator.RESTART);
objectAnimator.setRepeatCount(ValueAnimator.INFINITE);
objectAnimator.start();
```

3）ofObject  
构造：  
```java
public static PropertyValuesHolder ofObject(String propertyName, TypeEvaluator evaluator,
            Object... values)
```
- propertyName：ObjectAnimator动画操作的属性名。
- evaluator：Evaluator实例。根据动画进度算出值。
- values：可变长参数，操作动画属性的值。

🌰A~Z文字变换：
```java
MyTextView textView = findViewById(R.id.textView);
PropertyValuesHolder charHolder = PropertyValuesHolder.ofObject("charText",new CharEvaluator(),new Character('A'),new Character('Z'),new Character('['));
ObjectAnimator animator = ObjectAnimator.ofPropertyValuesHolder(textView,charHolder);
animator.setDuration(10000);
animator.setInterpolator(new AccelerateInterpolator());
animator.setRepeatMode(ValueAnimator.RESTART);
animator.setRepeatCount(ValueAnimator.INFINITE);
animator.start();
```

MyTextView.java
```java
public class MyTextView extends AppCompatTextView {
	public MyTextView(Context context, @Nullable AttributeSet attrs) {
		super(context, attrs);
	}
	public void setCharText(Character charText){
		setText(String.valueOf(charText));
	}
}
```

CharEvaluator.java
```java
class CharEvaluator implements TypeEvaluator<Character> {

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

#### Keyframe
之前我们控制动画速率都是用自定义插值器Evaluator的方式，为了简化控制的代码，我们可以用Keyframe类实现关键帧的方式定制速率。  
一个关键帧包含两个元素：时间点与位置：
```java
public static Keyframe ofFloat(float fraction,float value)
```
- fraction：表示当前显示进度，即getInterpolation()函数的返回值。
- value：表示动画当前所在的数值位置。

```java
TextView textView = findViewById(R.id.textView);
Keyframe frame0 = Keyframe.ofFloat(0f,-20f);
Keyframe frame1 = Keyframe.ofFloat(0.5f,0f);
Keyframe frame2 = Keyframe.ofFloat(1f,20f);
PropertyValuesHolder charHolder = PropertyValuesHolder.ofKeyframe("rotation",frame0,frame1,frame2);
ObjectAnimator animator = ObjectAnimator.ofPropertyValuesHolder(textView,charHolder);
animator.setDuration(1000);
animator.setInterpolator(new AccelerateInterpolator());
animator.setRepeatMode(ValueAnimator.REVERSE);
animator.setRepeatCount(ValueAnimator.INFINITE);
animator.start();
```

第一步，生成Keyframe对象，定义关键帧
第二步，用PropertyValuesHolder.ofKeyframe生成PropertyValuesHolder对象
第三步，用ObjectAnimator.ofPropertyValuesHolder生成对应的Animator

ofFloat和ofInt
```
//ofFloat
public static Keyframe ofFloat(float fraction)
public static Keyframe ofFloat(float fraction,float value)

//ofInt
public static Keyframe ofInt(float fraction)
public static Keyframe ofInt(float fraction,int value)

//ofObject
public static Keyframe ofObject(float fraction)
public static Keyframe ofObject(float fraction,Object value)

```

set函数
```
//设置当前进度
public void setFraction(float fraction)

//设置当前keyframe对应值
public void setValue(Object value)

//设置插值器
//public void setInterpolator(TimeInterpolator interpolator)
```

🌰ofObject的例子：
```java
MyTextView textView = findViewById(R.id.textView);
Keyframe frame0 = Keyframe.ofObject(0f,new Character('A'));
Keyframe frame1 = Keyframe.ofObject(0.1f,new Character('L'));
Keyframe frame2 = Keyframe.ofObject(1f,new Character('['));
PropertyValuesHolder charHolder = PropertyValuesHolder.ofKeyframe("charText",frame0,frame1,frame2);
charHolder.setEvaluator(new CharEvaluator());
ObjectAnimator animator = ObjectAnimator.ofPropertyValuesHolder(textView,charHolder);
animator.setDuration(10000);
animator.setInterpolator(new AccelerateInterpolator());
animator.setRepeatMode(ValueAnimator.RESTART);
animator.setRepeatCount(ValueAnimator.INFINITE);
animator.start();
```
MyTextView和CharEvaluator上面有。

注意：  
- 去掉第一帧时，则以第一个关键帧作为起始位置。
- 去掉最后一帧时，则以最后一个关键帧作为结束位置。
- 使用Keyframe来构建动画，至少要有2帧。

其他函数
```
//设置动画的Evaluator
public void setEvaluator(TypeEvaluator evaluator)

//用于设置ofFloat()所对应的动画值列表
public void setFloatValues(float... values)

//用于设置ofInt()所对应的动画值列表
public void setIntValues(int... values)

//用于设置ofkeyframe()所对应的动画值列表
public void setKeyframes(Keyframe... values)

//用于设置ofObject()所对应的动画值列表
public void setObjectValues(Object... values)

//设置动画属性名
public void setPropertyName(String propertyName)
```

## ViewPropertyAnimator
Android3.0引入的属性动画，新增的针对属性的set/get函数，但是使用上还是没有达到简便的要求，所以在Android3.1中，谷歌补充了ViewPropertyAnimator类。
原来：
```java
ObjectAnimator animator = ObjectAnimator.ofFloat(textView,"alpha",0f);
animator.start();
```

ViewPropertyAnimator：
```java
textView.animate().alpha(0f);
```

注意：  
- animate()：从View的animate()方法开始。函数会返回一个ViewPropertyAnimator对象。
- 自动开始：声明完毕即开始动画。
- 方法调用都会返回ViewPropertyAnimator实例，能串联多个函数。

#### 常见函数
<table>
	<tr>
		<td>函数</td>
		<td>含义</td>
	</tr>
	<tr>
		<td>alpha(float value)</td>
		<td>设置透明度</td>
	</tr>
	<tr>
		<td>scaleY(float value)</td>
		<td>设置Y轴方向的缩放大小</td>
	</tr>
	<tr>
		<td>scaleX(float value)</td>
		<td>设置X轴方向的缩放大小</td>
	</tr>
	<tr>
		<td>translationY(float value)</td>
		<td>设置Y轴方向的移动量</td>
	</tr>
	<tr>
		<td>translationX(float value)</td>
		<td>设置X轴方向的移动量</td>
	</tr>
	<tr>
		<td>rotation(float value)</td>
		<td>设置绕Z轴方向旋转角度</td>
	</tr>
	<tr>
		<td>rotationY(float value)</td>
		<td>设置绕Y轴方向旋转角度</td>
	</tr>
	<tr>
		<td>rotationX(float value)</td>
		<td>设置绕X轴方向旋转角度</td>
	</tr>
	<tr>
		<td>x(float value)</td>
		<td>相对于父容器左上角坐标在X轴方向的最终位置</td>
	</tr>
	<tr>
		<td>y(float value)</td>
		<td>相对于父容器左上角坐标在Y轴方向的最终位置</td>
	</tr>
	<tr>
		<td>alphaBy(float value)</td>
		<td>设置透明度增量</td>
	</tr>	
	<tr>
		<td>rotationBy(float value)</td>
		<td>设置绕Z轴旋转增量</td>
	</tr>	
	<tr>
		<td>rotationXBy(float value)</td>
		<td>设置绕X轴旋转增量</td>
	</tr>	
	<tr>
		<td>rotationYBy(float value)</td>
		<td>设置绕Y轴旋转增量</td>
	</tr>	
	<tr>
		<td>translationXBy(float value)</td>
		<td>设X轴方向的移动值增量</td>
	</tr>	
	<tr>
		<td>translationYBy(float value)</td>
		<td>设设Y轴方向的移动值增量</td>
	</tr>	
	<tr>
		<td>scaleXBy(float value)</td>
		<td>设设X轴方向的缩放大小增量</td>
	</tr>
	<tr>
		<td>scaleYBy(float value)</td>
		<td>设设Y轴方向的缩放大小增量</td>
	</tr>
	<tr>
		<td>xBy(float value)</td>
		<td>相对于父容器左上角坐标在X轴方向的位置增量</td>
	</tr>
	<tr>
		<td>yBy(float value)</td>
		<td>相对于父容器左上角坐标在y轴方向的位置增量</td>
	</tr>
	<tr>
		<td>setInterpolator(TimeInterpolator interpolator)</td>
		<td>设置插值器</td>
	</tr>
	<tr>
		<td>setStartDelay(long startDelay)</td>
		<td>设置开始延时</td>
	</tr>
	<tr>
		<td>setDuration(long duration)</td>
		<td>设置动画时长</td>
	</tr>
</table>

#### 性能考量
ViewPropertyAnimator没有像ObjectAnimator一样使用反射或者JNI技术。ViewPropertyAnimator会根据预设的每一个动画帧算出对应所有属性，并设置给控件，然后调用一次invalidate()函数进行重绘，解决了使用ObjectAnimator时每个属性单独计算、单独重绘的问题。

所以二者的区别在于，ObjectAnimator可以更灵活的为任何对象和属性做动画。但是需要为View多个属性(SDK提供的，非自由拓展的)做动画时，ViewPropertyAnimator会更方便。

## 为ViewGroup内的组件添加动画
为listView之类的拥有多个条目的控件，Android提供了四种方法。  
1）layoutAnimation标签与LayoutAnimationController
layoutAnimation标签在API1就引入了，专门针对listView添加入场动画使用，LayoutAnimationController时它的代码实现。但是创建完成后再添加的数据不会有入场动画。  

2）gridLayoutAnimation标签与GridLayoutAnimationController
gridLayoutAnimation标签也是在API1引入的，专门针对gridview添加入场动画使用。GridLayoutAnimationController是它的代码实现。同样添加的数据不会有入场动画。

3）android:animateLayoutChanges属性
在API11引入，属性值为boolean类型，所有派生自此ViewGroup类的控件都具有此属性，添加删除都有默认动画，无法自定义。

4）LayoutTransition
在API11引入，可以实现在ViewGroup动态添加删除动画，可以自定义。

🌰android:animateLayoutChanges：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/add"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="add"/>
    <Button
        android:id="@+id/remove"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="remove"/>
    <LinearLayout
        android:id="@+id/container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:animateLayoutChanges="true"
        android:orientation="vertical"/>
</LinearLayout>
```


```java
public class MainActivity extends AppCompatActivity {

    LinearLayout container;
    Button add,remove;
    int i = 0;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        container = findViewById(R.id.container);
        add = findViewById(R.id.add);
        remove = findViewById(R.id.remove);

        add.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                addTextView();
            }
        });

        remove.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                removeTextView();
            }
        });

    }

    private void addTextView(){
        i++;
        TextView textView = new TextView(this);
        textView.setText("Robot"+i);
        LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(ViewGroup.LayoutParams.WRAP_CONTENT,
                ViewGroup.LayoutParams.WRAP_CONTENT);
        textView.setLayoutParams(params);
        container.addView(textView);
    }

    private void removeTextView(){
        if(i>0){
            container.removeViewAt(0);
        }
        i--;
    }
}
```

🌰LayoutTransition:
```java
//第一步：构造
LayoutTransition transition = new LayoutTransition();

//第二步：创建动画并设置
ObjectAnimator animIn = ObjectAnimator.ofFloat(null,"alpha",0f,1f);
transition.setAnimator(LayoutTransition.APPEARING,animIn);

ObjectAnimator animOut = ObjectAnimator.ofFloat(null,"rotation",0f,90f,0f);
transition.setAnimator(LayoutTransition.DISAPPEARING,animOut);

//将LayoutTransition设置到ViewGroup中
container.setLayoutTransition(transition);
```
其他代码同上。

第二步的第一个参数为设置动画的类型，共有四种：
- APPEARING：元素在容器中出现时所定义的动画。
- DISAPPEARING：元素在容器中消失时所定义的动画。
- CHANGE_APPEARING：由于容器中要显现一个新的元素，其他需要变化的元素所用的动画。
- CHANGE_DISAPPEARING：由于容器中要显现一个新的元素，其他需要变化的元素所用的动画。

CHANGE_类型  
这种类型不常用，而且会出问题，不知道我的CHANGE_APPEARING出了啥问题反正就是用不了，迷的一逼。点快了还会有组件缺失的情况，不建议使用。

注意：  
- 只能用PropertyValuesHolder构造。
- "left"、"top"必须要写。
- 动画的第一个值和最后一个必须相等。
- 所有参数值不能都相同

```java
PropertyValuesHolder pvhLeft =
                PropertyValuesHolder.ofInt("left", 0,0);
PropertyValuesHolder pvhTop =
                PropertyValuesHolder.ofInt("top", 0,0);
PropertyValuesHolder anim1 =
	PropertyValuesHolder.ofFloat("scaleX",1f,0f,1f);
Animator animIn = ObjectAnimator.ofPropertyValuesHolder(container,pvhLeft,pvhTop,anim1);
transition.setAnimator(LayoutTransition.CHANGE_DISAPPEARING,animIn);
```

#### 其他函数
LayoutTransition类的其他函数：
```java
//所有动画完成所需要的时长
public void setDuration(long duration)
//针对单个Type设置动画时长
public void setDuration(int transitionType,long duration)
//针对单个Type设置插值器
public void setInterpolator(int transitionType,TimeInterpolator interpolator)
//针对单个Type设置动画延时
public void setStartDelay(int transitionType,long delay)
//针对单个Type设置每个子item动画的时间间隔。
public void setStagger(int transitionType,long duration)
```

设置监听：
```java
public void addTransitionListener(TransitionListener listener)

public interface TransitionListener{
	public void startTransition(LayoutTransition transition, ViewGroup container,
                View view, int transitionType);
      
	public void endTransition(LayoutTransition transition, ViewGroup container,
                View view, int transitionType);
}
```

## NineOldAndroids开源动画库