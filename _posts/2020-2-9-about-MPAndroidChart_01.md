---
layout: 		post
title: 			"MPAndroidChart_1"
subtitle: 		'关于MPAndroidChart的整理'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
> [MPAndroidChart](https://github.com/PhilJay/MPAndroidChart)是一款强大的图表制作开源框架。第一次使用他是因为大创的项目需要做图表，然后就接触到了这个框架。

## 准备工作
&emsp;首先下载Github上的[项目](https://github.com/PhilJay/MPAndroidChart)。接下来引用的方法有很多，可以导入他的库文件，或者有jar包就更方便啦。  
&emsp;下面来介绍如何引入和我遇到的一些小问题：
&emsp;依次点击左上角的```File->Import Module``` 然后找到```MPAndroidChart```文件下的```MPChartLib```,然后进入```Project Structure(按快捷键ctrl+alt+shift+s或者点右上角的一个文件夹的小图标)```,然后依次点击```Dependencies->app-> + ->Module Dependency```,最后选中```MPChartLib```  
&emsp;这里有遇到一个小问题，在MPChartLib的gradle文件中作者有加一行maven的依赖，可能会导致如下报错：
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200209_error_1.png)
只要删除如下一行代码即可
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200209_error_2.png)

## 使用
#### 初始化
&emsp;创建视图的方式有两种，第一种就是在XML文件里添加

```xml
<com.github.mikephil.charting.charts.LineChart
	android:id="@+id/chart"
	android:layout_width="match_parent"
	android:layout_height="match_parent" />
```

&emsp;然后在Activity、Fragment或是其他一些代码中进行处理

```java
// in this example, a LineChart is initialized from xml
LineChart chart = (LineChart) findViewById(R.id.chart);
```

&emsp;或是直接在代码中创建

```java
// programmatically create a LineChart
LineChart chart = new LineChart(Context);
// get a layout defined in xml
RelativeLayout rl = (RelativeLayout) findViewById(R.id.relativeLayout);
rl.add(chart); 
// add the programmatically created chart
```

#### 添加数据
&emsp;在你的图表初始化过后，你可以创建数据并添加到图表之中。这里用LineChart作为例子，LineChart的数据用Entry进行封装，Entry的属性包括x坐标与y坐标，而其他表格用其他的类进行封装(后文进行介绍)。
	
```java
YourData[] dataObjects = ...;
List<Entry> entries = new ArrayList<Entry>();
for (YourData data : dataObjects) {
	// turn your data into Entry objects
	entries.add(new Entry(data.getValueX(), data.getValueY())); 
}
```

&emsp;下一步，你需要将封装若干Entry的同类数据集放入一个LineDataSet中，并为这个数据集添加一个标签，进行单独的样式处理。

```java
LineDataSet dataSet = new LineDataSet(entries, "Label"); // add entries to dataset
dataSet.setColor(...);
dataSet.setValueTextColor(...); // styling, ...

```
&emsp;最后，你需要将所有的LineDataSet放入LineData中，有几条添加几条
	
```java
LineData lineData = new LineData();
lineData.addDataSet(dataSet);
chart.setData(lineData);
chart.invalidate(); // refresh
```

&emsp;整体代码：

```
public class MainActivity extends AppCompatActivity {
	LineChart lineChart;
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		lineChart = findViewById(R.id.lineChart);
		List<Entry> entries = new ArrayList<>();
		entries.add(new Entry(1,20f));
		entries.add(new Entry(2,14f));
		entries.add(new Entry(3,26f));
		entries.add(new Entry(4,10f));
		entries.add(new Entry(5,30f));

		LineDataSet lineDataSet = new LineDataSet(entries,"参数1");

		LineData lineData = new LineData();
		lineData.addDataSet(lineDataSet);
	
		lineChart.setData(lineData);
		lineChart.invalidate();
	}
}
```	

&emsp;显示效果：
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200209_simple_chart.png)


## 交互
#### 启用与禁用交互
- setTouchEnabled(boolean enabled)：允许启用/禁用与图表的所有可能的触摸交互。
- setDragEnabled(boolean enabled)：启用/禁用图表的拖动(平移)。
- setScaleEnabled(boolean enabled)：启用/禁用图表在两个轴上的缩放。
- setScaleXEnabled(boolean enabled)：启用/禁用x轴上的缩放。
- setScaleYEnabled(boolean enabled)：启用/禁用y轴上的缩放。
- setPinchZoom(boolean enabled)：如果设置为真，则启用按压缩放。如果禁用，x轴和y轴可以分开缩放.
- setDoubleTapToZoomEnabled(boolean enabled)：将此设置为false，不允许通过双击放大图表。

#### 图表翻转/减速
- setDragDecelerationEnabled(boolean enabled)：如果设置为真，则图表在修饰后继续滚动。默认值：真。
- setDragDecelerationFrictionCoef(float coef)：减速摩擦系数在[0；1]区间内，较高的值表示速度将缓慢下降，例如，如果它设置为0，它将立即停止。1是一个无效的值，并将自动转换为0.9999。

#### 高亮值
[内容太多 另外辟了个专题👇](#高亮)

#### 手势回调
&emsp;OnChartGestureListener能对图表操作的手势进行反应

```
public interface OnChartGestureListener {
	/**
		Callbacks when a touch-gesture has started on the chart (ACTION_DOWN)
     
		@param lastPerformedGesture
	*/
    	
	void onChartGestureStart(MotionEvent me, ChartGesture lastPerformedGesture);

	/**
		Callbacks when a touch-gesture has ended on the chart (ACTION_UP, ACTION_CANCEL)
    
		@param lastPerformedGesture
	*/

	void onChartGestureEnd(MotionEvent me, ChartGesture lastPerformedGesture);

	/**
		Callbacks when the chart is longpressed.
	*/

	public void onChartLongPressed(MotionEvent me);

	/**
		Callbacks when the chart is double-tapped.
	*/

	public void onChartDoubleTapped(MotionEvent me);

	/**
		Callbacks when the chart is single-tapped.
	*/

	public void onChartSingleTapped(MotionEvent me);

	/**
		Callbacks then a fling gesture is made on the chart.
      
		@param velocityX
		@param velocityY
	*/

	public void onChartFling(MotionEvent me1, MotionEvent me2, float velocityX, float velocityY);

	/**
		Callbacks when the chart is scaled / zoomed via pinch zoom gesture.
     
		@param scaleX scalefactor on the x-axis
		@param scaleY scalefactor on the y-axis
	*/

	public void onChartScale(MotionEvent me, float scaleX, float scaleY);

	/**
		Callbacks when the chart is moved / translated via   drag gesture.
     
		@param dX translation distance on the x-axis
		@param dY translation distance on the y-axis
	*/

	public void onChartTranslate(MotionEvent me, float dX, float dY);

}
```
    
## 高亮
#### 启用与禁用突出显示
- setHighlightPerDragEnabled(boolean enabled)：将此设置为真Chart允许在图表表面完全缩放时，每拖一次突出显示。默认值：true
- setHighlightPerTapEnabled(boolean enabled)：将此设置为falseChart若要防止通过点击手势突出显示值，请执行以下操作。值仍然可以通过拖动或编程方式突出显示。默认值：true
- setMaxHighlightDistance(float distanceDp)：在DP中设置最大高亮距离。在图表上按一下，离条目越远，距离越远，就不会触发高亮显示。默认值：500 dp

&emsp;高亮设置作用于DataSet对象
```java

dataSet.setHighlightEnabled(true); // allow highlighting for DataSet
// set this to false to disable the drawing of highlight indicator (lines)
dataSet.setDrawHighlightIndicators(true); 
dataSet.setHighlightColor(Color.BLACK); // color for highlight indicator
// and more...
```

#### 以编程的方式突出显示
- highlightValue(float x, int dataSetIndex, boolean callListener)：高亮显示给定数据集中给定x位置处的值。提供-1作为数据设置索引，以撤消所有突出显示。布尔标志决定选择侦听器是否应该被调用。
- highlightValue(Highlight high, boolean callListener)：突出显示所提供的值。Highlight对象。提供NULL以撤消所有突出显示。布尔标志决定选择侦听器是否应该被调用。
- highlightValues(Highlight[] highs)：突出显示由给定Highlight[]阵列。提供空数组或空数组来撤消所有突出显示。
- getHighlighted()：返回Highlight[]数组，该数组包含关于所有突出显示的条目、其x索引和数据集索引的信息。

#### 选择回调
&emsp;OnChartValueSelectedListener,数据被选择时调用
	
	public interface OnChartValueSelectedListener {
	 /**
	  Called when a value has been selected inside the chart.
  	
	  @param e The selected Entry.
	  @param h The corresponding highlight object that contains information
	  about the highlighted position
	 */

		public void onValueSelected(Entry e, Highlight h);

	 /**
	  Called when nothing has been selected or an "un-select" has been made.
	 */
		public void onNothingSelected();
	}

#### 高亮类
&emsp;高亮类能根据x轴y轴以及下标定位需要高亮的点

```java
public Highlight(float x, float y, int dataSetIndex, int dataIndex) {
	this.mX = x;
	this.mY = y;
	this.mDataSetIndex = dataSetIndex;
	this.mDataIndex = dataIndex;
}

public Highlight(float x, float y, int dataSetIndex) {
	this.mX = x;
	this.mY = y;
	this.mDataSetIndex = dataSetIndex;
	this.mDataIndex = -1;
}

public Highlight(float x, int dataSetIndex, int stackIndex) {
	this(x, Float.NaN, dataSetIndex);
	this.mStackIndex = stackIndex;
}

/**
	constructor
     
	@param x            the x-value of the highlighted value
	@param y            the y-value of the highlighted value
	@param dataSetIndex the index of the DataSet the highlighted value belongs to
*/
public Highlight(float x, float y, float xPx, float yPx, int dataSetIndex, YAxis.AxisDependency axis) {
	this.mX = x;
	this.mY = y;
	this.mXPx = xPx;
	this.mYPx = yPx;
	this.mDataSetIndex = dataSetIndex;
	this.axis = axis;
}

/**
	Constructor, only used for stacked-barchart.
	
	@param x            the index of the highlighted value on the x-axis
	@param y            the y-value of the highlighted value
	@param dataSetIndex the index of the DataSet the highlighted value belongs to
	@param stackIndex   references which value of a stacked-bar entry has been selected
*/
public Highlight(float x, float y, float xPx, float yPx, int dataSetIndex, int stackIndex, YAxis.AxisDependency axis) {
	this(x, y, xPx, yPx, dataSetIndex, axis);
	this.mStackIndex = stackIndex;
}
```

&emsp;举个🌰：
	
```java
//find the first point in dataset which position is （2，20）
Highlight highlight = new Highlight(2f,20f,0);

// highlight this value, don't call listener    
lineChart.highlightValue(highlight,false);
```

#### 自定义高亮笔
可以用ChartHighlighter类来定制自己的高亮笔
- setHighlighter(ChartHighlighter highlighter)：：为处理/处理图表视图上执行的所有高亮显示触摸事件的图表设置自定义高亮显示对象。您的自定义荧光笔对象需要扩展ChartHighlighter类。

参考资料：  
[Weeklycoding](https://weeklycoding.com/mpandroidchart-documentation/)
	