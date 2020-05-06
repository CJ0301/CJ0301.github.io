---
layout: 		post
title: 			"Android的设计规范"
subtitle: 		'Material Design'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---

这一篇和之前的[用户基础交互](https://www.cjcjcj.top/2020/03/31/User-Interaction/)有一点关系。

## Material Design
#### 概念
Material Design是从Android5.0开始引入的，由谷歌提倡的一种设计风格、理念、原则。

👉[通往中文文档的传送门](https://www.mdui.org/design/)

#### 使用
在历史上，Android收集并开发了不少开源项目放在自己的support包中提供给开发者使用。🌰：  
1）android-support-v4:最低兼容到Android 1.6系统，里面有类似ViewPager等控件。  
2）android-support-v7:appcompat、CardView、gridlayout、mediarouter、
palette、preference、recyclerView(最低兼容到3.0) 

这些support包简化了开发者的工作，同时保证了软件在每个系统版本下的视觉效果达到统一，现在的Android Studio会自动引入appcompat。

现在support包已经由AndroidX整理取代。

## SwipeRefreshLayout
依赖
```
implementation 'androidx.swiperefreshlayout:swiperefreshlayout:1.0.0'
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity {

    SwipeRefreshLayout srl;
    TextView show;
    int time=0;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        show = findViewById(R.id.show);
        srl = findViewById(R.id.swipe);
        srl.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
            @Override
            public void onRefresh() {
                //下拉完毕 加载更多数据
                time++;
                show.setText("刷新:"+time);

                //获取数据之后取消刷新
                srl.setRefreshing(false);
            }
        });
        //中间的圆圈
        srl.setColorSchemeColors(Color.RED,Color.BLUE,Color.GREEN);
        //设置进度条的背景颜色
        srl.setProgressBackgroundColorSchemeColor(Color.YELLOW);
        //设置下拉多少距离开始刷新
        srl.setDistanceToTriggerSync(70);

    }
}

```

activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.swiperefreshlayout.widget.SwipeRefreshLayout xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/swipe"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">


        <TextView
            android:id="@+id/show"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="刷新显示"
            android:textSize="40sp"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />
    </androidx.constraintlayout.widget.ConstraintLayout>

</androidx.swiperefreshlayout.widget.SwipeRefreshLayout>
```

#### 常用方法
```java
//设置进度View样式的大小，只有两个值DEFAULT和LARGE，表示默认和较大
swipeRefreshLayout.setSize(DEFAULT);
//设置触发下拉刷新的距离
swipeRefreshLayout.setDistanceToTriggerSync(300);
//设置动画样式下拉的起始点和结束点，scale 是指设置是否需要放大或者缩小动画。
swipeRefreshLayout.setProgressViewOffset(boolean scale, int start, int end)
//设置动画样式下拉的结束点，scale 是指设置是否需要放大或者缩小动画
swipeRefreshLayout.setProgressViewEndTarget(boolean scale, int end);
//如果自定义了swipeRefreshLayout，可以通过这个回调方法决定是否可以滑动。
setOnChildScrollUpCallback(@Nullable OnChildScrollUpCallback callback)
```

## Scrollview
#### xml中常见属性
1.上下渐变  

```xml
android:fadingEdgeLength="50dp"//渐变范围
android:requiresFadingEdge="vertical"//渐变方向
```

2.去掉拉到尽头的阴影效果，适用于2.3及以上的 否则不用设置。

```xml
android:overScrollMode="never"
```

3.设置滚动条显示，none（隐藏），horizontal（水平），vertical（垂直）。

```xml
android:scrollbars="none"
```

4.这是 ScrollView 独有的属性，用来定义 ScrollView 对象是否需要拉伸自身内容来填充
viewport。通俗来说，就是允许ScrollView去填充整个屏幕。比如ScrollView嵌套的子控件高度达不到屏幕高度时，虽然ScrollView高度设置了match_parent，也无法充满整个屏幕，需设置android:fillViewport=“true"使ScrollView填充整个页面，给ScrollView设置背景颜色就能体现。

```xml
android:fillViewport=“true"
```


#### 解决与swipeRefreshLayout的滑动冲突
低版本(sdk23以下)：
```java
package com.fb.smartsite;

import android.content.Context;
import android.util.AttributeSet;
import android.widget.ScrollView;

import androidx.swiperefreshlayout.widget.SwipeRefreshLayout;

public class mScrollView extends ScrollView {

    SwipeRefreshLayout swipeRefreshLayout;

    public mScrollView(Context context) {
        super(context);
    }

    public mScrollView(Context context, AttributeSet attrs, int defStyle) {
        super(context, attrs, defStyle);
    }

    public mScrollView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }


    public void setSwipeRefreshLayout(SwipeRefreshLayout swipeRefreshLayout) {
        this.swipeRefreshLayout = swipeRefreshLayout;
    }

    @Override
    protected void onScrollChanged(int l, int t, int oldl, int oldt) {
        super.onScrollChanged(l, t, oldl, oldt);
        if(this.getScrollY()==0){
            swipeRefreshLayout.setEnabled(true);
        }else {
            swipeRefreshLayout.setEnabled(false);
        }
    }
}


```
高版本(sdk23以上)：
```java
scrollView.setOnScrollChangeListener(new View.OnScrollChangeListener() {
            @Override
            public void onScrollChange(View view, int i, int i1, int i2, int i3) {
                srl.setEnabled(scrollView.getScrollY()==0);
            }
        });
```

#### 常用方法

滑动开关控制

```java
scrollView.setOnTouchListener(new View.OnTouchListener() {
	@Override
 	public boolean onTouch(View view, MotionEvent motionEvent) {
        // true禁止滑动  false可滑动
 		return true;
  	}
});
```

滑动位置控制

```java
scrollView.post(new Runnable() {
	@Override
	public void run() {
		//滑动到顶部
		scrollView.fullScroll(ScrollView.FOCUS_UP);
        
        //滑动到底部
        scrollView.fullScroll(ScrollView.FOCUS_DOWN);
	}
});
```

滑动到某个位置

```java
scrollView.post(new Runnable() {
	@Override
	public void run() {
		//偏移值
		int offset = 100;
		scrollView.smoothScrollTo(0, offset);
	}
});
```

## RecyclerView
RecyclerView是谷歌在高版本提出的一个替代ListView、GridView的控件。

相较于ListView的优点：  
1.封装了ViewHolder的回收复用，标准化了ViewHolder，将复用的逻辑封装了。  
2.高度解耦。  
3.有线性、网格、瀑布流三种布局方式。  
4.可以设置Item的间隔样式。继承ItemDecoration类。  
5.控制Item增删动画。  

#### 依赖  
```xml
implementation 'androidx.recyclerview:recyclerview:1.1.0'
```

#### 适配器
1.创建Adapter：继承RecyclerView.Adapter<VH>。  
2.创建ViewHolder内部类：在Adapter中创建一个继承RecyclerView.ViewHolder的静态内部类，记为VH。ViewHolder的实现和ListView的ViewHolder实现几乎一样。
3.实现三个方法：

onCreateViewHolder()
这个方法主要生成为每个Item inflater出一个View，但是该方法返回的是一个ViewHolder。该方法把View直接封装在ViewHolder中，然后我们面向的是ViewHolder这个实例，当然这个ViewHolder需要我们自己去编写。

onBindViewHolder()
这个方法主要用于适配渲染数据到View中。方法提供给你了一viewHolder而不是原来的convertView。

getItemCount()
这个方法就类似于BaseAdapter的getCount方法了，即总共有多少个条目。

基本实现：  
```java
public class MyRecyclerAdapter extends RecyclerView.Adapter<MyRecyclerAdapter.MyViewHolder> {

	private List<String> list;

	public MyRecyclerAdapter(List<String> list) {
		// TODO Auto-generated constructor stub
		this.list = list;
	}
	
	class MyViewHolder extends RecyclerView.ViewHolder{
		TextView tv;

		public MyViewHolder(View view) {
			super(view);
			tv = (TextView)view.findViewById(android.R.id.text1);
			
		}
		
	}

	@Override
	public int getItemCount() {
		// TODO Auto-generated method stub
		return list.size();
	}

	@Override
	public void onBindViewHolder(MyViewHolder holder, int position) {
		//设置数据
		holder.tv.setText(list.get(position));
	}

	@Override
	public MyViewHolder onCreateViewHolder(ViewGroup viewGroup, int arg1) {
		//创建ViewHolder
		MyViewHolder holder = new MyViewHolder(View.inflate(viewGroup.getContext(), android.R.layout.simple_list_item_1, null));
		return holder;
	}
}
```

#### 设置RecyclerView
一般来说，需要为RecyclerView进行四大设置：  
1.Layout Manager(必选):Item的布局。  
2.Adapter(必选)：为Item提供数据。  
3.Item Decoration(可选，默认为空)：Item之间的Divider。
4.Item Animator(可选，默认为DefaultItemAnimator)：添加、删除Item动画。  

如果要实现ListView的效果，只需要设置Adapter和Layout Manager，如下🌰：  
```java
List<String> data = initData();
RecyclerView rv = (RecyclerView) findViewById(R.id.rv);
rv.setLayoutManager(new LinearLayoutManager(this));
rv.setAdapter(new MyRecyclerAdapter(data));
```

一、LayoutManager  
RecyclerView提供了三种布局管理器：
LinerLayoutManager 以垂直或者水平列表方式展示Item。  
GridLayoutManager 以网格方式展示Item。  
StaggeredGridLayoutManager 以瀑布流方式展示Item。  
如果你想用 RecyclerView 来实现自己自定义效果，则应该去继承实现自己的 LayoutManager，并重写相应的方法，而不应该想着去改写 RecyclerView。

LayoutManager 常见 API  
```java
canScrollHorizontally();//能否横向滚动
canScrollVertically();//能否纵向滚动
scrollToPosition(int position);//滚动到指定位置

setOrientation(int orientation);//设置滚动的方向
getOrientation();//获取滚动方向

findViewByPosition(int position);//获取指定位置的Item View
findFirstCompletelyVisibleItemPosition();//获取第一个完全可见的Item位置
findFirstVisibleItemPosition();//获取第一个可见Item的位置
findLastCompletelyVisibleItemPosition();//获取最后一个完全可见的Item位置
findLastVisibleItemPosition();//获取最后一个可见Item的位置
```

二、添加点击事件  
RecyclerView中的点击事件需要自己写。  

接口  
```java
public interface RecyclerItemClickListener {
    void click(TextView textView);//括号放入需要操作的对象
}
```

在ViewHolder的构造方法中给view加上点击事件
```java
view.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View view) {
		if(listener!=null)
			listener.click(tv);//传入参数
					
	}
});
```

适配器中加入set方法
```java
public void setOnnItemClickListener(RecyclerItemClickListener listener){
	this.listener = listener;
}
```
使用
```
adapter.setOnnItemClickListener(new 	RecyclerItemClickListener() {
	@Override
	public void click(TextView textView) {
		Toast.makeText(MainActivity.this,textView.getText(),Toast.LENGTH_SHORT).show();
	}
});
```

三、Item Decoration间隔样式
RecyclerView通过addItemDecoration()方法添加item之间的分割线。Android并没有提供实现好的Divider，因此任何分割线样式都需要自己实现。

自定义间隔样式需要继承RecyclerView.ItemDecoration类，该类是个抽象类，官方目前并没有提供默认的实现类，主要有三个方法。

onDraw(Canvas c, RecyclerView parent, State state)，在Item绘制之前被调用，该方法主要用于绘制间隔样式。

onDrawOver(Canvas c, RecyclerView parent, State state)，在Item绘制之前被调用，该方法主要用于绘制间隔样式。

getItemOffsets(Rect outRect, View view, RecyclerView parent, State state)，设置item的偏移量，偏移的部分用于填充间隔样式，即设置分割线的宽、高；在RecyclerView的onMesure()中会调用该方法。

`onDraw()`和`onDrawOver()`这两个方法都是用于绘制间隔样式，我们只需要复写其中一个方法即可。

Google给了一个参考实现类DividerItemDecoration,可以简化我们的开发流程:  
```java
//设置recyclerView每个item间的分割线
DividerItemDecoration itemDecoration = new DividerItemDecoration(
	this, DividerItemDecoration.VERTICAL);
Drawable drawable = ContextCompat.getDrawable(this,R.drawable.grid_divider);
itemDecoration.setDrawable(drawable);
recyclerView.addItemDecoration(itemDecoration);
```

自定义间隔样式

1.getItemOffsets  
除了 getItemOffsets 方法，其他方法的默认实现都为空，而 getItemOffsets 的默认实现方法也很简单：
```java
@Deprecated
public void getItemOffsets(@NonNull Rect outRect, int itemPosition,
	@NonNull RecyclerView parent) {
	outRect.set(0, 0, 0, 0);
}
```
两个getItemOffsets方法最终都是调用了上面实现,就一行代码,如果我们自定义过 ItemDecoration 的话,就会知道,我们可以为 outRect 设置四边的大小来为 itemView 设置一个偏移量。偏移量在绘制时与parent-padding、layout_margin加在一起。

2.onDraw  
```java
public void onDraw(Canvas c, RecyclerView parent, State state) {
	onDraw(c, parent);
}

/**
* @deprecated Override {@link #onDraw(Canvas, RecyclerView, RecyclerView.State)}
*/
@Deprecated
public void onDraw(Canvas c, RecyclerView parent) {
}
```

onDraw方法有两个重载，一个被标注为 @deprecated,即弃用了，我们知道，如果重写了 onDraw，就可以在我们上面的 getItemOffsets中设置的范围内绘制。

