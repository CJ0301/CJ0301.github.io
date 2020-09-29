---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'自定义控件基础'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## dp、sp和px
px:像素点  
dp:与像素密度密切相关  
sp:相当于dp(用来修饰文字)  

使用：  
文字尺寸一律用sp    
非文字尺寸一律用dp  
在屏幕上画细线作为分隔可以用px  

## LayoutInflater
LayoutInflater用于将xml文件解析成视图，相当于findViewById()。  

获得LayoutInflater实例的三种方法  
- getLayoutInflater()
- (LayoutInflater) getSystemService(LAYOUT_INFLATER_SERVICE)  
- LayoutInflater.from(Context context)

#### 使用
LayoutInfalter加载视图采用inflate方法
```java

public View inflate(@LayoutRes int resource, @Nullable ViewGroup root) {
        return inflate(resource, root, root != null);
}

public View inflate(XmlPullParser parser, @Nullable ViewGroup root) {
        return inflate(parser, root, root != null);
}

public View inflate(@LayoutRes int resource, @Nullable ViewGroup root, boolean attachToRoot) {
	final Resources res = getContext().getResources();
	if (DEBUG) {
		Log.d(TAG, "INFLATING from resource: \"" + res.getResourceName(resource) + "\" ("
			+ Integer.toHexString(resource) + ")");
	}

	View view = tryInflatePrecompiled(resource, res, root, attachToRoot);
	if (view != null) {
		return view;
	}
	XmlResourceParser parser = res.getLayout(resource);
	try {
		return inflate(parser, root, attachToRoot);
	} finally {
	parser.close();
	}
}

public View inflate(XmlPullParser parser, @Nullable ViewGroup root, boolean attachToRoot) {
	synchronized (mConstructorArgs) {
		Trace.traceBegin(Trace.TRACE_TAG_VIEW, "inflate");

		final Context inflaterContext = mContext;
		final AttributeSet attrs = Xml.asAttributeSet(parser);
		Context lastContext = (Context) mConstructorArgs[0];
		mConstructorArgs[0] = inflaterContext;
		View result = root;

		try {
			advanceToRootNode(parser);
			final String name = parser.getName();

			if (DEBUG) {
				System.out.println("**************************");
				System.out.println("Creating root view: "
				+ name);
				System.out.println("**************************");
			}

			if (TAG_MERGE.equals(name)) {
				if (root == null || !attachToRoot) {
					throw new InflateException("<merge /> can be used only with a valid "
						+ "ViewGroup root and attachToRoot=true");
				}

				rInflate(parser, root, inflaterContext, attrs, false);
			} else {
				// Temp is the root view that was found in the xml
				final View temp = createViewFromTag(root, name, inflaterContext, attrs);

				ViewGroup.LayoutParams params = null;

				if (root != null) {
					if (DEBUG) {
						System.out.println("Creating params from root: " +
						root);
					}
					// Create layout params that match root, if supplied
					params = root.generateLayoutParams(attrs);
					if (!attachToRoot) {
						// Set the layout params for temp if we are not
						// attaching. (If we are, we use addView, below)
						temp.setLayoutParams(params);
					}
				}

				if (DEBUG) {
					System.out.println("-----> start inflating children");
				}

				// Inflate all children under temp against its context.
				rInflateChildren(parser, temp, attrs, true);

				if (DEBUG) {
					System.out.println("-----> done inflating children");
				}

				// We are supposed to attach all the views we found (int temp)
				// to root. Do that now.
				if (root != null && attachToRoot) {
					root.addView(temp, params);
				}

				// Decide whether to return the root that was passed in or the
				// top view found in xml.
				if (root == null || !attachToRoot) {
					result = temp;
				}
			}

		} catch (XmlPullParserException e) {
		final InflateException ie = new InflateException(e.getMessage(), e);
			ie.setStackTrace(EMPTY_STACK_TRACE);
		throw ie;
		} catch (Exception e) {
			final InflateException ie = new 	InflateException(
				getParserStateDescription(inflaterContext, attrs)
				+ ": " + e.getMessage(), e);
			ie.setStackTrace(EMPTY_STACK_TRACE);
			throw ie;
		} finally {
			// Don't retain static reference on context.
			mConstructorArgs[0] = lastContext;
			mConstructorArgs[1] = null;

			Trace.traceEnd(Trace.TRACE_TAG_VIEW);
		}

		return result;
	}
}
```

一共有四个方法，有两个最终还是会调用有attachToRoot的方法，且默认值都是存在即捆绑。

这里的捆绑是个啥意思呢，用一个例子来体会一下。
这是一个MainActivity的视图，给LinearLayout一个id值，等会当容器用。
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/container"
    tools:context=".MainActivity"
    android:orientation="horizontal">
    
</LinearLayout>
```

这是一个普通的视图
linearlayout_for_test.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="wrap_content"
    android:layout_height="wrap_content">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="生成视图"
        android:textSize="26sp"/>
</LinearLayout>
```

如果attachToRoot为true，容器将直接添加视图。这个true如果有根容器也可以不加。
```java
LinearLayout ll = findViewById(R.id.container);
LayoutInflater layoutInflater = LayoutInflater.from(this);
layoutInflater.inflate(R.layout.linearlayout_for_test,ll,true);
```

若为false，则需要自己用addView添加。
```java
LinearLayout ll = findViewById(R.id.container);
LayoutInflater layoutInflater = LayoutInflater.from(this);
View view = layoutInflater.inflate(R.layout.linearlayout_for_test,ll,false);
ll.addView(view);
```

这个XmlPullParser的就是自定义解析器，现在还用不到，等用到了再更。

## 提取布局属性
Theme是针对窗体级别的，用于改变窗体样式。  
Style是针对窗体元素级别的，改变指定控件或者Layout样式。

共同点：抽象view的共同属性，可继承。

theme能写在Manifest文件中的application或activity中。  
style写于控件的style属性中。

具体在哪个标签写就在安卓资源文件那篇文章更新了。  

这里提一下快速抽取View的共同属性：
右键选择控件，点击Refactor，选择style，然后选择抽取的属性值以及style名称即可。

## 自定义控件模板
#### 流程
- 构造器->初始化  
- onMeasure->定大小  
- onLayout->定位置  
- onDraw->绘制  
- invalidate->刷新  

#### 三种主要形式
- 继承已有控件
- 继承布局文件
- 继承view

#### 例子
初始化推荐写法  
代码更简洁，不需要在每个地方进行初始化，便于修改。
```java
//如果view是在Java代码里new的，调用第一个构造函数
public RedNumButton(Context context) {
	this(context,null);
}

//如果view是在.xml里声明的，则调用第二个构造函数
//自定义属性是从AttributeSet参数传来的
public RedNumButton(Context context, @Nullable AttributeSet attrs) {
	this(context, attrs,0);
}

//不会自动调用
//一般在第二个构造函数中主动调用
//如果view有style属性
public RedNumButton(Context context, @Nullable AttributeSet attrs, int defStyleAttr) {
	super(context, attrs, defStyleAttr);
	init();
}

//API21之后才使用，不会自动调用
//一般在第二个构造函数中主动调用
//如果view有style属性
@RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
public RedNumButton(Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes) {
	super(context, attrs, defStyleAttr, defStyleRes);
}
```


增加自定义属性  
在values中新建attrs.xml文件
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="RedNumButton">
        <attr name="backgroundColor" format="color"/>
        <attr name="TimeLoader" format="integer"/>
    </declare-styleable>
</resources>
```

在布局文件引用自定义属性时得在跟布局加入引用，输入app，在自动提示选中appNs。
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/container"
    tools:context=".MainActivity"
    android:orientation="horizontal">
    <com.fb.daily.RedNumButton
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:layout_centerInParent="true"
        app:timeLoader="30"
        app:backgroundColor="#00BCD4"/>
</RelativeLayout>
```

tips:如果不知道颜色怎么选，点击颜色行左侧那个色块。

代码中要读取，需要使用TypedArray。
```java
TypedArray typedArray = context.obtainStyledAttributes(attrs,R.styleable.RedNumButton);
mBackgroundColor = typedArray.getColor(R.styleable.RedNumButton_backgroundColor,Color.RED);
num = typedArray.getInt(R.styleable.RedNumButton_timeLoader,20);
```

首先要通过上下文的obtainStyledAttributes方法获取TypeArray，需要传入参数AttributeSet和资源文件。  
获取参数就是用styleble_+属性名，第二个参数就是默认值。

计时按钮
```java
public class RedNumButton extends View {
    private Paint mCirclePaint;
    private Paint mTextPaint;
    private Rect mRect;
    private int num,time;
    private boolean clickFlag = false;
    private int mBackgroundColor;

    public RedNumButton(Context context) {
        this(context,null);
    }

    public RedNumButton(Context context, AttributeSet attrs) {
        this(context, attrs,0);
    }

    public RedNumButton(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        init(context,attrs);
    }

    public void init(Context context, AttributeSet attrs){

        TypedArray typedArray = context.obtainStyledAttributes(attrs,R.styleable.RedNumButton);
        mBackgroundColor = typedArray.getColor(R.styleable.RedNumButton_backgroundColor,Color.RED);
        num = typedArray.getInt(R.styleable.RedNumButton_timeLoader,20);
		typedArray.recycle();
        time = num;

        mCirclePaint = new Paint();
        mCirclePaint.setColor(mBackgroundColor);
        mTextPaint = new Paint();
        mTextPaint.setColor(Color.WHITE);
        mTextPaint.setTextSize(200);
        mRect = new Rect();

        this.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.i("Click","点击");
                if(!clickFlag){
                    Log.i("Click","计时事件消费");
                    clickFlag = true;
                    final Timer timer = new Timer();
                    TimerTask task = new TimerTask() {
                        @Override
                        public void run() {
                            time--;
                            if(time<0){
                                timer.cancel();
                                time = num;
                                clickFlag = false;
                            }
                            invalidate();
                        }
                    };
                    timer.schedule(task,0,1000);
                }
            }
        });
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        canvas.drawCircle(getWidth()/2,getHeight()/2,getWidth()/2,mCirclePaint);
        String text = String.valueOf(time);
        mTextPaint.getTextBounds(text,0,text.length(),mRect);
        canvas.drawText(text,getWidth()/2-mRect.width()/2,getHeight()/2+mRect.height()/2,mTextPaint);
    }
}

```


## AttributeSet与TypedArray
#### AttributeSet
AttributeSet是xml解析工具类，帮我们从布局xml中提取属性名与属性值，他是一个接口，实现类是XmlBlock的子类Parser。
打印属性。
首先将刚才布局的属性换成一个索引。  
```xml
<com.fb.daily.RedNumButton
	android:layout_width="200dp"
	android:layout_height="200dp"
	android:layout_centerInParent="true"
	app:timeLoader="30"
	app:backgroundColor="@color/colorAccent"/>
```

```java
public RedNumButton(Context context, AttributeSet attrs) {
	this(context, attrs,0);
	for (int i = 0; i < attrs.getAttributeCount(); i++) {
		Log.d("TAG-----", "name:" + attrs.getAttributeName(i) + "  value:" + attrs.getAttributeValue(i));
	}
}
```

结果
```
name:layout_width  value:200.0dip
name:layout_height  value:200.0dip
name:layout_centerInParent  value:true
name:timeLoader  value:30
name:backgroundColor  value:@2130968617
```

我们会发现两个问题：  
其中一个backgroundColor属性变成了地址值。  
还有我们非自定义的属性也在结果中。

#### TypedArray
TypedArray的存在解决了这个问题。
```java
TypedArray typedArray = context.obtainStyledAttributes(attrs,R.styleable.RedNumButton);
	//count 表示解析出来的个数
	int count = typedArray.getIndexCount();
	for (int i = 0; i < count; i++) {
		int indexValue = typedArray.getIndex(i);
		Log.d("TAG", "id:" + i);
		//通过属性index找到属性值
		switch (indexValue) {
			case R.styleable.RedNumButton_backgroundColor:
				int color = typedArray.getColor(R.styleable.RedNumButton_backgroundColor,-1);
				String hex = Integer.toHexString(color);
				Log.d("TAG", "color value:" + hex);
				break;
			case R.styleable.RedNumButton_timeLoader:
				int time =  typedArray.getInt(R.styleable.RedNumButton_timeLoader,-1);
				Log.d("TAG","time value:"+time);
			}
	}
typedArray.recycle();
```

运行结果
```
id:0
color value:ff03dac5
id:1
time value:30
```

R.styleable.RedNumButton本质上是一个数组，其索引在编译期间生成在R.java中。  
通过context.obtainStyledAttributes方法源码可以看出，其在最后调用了TypeArray的obtain方法。

在R.java里
RedNumButton_backgroundColor 代表数组索引下标
RedNumButton 代表属性数组
backgroundColor 代表属性
总结来说：通过下标取数组里属性。