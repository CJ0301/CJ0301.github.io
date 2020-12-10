---
layout: 		post
title: 			"MPAndroidChart_2"
subtitle: 		'关于轴基与XY轴'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
> 目录太长了然后出现滑动条了，感觉有点丑，就分多篇来写吧

## 轴
#### 轴基(AxisBase)
&emsp;以下方法可应用与两个轴  

&emsp;Axis类允许特定的样式，由以下组件/部件组成(可以包括)：

- 标签(以垂直(y-轴)或水平(x-轴)对齐方式绘制)，其中包含轴描述值。
- 一种所谓的“轴线”，它直接画在标签旁边并与标签平行。
- “网格线”，每条线都来自于水平方向的轴标签。
- LimitLines，允许呈现特殊的信息，如边界或约束。

#### 控制应绘制(轴的)哪些部分
- setEnabled(boolean enabled)：设置启用或禁用轴。如果禁用，则不管其他设置如何，都不会绘制轴的任何部分。
- setDrawLabels(boolean enabled)：将此设置为true，以启用绘制轴的标签。
- setDrawAxisLine(boolean enabled)：如果沿轴线(轴线线)是否应该绘制，则将其设置为true。
- setDrawGridLines(boolean enabled)：将其设置为true，以启用设置轴的网格线。

#### 自定义轴范围(最小/最大)
- setAxisMaximum(float max)：设置此轴的自定义最大值。如果设置了该值，则不会根据所提供的数据自动计算此值。
- resetAxisMaximum()：调用它以撤消以前设置的最大值。通过这样做，您将再次允许轴自动计算它的最大值。
- setAxisMinimum(float min)：设置此轴的自定义最小值。如果设置了该值，则不会根据所提供的数据自动计算此值。
- resetAxisMinimum()调用它以撤消以前设置的最小值。通过这样做，您将再次允许轴自动计算它的最小值。
- setStartAtZero(boolean enabled)：弃用-使用setAxisMinValue(...)或setAxisMaxValue(...)相反。
- setInverted(boolean enabled)：如果设置为真，这个轴将反转，这意味着最高的值将在底部，最低的值在顶部。
- setSpaceTop(float percent)：设置图表中最高值的顶部间距(占总轴范围的百分比)，与轴上的最高值相比。
- setSpaceBottom(float percent)：将图表中最低值的底部间距(以总轴范围的百分比)与轴上的最低值相比较。
- setShowOnlyMinMax(boolean enabled)如果启用，此轴将只显示它的最小值和最大值。这将忽略/覆盖定义的标签计数(如果不是强制的话)。
- setLabelCount(int count, boolean force)：设置y轴的标签数。请注意，这个数字不是固定的(如果force==false)，并且只能近似。如果启用了强制(True)，则会绘制精确的标签计数--这会导致轴上的不均匀数字。
- setPosition(YAxisLabelPosition pos)：设置绘制轴标签的位置。内部图表或外部图表。
- setGranularity(float gran)：设置y轴值之间的最小间隔。这可用于避免在缩放到为轴设置的小数数不再允许区分两个轴值时重复值。
- setGranularityEnabled(boolean enabled)：启用粒度特性，在缩放时限制y轴的间隔。默认值：false

#### 格式化轴值
&emsp;使用ValueFormatter类，进行坐标信息显示的定制  

&emsp;举个🌰：
```java
xAxis.setValueFormatter(new IAxisValueFormatter() {
	@Override
	public String getFormattedValue(float v, AxisBase axisBase) {
		return v==0?"个数":v==6?"(星期)":(int)v+"";
	}
});
```
	

#### 警戒线
&emsp;在x轴或者y轴添加边线或者警戒线。

- addLimitLine(LimitLine l)*增加一个新的LimitLine到这个轴。
- removeLimitLine(LimitLine l)*移除指定的LimitLine从这个轴。
添加/删除可用的更多方法。
- setDrawLimitLinesBehindData(boolean enabled)：允许控制LimitLines和实际数据。如果此值设置为true，则LimitLines则绘制在实际数据后面，否则绘制在顶部。默认值：false  

&emsp;举个🌰：
```java
YAxis leftAxis = chart.getAxisLeft();
LimitLine ll = new LimitLine(140f, "Blood Pressure High");
ll.setLineColor(Color.RED);
ll.setLineWidth(4f);
ll.setTextColor(Color.BLACK);
ll.setTextSize(12f);
// .. and more styling options
leftAxis.addLimitLine(ll);
```
## XAxis
&emsp;XAxis继承自[AxisBase](#轴基(AxisBase))，是与水平轴相关的所有内容的数据和信息容器。
&emsp;这个XAxis类允许特定的样式，并由以下组件/部件组成(可以由以下组件/部件组成)：

- 一种所谓的“轴线”，它直接画在标签旁边并与标签平行。
- “网格线”，每条线都来自垂直方向的轴标签。

&emsp;获取XAxis实例

```java
XAxis xAxis = chart.getXAxis();

```
#### 自定义轴值
- setLabelRotationAngle(float angle)：设置绘制x轴标签的角度(以度数为单位)。
- setPosition(XAxisPosition pos)：设置XAxis应该出现。在顶部、底部、两边、顶部、内部或底部之间进行选择。

&emsp;举个🌰：
```java
XAxis xAxis = chart.getXAxis();
xAxis.setPosition(XAxisPosition.BOTTOM);
xAxis.setTextSize(10f);
xAxis.setTextColor(Color.RED);
xAxis.setDrawAxisLine(true);
xAxis.setDrawGridLines(false);
// set a custom value formatter
xAxis.setValueFormatter(new MyCustomFormatter()); 
// and more...
```
## YAxis
&emsp;YAxis也继承自[AxisBase](#轴基(AxisBase))，是与垂直轴相关的所有内容的数据和信息容器。有一些图表有左右轴，像雷达图只有一个轴。默认情况下两个轴都会被画出来

&emsp;获取YAxis实例

```java
YAxis leftAxis = chart.getAxisLeft();
YAxis rightAxis = chart.getAxisRight();
YAxis leftAxis = chart.getAxis(AxisDependency.LEFT);
YAxis yAxis = radarChart.getYAxis(); // this method radarchart only
```

Tips：

- 在运行时，使用```public AxisDependency getAxisDependency()```决定用哪个轴。
- 如果想让定制对轴的范围生效则需要在设置数据之前

#### 轴相依性
&emsp;默认情况下，添加到图表的所有数据均相对于图表的左侧YAxis进行绘制。 如果未进一步指定和启用，则将调整右Y轴以表示与左轴相同的比例。

&emsp;如果您的图表需要支持不同的轴比例，则可以通过设置数据应绘制的轴来实现。 这可以通过更改DataSet对象的AxisDependency来完成：

```java
LineDataSet dataSet = ...; // get a dataset
dataSet.setAxisDependency(AxisDependency.RIGHT);

```
#### 零线
&emsp;除了网格线，YAxis还有一个零线可单独配置

- setDrawZeroLine(boolean enabled)：：启用/禁用绘制零线。
-  setZeroLineWidth(float width)：：设置零行的线宽。
- setZeroLineColor(int color)：：设置零行应该具有的颜色。

&emsp;举个🌰：

```java
// data has AxisDependency.LEFT
YAxis left = mChart.getAxisLeft();
left.setDrawLabels(false); // no axis labels
left.setDrawAxisLine(false); // no axis line
left.setDrawGridLines(false); // no grid lines
left.setDrawZeroLine(true); // draw a zero line
mChart.getAxisRight().setEnabled(false); // no right axis
```

&emsp;更多的🌰：

```java
YAxis yAxis = mChart.getAxisLeft();
yAxis.setTypeface(...); // set a different font
yAxis.setTextSize(12f); // set the text size
yAxis.setAxisMinimum(0f); // start at zero
yAxis.setAxisMaximum(100f); // the axis maximum is 100
yAxis.setTextColor(Color.BLACK);
yAxis.setValueFormatter(new MyValueFormatter());
yAxis.setGranularity(1f); // interval 1
yAxis.setLabelCount(6, true); // force 6 labels
//... and more
```
