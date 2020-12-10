---
layout: 		post
title: 			"MPAndroidChart_3"
subtitle: 		'图表设定数据以及形式的变化'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
> 既然有了轴，后面肯定要添加数据啦

## 设定数据
#### 表格类型
&emsp;MPAndroidChart提供了九种基本的图表类型，分别为：

- LineChart					曲线图
- BarChart					柱状图
- ScatterChart				散点图
- CandleStickChart			蜡烛图
- PieChart					饼图
- RadarChart				雷达图
- BubbleChart				气泡图
- CombinedChart				综合图
- HorizontalBarChart		水平柱状图

&emsp;在这九类中又分为两个大类，分别为：  

- BarLineChartBase
- PieRadarChartBase

&emsp;第一类包括了LineChart, BarChart, ScatterChart 和 CandleStickChart。  
&emsp;第二类包括了PieChart 和 RadarChart。

#### 数据类型-

<table border="1px" style="border-collapse: collapse;">
		<tr>
            <th>表格类型</th>
            <th>数据类型</th>
        </tr>
        <tr>
            <td>LineChart 曲线图</td>
            <td rowspan="2">Enrty</td>
        </tr>
        <tr>
            <td>ScatterChart 散点图</td>
        </tr>
        <tr>
            <td>BarChart 柱状图</td>
            <td rowspan="2">BarEntry</td>
        </tr>
        <tr>
            <td>HorizontalBarChart 水平柱状图</td>
        </tr>
        <tr>
            <td>CandleStickChart 蜡烛图</td>
            <td>CandleEntry</td>
        </tr>
        <tr>
            <td>PieChart 饼图</td>
            <td>PieEntry</td>
        </tr>
        <tr>
            <td>RadarChart 雷达图</td>
            <td>RaderEntry</td>
        </tr>
        <tr>
            <td>BubbleChart 气泡图</td>
            <td>BubbleEntry</td>
        </tr>
        <tr>
            <td>CombinedChart 综合图</td>
            <td>比较特殊</td>
        </tr>
    </table>

## 实例🌰
#### Entry
&emsp;曲线图

```java
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
Highlight highlight = new Highlight(2f,20f,0);
lineChart.setData(lineData);
lineChart.highlightValue(highlight,false);
lineChart.invalidate();
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200209_simple_chart.png)

&emsp;散点图

```java
scatterChart = findViewById(R.id.scatterChart);
List<Entry> entries = new ArrayList<>();
entries.add(new Entry(1,20f));
entries.add(new Entry(2,14f));
entries.add(new Entry(3,26f));
entries.add(new Entry(4,10f));
entries.add(new Entry(5,30f));

ScatterDataSet scatterDataSet = new ScatterDataSet(entries,"参数1");

ScatterData scatterData = new ScatterData();
scatterData.addDataSet(scatterDataSet);
scatterChart.setData(scatterData);
scatterChart.invalidate();
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_scatterChart.png)

#### BarEntry
&emsp;柱状图

```java
barChart = findViewById(R.id.barChart);
List<BarEntry> barEntries = new ArrayList<>();
barEntries.add(new BarEntry(1,20));
barEntries.add(new BarEntry(2,45));
barEntries.add(new BarEntry(3,23));
barEntries.add(new BarEntry(4,30));
barEntries.add(new BarEntry(5,16));

BarDataSet barDataSet = new BarDataSet(barEntries,"参数1");

BarData barData = new BarData();
barData.addDataSet(barDataSet);
barChart.setData(barData);
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_barChart.png)

&emsp;水平柱状图

```java
hBarChart = findViewById(R.id.hBarChart);
List<BarEntry> barEntries = new ArrayList<>();
barEntries.add(new BarEntry(1,20));
barEntries.add(new BarEntry(2,45));
barEntries.add(new BarEntry(3,23));
barEntries.add(new BarEntry(4,30));
barEntries.add(new BarEntry(5,16));

BarDataSet barDataSet = new BarDataSet(barEntries,"参数1");

BarData barData = new BarData();
barData.addDataSet(barDataSet);
hBarChart.setData(barData);
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_hBarChart.png)

#### CandleEntry
&emsp;这一块太复杂了，以后有机会再更新

#### PieEntry
&emsp;饼图

```java
pieChart = findViewById(R.id.pieChart);
List<PieEntry> pieEntries = new ArrayList<>();
pieEntries.add(new PieEntry(35,"参数1"));
pieEntries.add(new PieEntry(60,"参数2"));

PieDataSet pieDataSet = new PieDataSet(pieEntries,"标签");
pieDataSet.addColor(Color.GREEN);//必须要加颜色

PieData pieData = new PieData();
pieData.addDataSet(pieDataSet);
pieChart.setData(pieData);
```
![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_pieChart.png)

#### RadarEntry
&emsp;雷达图

```java
radarChart = findViewById(R.id.radarChart);
List<RadarEntry> radarEntries = new ArrayList<>();
radarEntries.add(new RadarEntry(20));
radarEntries.add(new RadarEntry(32));
radarEntries.add(new RadarEntry(25));
radarEntries.add(new RadarEntry(10));
radarEntries.add(new RadarEntry(18));

RadarDataSet radarDataSet = new RadarDataSet(radarEntries,"参数1");

RadarData radarData = new RadarData();
radarData.addDataSet(radarDataSet);
radarChart.setData(radarData);
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_radarChart.png)

#### BubbleEntry
&emsp;气泡图

```java
bubbleChart = findViewById(R.id.bubbleChart);
ArrayList<BubbleEntry> yVals = new ArrayList<BubbleEntry>();

ArrayList<BubbleEntry> yVals_blue = new ArrayList<BubbleEntry>();
ArrayList<BubbleEntry> yVals_yellow = new ArrayList<BubbleEntry>();
ArrayList<BubbleEntry> yVals_red = new ArrayList<BubbleEntry>();

for (int i = 0; i < 10; i++) {
	float val = (float) (Math.random() * 100);
	yVals.add(new BubbleEntry(i + 1, val, val));
}

for (int i = 0; i < yVals.size(); i++) {
	BubbleEntry bubbleEntry = yVals.get(i);
	if (bubbleEntry.getY() <= 100 / 3) {
		yVals_red.add(bubbleEntry);
	} else if (bubbleEntry.getY() > 100 / 3 && bubbleEntry.getY() <= 200 / 3) {
		yVals_yellow.add(bubbleEntry);
	} else if (bubbleEntry.getY() > 200 / 3) {
		yVals_blue.add(bubbleEntry);
	}
}


BubbleDataSet set1 = new BubbleDataSet(yVals_blue, "优秀");
set1.setDrawIcons(false);
set1.setColor(Color.BLUE, 100);
set1.setDrawValues(true);

BubbleDataSet set2 = new BubbleDataSet(yVals_yellow, "良好");
set2.setDrawIcons(false);
set2.setColor(Color.YELLOW, 100);
set2.setDrawValues(true);

BubbleDataSet set3 = new BubbleDataSet(yVals_red, "很差");
set3.setDrawIcons(false);
set3.setColor(Color.RED, 100);
set3.setDrawValues(true);

ArrayList<IBubbleDataSet> dataSets = new ArrayList<IBubbleDataSet>();
dataSets.add(set1);
dataSets.add(set2);
dataSets.add(set3);

BubbleData bubbleData = new BubbleData(dataSets);
bubbleChart.setData(bubbleData);
```


![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200210_bubbleChart.png)

## 设置颜色
&emsp;这一块感觉没啥好讲的，在相应的dataset上添加颜色，如果不添加就会使用默认颜色。一般在数据集多的时候会使用，饼图是肯定要用到的，毕竟至少有两个数据。    
&emsp;颜色的选择可以用这个开源框架下的ColorTemplate类，也可以用自带的Color类。

## 值的形式
&emsp;ValueFormatter类可以帮助我们改变DataSets数据集和轴的数据形式。  
&emsp;使用方式为将重写好的ValueFormatter子类通过setValueFormatter设置。


