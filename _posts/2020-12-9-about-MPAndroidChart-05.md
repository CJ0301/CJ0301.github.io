---
layout: 		post
title: 			"MPAndroidChart_4"
subtitle: 		'图表造型的美化'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
> 有了数据，下一步就是美化了

## 一般设置与造型
#### 刷新
- invalidate()：在图表上调用此方法将刷新(重画)它。为了使图表上执行的更改生效，需要这样做。
- notifyDataSetChanged()：让图表知道它的底层数据已经改变，并执行所有必要的重新计算(偏移、图例、极大值、最小值、…)。这是必要的，特别是当动态添加数据.

#### 日志打印
- setLogEnabled(boolean enabled)：将此设置为true将激活图表logcat输出。启用此功能对性能不利，如果没有必要，请保持禁用状态。

#### 通用图表造型

- setBackgroundColor(int color)：设置涵盖整个图表视图的背景色。此外，背景颜色可以通过.xml在布局文件中。
- setDescription(String desc)：设置显示在图表右下角的描述文本。
- setDescriptionColor(int color)：设置描述文本的颜色。
- setDescriptionPosition(float x, float y)：设置屏幕上以像素为单位的描述文本的自定义位置。
- setDescriptionTypeface(Typeface t)：设置Typeface用于绘制描述文本。
- setDescriptionTextSize(float size)：设置描述文本的大小，以像素为单位，最小为6f，最大为16F。
- setNoDataText(String text)：设置在图表为空时应显示的文本。
- setDrawGridBackground(boolean enabled)：如果启用，图表绘制区域后面的背景矩形将被绘制.
- setGridBackgroundColor(int color)：设置网格背景应使用的颜色。
- setDrawBorders(boolean enabled)：启用/禁用绘制图表边框(围绕图表的线条)。
- setBorderColor(int color)：设置图表边框的颜色。
- setBorderWidth(float width)：设置DP中图表边框的宽度。
- setMaxVisibleValueCount(int count)：设置图表上的最大可视绘制值-标签数。这只在setDrawValues()已启用。

## 特殊的造型设置
#### Line-, Bar-, Scatter-, Candle- & BubbleChart
- setAutoScaleMinMaxEnabled(boolean enabled)：指示是否启用y轴自动缩放的标志。如果启用，y轴将自动调整到当前x轴范围的最小和最大y值，只要视图改变。这对于显示金融数据的图表尤其有趣。默认值：false
- setKeepPositionOnRotation(boolean enabled)：设置图表是否应在改变方向后保持其位置(缩放/滚动)。默认值：false

#### BarChart
- setDrawValueAboveBar(boolean enabled)：如果设置为true，则所有值都绘制在它们的条形图之上，而不是在其顶部下面。
- setDrawBarShadow(boolean enabled)：如果设置为true，则在指示最大值的每个栏后面绘制灰色区域。使他的表现下降约40%。
- setDrawValuesForWholeStack(boolean enabled)：如果设置为真，则所有叠加栏的值都是单独绘制的，而不仅仅是它们的总和。
- setDrawHighlightArrow(boolean enabled)：将此设置为true，以便在高亮显示时将高亮箭头绘制在每个条形图上方。

#### PieChart
- setDrawSliceText(boolean enabled)：将其设置为true，将x值文本绘制到饼片中。
- setUsePercentValues(boolean enabled)：如果启用，图表中的值是以百分比绘制的，而不是用原始值绘制的。为ValueFormatter然后以百分比提供格式。
- setCenterText(SpannableString text)：设置在分段中间绘制的文本。较长的文本将自动“包装”，以避免剪裁到饼片。
- setCenterTextRadiusPercent(float percent)：将中间文本的边框的矩形半径设置为饼孔默认为1.f(100%)的百分比。
- setHoleRadius(float percent)：以最大半径的百分比(max=整个图表的半径)设置分段中心的孔半径，默认为50%。
- setTransparentCircleRadius(float percent)：以最大半径的百分比(max=整个图表的半径)为单位，设置在圆孔旁边绘制的透明圆的半径，默认为55%->意味着默认情况下比中心孔大5%。
- setTransparentCircleColor(int color)：设置透明圆圈的颜色。
- setTransparentCircleAlpha(int alpha)：设置透明圈应该具有的透明度(0-255)。
- setMaxAngle(float maxangle)：设置用于计算饼圆的最大角度。360 F意味着它是一个满的PieChart，180 F的结果是半饼图。默认：360 F

#### RadarChart
- setSkipWebLineCount(int count)：允许跳过来自图表中心的网页线。如果有很多行的话，特别有用。

## 图例
&emsp;默认情况下，每一个图表在设置完数据后会生成一个图例。图例通常由多个条目组成，每个条目由一个标签、一个窗体/形状表示。  
&emsp;图例生成的条目数量取决于不同颜色（跨所有DataSet对象）的数目以及DataSet标签。 图例的标签取决于为图表中使用的DataSet对象设置的标签。 如果没有为DataSet对象指定标签，则图表将自动生成它们。 如果一个数据集使用了多种颜色，则这些颜色将被分组，并且仅由（属于）一个标签来描述。 

&emsp;获取Legend类

	Legend legend = chart.getLegend();

#### 画图例
- setEnabled(boolean enabled)：设置Legend启用或禁用。如果禁用，则Legend不会被画。

#### 修改图例样式
- setTextColor(int color)：设置图例标签的颜色。
- setTextSize(float size)：在dp中设置图例标签的文本大小。
- setTypeface(Typeface tf)：设置字体。

#### 避免包装/修剪
- setWordWrapEnabled(boolean enabled)：如果启用，图例的内容将不会夹在图表边界之外，而是创建一个新的行。请注意，这会降低性能，并且只适用于图表下面的图例。
- setMaxSizePercent(float maxSize)：以百分比为单位，将整个图表视图中的最大相对大小设置为百分比。默认：0.95f(95%)

#### 定制图例
- setPosition(LegendPosition pos)：设置LegendPosition，它定义了Legend应该出现。在右图、右图_中心、右_图_内、__图表_左、下面__图表_右、__图表_中心以下或分段中心之间进行选择(PieChart)，…还有更多。
- setForm(LegendForm shape)：设置LegendForm应该用它。此形状是在图例标签旁边绘制的，颜色为DataSet图例-条目代表。在正方形、圆形或直线之间进行选择。
- setFormSize(float size)：在DP中设置图例窗体的大小。
- setXEntrySpace(float space)：设置水平轴上图例-条目之间的空间。
- setYEntrySpace(float space)：在垂直轴上设置图例-条目之间的空间。
- setFormToTextSpace(float space)：设置图例标签与相应图例格式之间的空格。
- setWordWrapEnabled(boolean enabled)：传奇词应该包装吗？/目前只支持BelowChartLeft、BelowChartRight、BelowChartCenter。/您可能希望在单词包装时设置maxSizePerse，以设置文本包装的点。

#### 自定义标签和颜色
- setCustom(int[] colors, String[] labels)：设置自定义图例的标签和颜色数组。颜色计数应与标签计数相匹配。每种颜色都是在同一索引处绘制的窗体的颜色。空标签将启动一个组。(-2)颜色将避免绘制表单，这将禁用自动从数据集中计算图例标签和颜色的功能。打电话resetCustom()重新启用自动计算(然后notifyDataSetChanged()是自动计算图例所必需的)
- resetCustom()：调用这将禁用自定义图例标签(由setCustom(...))。相反，标签将再次自动计算(在notifyDataSetChanged()被称为)。
- setExtra(int[] colors, String[] labels)：设置将在计算图例后追加到自动计算的颜色和标签数组末尾的颜色和标签。(如果图例已经计算过，则需要调用notifyDataSetChanged()使更改生效)

&emsp;举个🌰：

	Legend l = chart.getLegend();
	l.setFormSize(10f); // set the size of the legend forms/shapes
	l.setForm(LegendForm.CIRCLE); // set what type of form/shape should be used
	l.setPosition(LegendPosition.BELOW_CHART_LEFT);
	l.setTypeface(...);
	l.setTextSize(12f);
	l.setTextColor(Color.BLACK);
	l.setXEntrySpace(5f); // space between the legend entries on the x-axis
	l.setYEntrySpace(5f); // space between the legend entries on the y-axis
    // set custom labels and colors
	 l.setCustom(ColorTemplate.VORDIPLOM_COLORS, new String[] { "Set1", "Set2", "Set3", "Set4", "Set5" });
    // and many more...

## 解释
&emsp;默认在表格的右下角会有个小标签，没多少可讲的，主要就是获取：
	
	Description description = chart.getDescription();

&emsp;与样式：

	// enable or disable the description
	description.setEnabled(...);
	// set the description text
	description.setText("...");
	// set the position of the description on the screen
	description.setPosition(float x, float y);

## 动画
&emsp;为了优化用户体验，我们还可以加一些动画。  
&emsp;动画主要分为X轴和Y轴： 
 
- animateX(int durationMillis)：：在水平轴上动画图表值，这意味着图表将在指定的时间内从左到右建立起来。
- animateY(int durationMillis)：：在垂直轴上动画图表值，这意味着图表将在指定的时间内从下到上建立起来。
- animateXY(int xDuration, int yDuration)：：动画的水平和垂直轴，导致左/右，底部/上建。

	mChart.animateX(3000); // animate horizontal 3000 milliseconds
	// or:
	mChart.animateY(3000); // animate vertical 3000 milliseconds
	// or:
	mChart.animateXY(3000, 3000); // animate horizontal and vertical 3000 milliseconds

&emsp;动画的减缓效果都在Easing类里，这里就不多做尝试了。

#### 定制自己的动画
&emsp;作者留了一个EasingFunction接口，有兴趣的可以自己研究一下