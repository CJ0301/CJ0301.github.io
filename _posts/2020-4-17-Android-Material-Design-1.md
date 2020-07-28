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
```xml
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
1.创建Adapter：继承RecyclerView.Adapter\<VH\>。  
2.创建ViewHolder内部类：在Adapter中创建一个继承。RecyclerView.ViewHolder的静态内部类，记为VH。ViewHolder的实现和ListView的ViewHolder实现几乎一样。    
3.实现三个方法：

onCreateViewHolder()  
这个方法主要生成为每个Item inflater出一个View，但是该方法返回的是一个ViewHolder。该方法把View直接封装在ViewHolder中，然后我们面向的是ViewHolder这个实例，当然这个ViewHolder需要我们自己去编写。  

onBindViewHolder()  
这个方法主要用于适配渲染数据到View中。方法提供给你了该条目的viewHolder而不是原来的convertView。
 
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
		//获取创建好的holder，对其进行数据赋值
		holder.tv.setText(list.get(position));
	}

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup viewGroup, int arg1) {
        Log.i("onCreateViewHolder","调用");
        View view = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.recycler_item,viewGroup,false);
        //创建ViewHolder，初始化其视图
        MyViewHolder holder = new MyViewHolder(view);
        return holder;
    }
}
```

注意：  
视图创建一定要用LayoutInflater
```java
View view = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.recycler_item,viewGroup,false);
```
去生成，用
```java
View view=View.inflate(context,layoutId,null);
```
创建的view未添加viewGroup，无法获得LayoutParams，会导致宽高不正常。

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

给view加上点击事件
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
```java
adapter.setOnnItemClickListener(new
	RecyclerItemClickListener() {
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
两个getItemOffsets方法最终都是调用了上面实现,就一行代码,如果我们自定义过 ItemDecoration 的话,就会知道,我们可以为 outRect 设置四边的大小来为 itemView 设置一个偏移量,对绘制区域进行偏移。

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

线性布局分割线
```java
public class DividerDecoration extends RecyclerView.ItemDecoration {
    private int mOrientation = LinearLayoutManager.VERTICAL;
    private Drawable mDivider;
    private int[] attrs = new int[]{
      android.R.attr.listDivider
    };
    public DividerDecoration(Context context, int orientation) {
        TypedArray typedArray = context.obtainStyledAttributes(attrs);
        mDivider = typedArray.getDrawable(0);
        typedArray.recycle();
        setOrientation(orientation);
    }

    public void setOrientation(int orientation){
        if(orientation != LinearLayoutManager.HORIZONTAL && orientation != LinearLayoutManager.VERTICAL){
            throw new IllegalArgumentException("参数设置异常");
        }
        this.mOrientation = orientation;
    }

    @Override
    public void getItemOffsets(@NonNull Rect outRect, @NonNull View view, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) {
        super.getItemOffsets(outRect, view, parent, state);
        //调用此方法，先获取条目之间的宽度，即Rect矩形区域
        //获取条目的偏移量，所有条目都会调用一次该方法
        if(mOrientation == LinearLayoutManager.VERTICAL){
            //right先设置为0，之后再拉伸，这里也可以设置
            outRect.set(0,0,0,mDivider.getIntrinsicHeight());
        }else{
            outRect.set(0,0,mDivider.getIntrinsicWidth(),0);
        }
    }

    @Override
    public void onDraw(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) {
        super.onDraw(c, parent, state);
        //调用绘制方法
        if(mOrientation == LinearLayoutManager.VERTICAL){
            drawVertical(c,parent);
        }else{
            drawHorizontal(c,parent);
        }
    }

    private void drawHorizontal(Canvas c, RecyclerView parent) {
        //画垂直线
        int top = parent.getPaddingTop();
        int bottom = parent.getHeight()-parent.getPaddingBottom();
        int childCount = parent.getChildCount();
        for(int i=0;i<childCount;i++){
            View child = parent.getChildAt(i);
            RecyclerView.LayoutParams params = (RecyclerView.LayoutParams)child.getLayoutParams();
            //底部值+外边距+动画偏移
            int left = child.getRight() + params.rightMargin + Math.round(ViewCompat.getTranslationX(child));
            int right = left + mDivider.getIntrinsicHeight();
            mDivider.setBounds(left,top,right,bottom);
            mDivider.draw(c);
        }
    }

    private void drawVertical(Canvas c, RecyclerView parent) {
        //画水平线
        int left = parent.getPaddingLeft();
        int right = parent.getWidth()-parent.getPaddingRight();
        int childCount = parent.getChildCount();
        for(int i=0;i<childCount;i++){
            View child = parent.getChildAt(i);
            RecyclerView.LayoutParams params = (RecyclerView.LayoutParams)child.getLayoutParams();
            //底部值+外边距+动画偏移
            int top = child.getBottom() + params.bottomMargin + Math.round(ViewCompat.getTranslationY(child));
            int bottom = top + mDivider.getIntrinsicHeight();
            mDivider.setBounds(left,top,right,bottom);
            mDivider.draw(c);
        }
    }

}

```

网格布局分割线
```java
public class GridDividerDecoration extends RecyclerView.ItemDecoration {
    private Drawable mDivider;

    public GridDividerDecoration(Context context) {
        Resources resources = context.getResources();
        Drawable drawable = resources.getDrawable(R.drawable.item_deco);
        mDivider = drawable;
    }

    @Override
    public void onDraw(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) {
        super.onDraw(c, parent, state);
        drawVertical(c,parent);
        drawHorizontal(c,parent);
    }

    private void drawHorizontal(Canvas c, RecyclerView parent) {
        //水平间隔线
        int childCount = parent.getChildCount();
        for(int i=0;i<childCount;i++){
            View child = parent.getChildAt(i);
            RecyclerView.LayoutParams params = (RecyclerView.LayoutParams)child.getLayoutParams();
            int left = child.getLeft() - params.leftMargin;
            int right = child.getRight() + params.rightMargin;
            int top = child.getBottom() + params.bottomMargin;
            int bottom = top + mDivider.getIntrinsicHeight();

            mDivider.setBounds(left,top,right,bottom);
            mDivider.draw(c);
        }
    }

    private void drawVertical(Canvas c, RecyclerView parent) {
        //垂直间隔线
        int childCount = parent.getChildCount();
        for(int i=0;i<childCount;i++){
            View child = parent.getChildAt(i);
            RecyclerView.LayoutParams params = (RecyclerView.LayoutParams)child.getLayoutParams();
            int left = child.getRight();
            int right = left + mDivider.getIntrinsicWidth();
            int top = child.getTop() - params.topMargin;
            int bottom = child.getBottom() + params.bottomMargin;

            mDivider.setBounds(left,top,right,bottom+10);
            mDivider.draw(c);
        }
    }

    @Override
    public void getItemOffsets(@NonNull Rect outRect, @NonNull View view, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) {
        super.getItemOffsets(outRect, view, parent, state);
        Log.i("count",parent.getChildPosition(view)+"  ");
        int position = parent.getChildPosition(view);
        //四个方向的偏移值
        int right = mDivider.getIntrinsicWidth();
        int bottom = mDivider.getIntrinsicHeight();

		//最后的行列不再绘制
        if(isLastColumn(position,parent))
            right = 0;

        if(isLastRow(position,parent))
            bottom = 0;

        outRect.set(0,0,right,bottom);

    }

    private boolean isLastRow(int position,RecyclerView parent) {
        RecyclerView.LayoutManager lm = parent.getLayoutManager();
        if(lm instanceof GridLayoutManager){
            GridLayoutManager gm = (GridLayoutManager)lm;
            int childCount = gm.getItemCount();
            int spanCount = gm.getSpanCount();
            int lastRowCount = childCount%spanCount;

            if(lastRowCount==0||lastRowCount<spanCount)
                return true;

        }

        return false;
    }

    private boolean isLastColumn(int position,RecyclerView parent) {
        RecyclerView.LayoutManager lm = parent.getLayoutManager();
        if(lm instanceof GridLayoutManager){
            GridLayoutManager gm = (GridLayoutManager)lm;
            int spanCount = gm.getSpanCount();
            if((position+1)%spanCount == 0){
                return true;
            }
        }

        return false;
    }

}


```

![](20200715-grid-item-decorate.jpg)
过程就是先通过getItemOffsets方法进行偏移，然后在调用onDraw方法进行绘制。  
上面的线性布局分割线其实就是按谷歌提供的DividerItemDecoration写的，也可以进源码看看。

注意：
- 可以通过修改通过Them.Appcompat主题样式里的android:listSelector或者android:listDivider属性达到改变间隔线大小和颜色，例：

```xml
<style name="AppTheme" parent="AppBaseTheme">
	<item name="android:listDivider">@drawble/item_divider</item>
</style>
```
- 绘制RecyclerView的时候，会分发Canvas到ItemDecoration里

四、多条目种类  
实现多条目得重写getItemViewType()方法，再通过onCreateViewHolder()方法判断生成视图。

```java
public class QuestionAdapter extends RecyclerView.Adapter<QuestionAdapter.MyViewHolder> {
	private final int SINGLE = 0;
	private final int MULTI = 1;
	private final int EDIT = 2;
	private List<Question> lists;
	private String[] answers;
	public QuestionAdapter(List<Question> lists) {
		this.lists = lists;
		answers = new String[lists.size()];
	}

	public int getItemCount() {
		return lists.size();
	}

	@Override
	public QuestionAdapter.MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
		QuestionAdapter.MyViewHolder viewHolder = null;
		if(viewType == SINGLE){
			View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.itemlayout_single,parent,false);
			return new SingleViewHolder(view);
			
		}else if(viewType == MULTI){
			View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.itemlayout_multi,parent,false);
			return new MultiViewHolder(view);
		}else if(viewType == EDIT){
			View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.itemlayout_edit,parent,false);
			return new EditViewHolder(view);
		}
		return viewHolder;
	}

	@Override
	public void onBindViewHolder(QuestionAdapter.MyViewHolder holder, int position) {
		holder.setIsRecyclable(false);//禁止复用 不加这个会出错 以后好好研究研究
		holder.setDate(position);
	}

	@Override
	public int getItemViewType(int position) {
		return lists.get(position).getType();
	}

	abstract class MyViewHolder extends RecyclerView.ViewHolder{
		TextView id;
		TextView question;
		public MyViewHolder(View itemView) {
			super(itemView);
			id=itemView.findViewById(R.id.question_id);
			question = itemView.findViewById(R.id.question);
		}

		public void setDate(int pos){
			id.setText("Q"+(pos+1)+".");
			question.setText(lists.get(pos).getQues());
			setAnswer(pos);
		}

		abstract void setAnswer(int pos);
	}

	String answer;
	class SingleViewHolder extends MyViewHolder{
		RadioGroup radioGroup;
		public SingleViewHolder(View itemView) {
			super(itemView);
			radioGroup = itemView.findViewById(R.id.radioGroup);
		}

		@Override
		void setAnswer(final int pos) {
			List<String> singles = lists.get(pos).getAnswers();
			for(String s:singles){
				final RadioButton radioButton = new RadioButton(radioGroup.getContext());
				radioButton.setLayoutParams(new LinearLayout.LayoutParams(LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT));
				radioButton.setText(s);
				answer = radioButton.getText().toString().substring(0,1);
				if(answer.equals(answers[pos])){
					radioButton.setChecked(true);
				}
				radioButton.setOnClickListener(new View.OnClickListener() {
					@Override
					public void onClick(View v) {
						answer = radioButton.getText().toString().substring(0,1);
						answers[pos] = answer;
					}
				});
				radioGroup.addView(radioButton);
			}
		}

	}

	class MultiViewHolder extends MyViewHolder{
		LinearLayout linearLayout;
		public MultiViewHolder(View itemView) {
			super(itemView);
			linearLayout = itemView.findViewById(R.id.linearLayout);

		}

		@Override
		void setAnswer(final int pos) {
			List<String> multies = lists.get(pos).getAnswers();
			for(String s:multies){
				final CheckBox checkBox = new CheckBox(linearLayout.getContext());
				checkBox.setLayoutParams(new LinearLayout.LayoutParams(LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT));
				checkBox.setText(s);
				answer = checkBox.getText().toString().substring(0,1);
				if(answers[pos]!=null){
					if(answers[pos].contains(answer)){
						checkBox.setChecked(true);
					}
				}
				checkBox.setOnClickListener(new View.OnClickListener() {
					@Override
					public void onClick(View v) {
						String answer = checkBox.getText().toString().substring(0,1);
						if(answers[pos]!=null){
							if(!answers[pos].contains(answer)){
								answers[pos] += answer;
							}else{
								answer.replace(answer,"");
							}
						}else if(answers[pos]==null){
							answers[pos]=answer;
						}
					}
				});
				linearLayout.addView(checkBox);
			}
		}
	}

	class EditViewHolder extends MyViewHolder{
		private EditText editText;
		public EditViewHolder(View itemView) {
			super(itemView);
			editText = itemView.findViewById(R.id.editAnswer);
		}

		@Override
		void setAnswer(final int pos) {
			if(answers[pos]!=null){
				editText.setText(answers[pos]);
			}
			editText.addTextChangedListener(new TextWatcher() {
				@Override
				public void beforeTextChanged(CharSequence s, int start, int count, int after) {

				}

				@Override
				public void onTextChanged(CharSequence s, int start, int before, int count) {

				}

				@Override
				public void afterTextChanged(Editable s) {
					answers[pos] = editText.getText().toString();
				}
			});
		}
	}

	public int commitCheck(){
		for(int i=0;i<answers.length;i++){
			if(answers[i]==null){
				return i;
			}
		}
		return -1;
	}

	public String[] getAnswers() {
		return answers;
	}

	/**
	 * 目标项是否在最后一个可见项之后
	 */
	private boolean mShouldScroll;
	/**
	 * 记录目标项位置
	 */
	private int mToPosition;

	/**
	 * 滑动到指定位置
	 *
	 * @param mRecyclerView
	 * @param position
	 */
	public void smoothMoveToPosition(RecyclerView mRecyclerView, final int position) {
		// 第一个可见位置
		int firstItem = mRecyclerView.getChildLayoutPosition(mRecyclerView.getChildAt(0));
		// 最后一个可见位置
		int lastItem = mRecyclerView.getChildLayoutPosition(mRecyclerView.getChildAt(mRecyclerView.getChildCount() - 1));

		if (position < firstItem) {
			// 如果跳转位置在第一个可见位置之前，就smoothScrollToPosition可以直接跳转
			mRecyclerView.smoothScrollToPosition(position);
		} else if (position <= lastItem) {
			// 跳转位置在第一个可见项之后，最后一个可见项之前
			// smoothScrollToPosition根本不会动，此时调用smoothScrollBy来滑动到指定位置
			int movePosition = position - firstItem;
			if (movePosition >= 0 && movePosition < mRecyclerView.getChildCount()) {
				int top = mRecyclerView.getChildAt(movePosition).getTop();
				mRecyclerView.smoothScrollBy(0, top);
			}
		} else {
			// 如果要跳转的位置在最后可见项之后，则先调用smoothScrollToPosition将要跳转的位置滚动到可见位置
			// 再通过onScrollStateChanged控制再次调用smoothMoveToPosition，执行上一个判断中的方法
			mRecyclerView.smoothScrollToPosition(position);
			mToPosition = position;
			mShouldScroll = true;
		}
	}

}

```

五、交互动画
RecyclerView有一个专门能实现交互的类ItemTouchHelper，它的Callback类能在一些操作下被RecyclerView回调。  

首先我们写一个ItemTouchCallback继承自ItemTouchHelper.Callback，必须重写的有三个方法：
```java
//Callback回调时先调用，用来判断是什么动作，比如方向
public int getMovementFlags(RecyclerView recyclerView,RecyclerView.ViewHolder viewHolder) 

//移动时回调的方法
public boolean onMove(RecyclerView recyclerView, RecyclerView.ViewHolder viewHolder,RecyclerView.ViewHolder target)

//侧滑时回调的方法
public void onSwiped(RecyclerView.ViewHolder viewHolder, int direction)
```

首先是第一个方法，第一个方法有四个方向可以选择，在ItemTouchHelper里以常量形式存在，上下左右分别对应1，2，4，8，底层上是进行了二进制的移位，方便用或运算组成十六种不同的组合(之前二进制的文章里也有写这个用法)，根据这个组合拖拽与侧滑的方向标记，然后进行合成作为函数返回值。
```java
//方向：上下左右
//常量:ItemTouchHelper.UP,ItemTouchHelper.DOWN
// ItemTouchHelper.LEFT,ItemTouchHelper.RIGHT

//实现原理，UP的值是二进制的0001，DOWN的值为二进制的0010，进行或运算得到0011表示能监听上下两个方位。
//拖拽的监听方向
int dragFlags = ItemTouchHelper.UP|ItemTouchHelper.DOWN;

//侧滑的监听方向
int swipeFlags = ItemTouchHelper.LEFT|ItemTouchHelper.RIGHT;

//合成监听标记
int flags = makeMovementFlags(dragFlags,swipeFlags);
return flags;
```

第二个方法是实现拖拽使用的  
ItemTouchCallback的长按拖拽默认是存在的，更改需要在isLongPressDragEnabled中重写返回值。

下面来实现一个直接拖拽  
首先准备一个接口  
```java
public interface StartDragListener {
    //回调拖拽效果
    void onStartDrag(RecyclerView.ViewHolder viewHolder);
}
```

activity中继承接口，重写接口方法等待adapter传入数据。
```java
//暴露给适配器的方法
public void onStartDrag(RecyclerView.ViewHolder viewHolder){
	helper.startDrag(viewHolder);
}
```

把activity对象传给adapter，获取对应控件的点击时间后调用接口方法，并把当前holder传递。
```java
@Override
public void onBindViewHolder(final MyViewHolder holder, int position) {
	//获取创建好的holder，对其进行数据赋值
	holder.tv.setText(list.get(position));
	holder.photo.setOnTouchListener(new View.OnTouchListener() {
		@Override
		public boolean onTouch(View v, MotionEvent event){
			if(event.getAction() == MotionEvent.ACTION_DOWN){
				//传递触摸情况给指定控件
            	listener.onStartDrag(holder);
			}
		return false;
		}
	});
}
```

这样实现的拖拽还不能数据交互，这时候就需要ItemTouchCallback去调用adapter中的数据交互方法了。  
同样准备接口，adapter继承
```java
public interface ItemTouchMoveListener {
    //拖拽的时候回调，在此方法中实现拖拽条目并刷新
    boolean onItemMove(int fromPosition,int toPosition);
}
```

实现数据交换逻辑
```java
@Override
public boolean onItemMove(int fromPosition, int toPosition) {
	//数据交换
	Collections.swap(list,fromPosition,toPosition);
	//刷新
	notifyItemMoved(fromPosition,toPosition);
	return true;
}
```

重写移动回调
```java
//移动时回调的方法
@Override
public boolean onMove(@NonNull RecyclerView recyclerView, @NonNull RecyclerView.ViewHolder viewHolder, @NonNull RecyclerView.ViewHolder target) {
	//布局种类不同则不交换
	if(viewHolder.getItemViewType()!=target.getItemViewType())
            return false;
        
	boolean flag = listener.onItemMove(viewHolder.getAdapterPosition(),target.getAdapterPosition());
	return flag;
}
```

第三个方法是侧滑  
在适配器那个接口加个方法给删除用
```java
public interface ItemTouchMoveListener {
    //拖拽的时候回调，在此方法中实现拖拽条目并刷新
    boolean onItemMove(int fromPosition,int toPosition);

    //条目移除时回调
    boolean onItemRemove(int position);
}
```

重写方法
```
@Override
public boolean onItemRemove(int position) {
	list.remove(position);
	notifyItemRemoved(position);
	return true;
}
```

重写侧滑方法
```java
//侧滑时回调
@Override
public void onSwiped(@NonNull RecyclerView.ViewHolder viewHolder, int direction) {
	//方向判断
//        if(direction == 4){
//            listener.onItemRemove(viewHolder.getAdapterPosition());
//        }
	listener.onItemRemove(viewHolder.getAdapterPosition());
}
```

ItemTouchCallback还有很多方法和代表状态的变量
选中时改变背景色
```java
@Override
public void onSelectedChanged(@Nullable RecyclerView.ViewHolder viewHolder, int actionState) {
	super.onSelectedChanged(viewHolder, actionState);
	//判断选中状态
	if(actionState!=ItemTouchHelper.ACTION_STATE_IDLE){
		viewHolder.itemView.setBackgroundColor(viewHolder.itemView.getContext().getResources().getColor(R.color.colorPrimary));
	}
}
```

侧滑时实现动画 
```java
//重绘Child
@Override
public void onChildDraw(@NonNull Canvas c, @NonNull RecyclerView recyclerView, @NonNull RecyclerView.ViewHolder viewHolder, float dX, float dY, int actionState, boolean isCurrentlyActive) {
	super.onChildDraw(c, recyclerView, viewHolder, dX, dY, actionState, isCurrentlyActive);
	//dx范围0~view.getWidth
	if(actionState == ItemTouchHelper.ACTION_STATE_SWIPE){
		float flag = 1-Math.abs(dX)/viewHolder.itemView.getWidth();
		//透明度动画
		viewHolder.itemView.setAlpha(flag);
		//缩放动画
		viewHolder.itemView.setScaleX(flag);
		viewHolder.itemView.setScaleY(flag);
	}

	//方向反转
	viewHolder.itemView.setTranslationX(-0.5f*viewHolder.itemView.getTranslationX());

}
```

这里注意，ListView和RecyclerView中都有复用的条目itemView，上面两个方法改变的参数都需要用clearView方法恢复条目状态，否则会出现视图问题。
```java
@Override
public void clearView(@NonNull RecyclerView recyclerView, @NonNull RecyclerView.ViewHolder viewHolder) {
	super.clearView(recyclerView, viewHolder);
	viewHolder.itemView.setBackgroundColor(Color.WHITE);

	//会遇到一个bug，存在侧滑删除后视图倒转之类的问题，在下面的动画绘制完之后需要恢复视图属性
	viewHolder.itemView.setAlpha(1);
	viewHolder.itemView.setScaleX(1);
	viewHolder.itemView.setScaleY(1);
}
```

