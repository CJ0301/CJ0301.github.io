---
layout: 		post
title: 			"Java的日期处理"
subtitle: 		'关于一些日期使用的处理'
author: 		"CJ"
header-img: 	"img/post-bg-java.jpg"
outer-img:		"post-bg-java.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Java
---

> 在Java中有三个用于处理时间的类：`Date`,`Calender`,`Time`。分别出现于`1.1`,`1.2`,`1.8`版本。

## 日期与实践API
#### 时间线
Java的Date和Time API规范要求Java使用的时间尺度为：
- 每天866400秒
- 每天正午时间与官方时间精确匹配
- 在其他时间点上，以精确定义的方式与官方时间接近匹配

在Java中Instant类表示时间线上的某个点，用于作为时间戳。Duration类是两个时刻之间的时间差。二者一起使用可计算算法的运行时间：

```java
Instant start = Instant.now();
//执行算法...

Instant end = Instant.now();
Duration timeElapsed = Duration.between(start,end);
long millis = timeElapsed.toMillis();
```

用于时间的Instant和Duration的算术运算

<table>
    <thead>
        <td>方法</td>
        <td>描述</td>
    </thead>
    <tr>
        <td>plus,minus</td>
        <td>在当前的Instant或Duration上加上或减去一个时间</td>
    </tr>
    <tr>
        <td>toNanos,toMillis,getSeconds,toMinutes,toHours,toDays</td>
        <td>获取Duration按照传统单位度量的时间</td>
    </tr>
    <tr>
        <td>plusNanos,plusMillis,plusSeconds...</td>
        <td>给当前Instant或Duration加上或减去给定时间单位的数值</td>
    </tr>
    <tr>
        <td>multipliedBy,dividedBy,negated</td>
        <td>返回当前Duration乘或除以给定long或-1而得到的Duration(Instant无法缩放)</td>
    </tr>
    <tr>
        <td>isZero,isNegative</td>
        <td>检查当前Duration是否是0或负值</td>
    </tr>
</table>

#### 本地时间
Java API中有两种人类时间，本地日期/时间和时区时间。  
LocalDate是带有年、月、日的日期。构建可使用now或of方法。  

LocalDate的方法
<table>
    <thead>
        <td>方法</td>
        <td>描述</td>
    </thead>
    <tr>
        <td>now,of</td>
        <td>用当前时间构建LocalDate或用年月日构建，月份用通常使用的数字(例如一月用1)或者用Month枚举</td>
    </tr>
    <tr>
        <td>plusDays,plusWeeks,minusDays...</td>
        <td>给当前LocalDate上加减一定的天、星期、月或年</td>
    </tr>
    <tr>
        <td>plus,minus</td>
        <td>加减一个Duration或Period</td>
    </tr>
    <tr>
        <td>withDayOfMonth,withDayOfYear...</td>
        <td>返回新的LocalDate,其对应的值修改为给定值</td>
    </tr>
    <tr>
        <td>getDayOfMonth,getDayOfYear</td>
        <td>获取对应值</td>
    </tr>
	<tr>
        <td>until</td>
        <td>获取Period或两个日期按指定ChronoUnits计算的数值</td>
    </tr>
	<tr>
        <td>isBefore,isAfter</td>
        <td>将两个LocalDate进行比较</td>
    </tr>
	<tr>
        <td>isLeapYear</td>
        <td>是否是闰年</td>
    </tr>
</table>

相关的知识点还有日期调整器TemporalAdjusters类，当日时刻LocalTime类，时区时间ZonedDateTime类。由于最近不常用，就不深入研究了。

#### 格式化与解析
DateTimeForMatter类提供了三种用于打印日期/时间值的格式器：
- 预定义的格式器
- Locale相关的格式器
- 带有定制模式的格式器

常用的是使用他的子类SimpleDateFormat
```java
import java.text.*;
import java.util.Date;

/**
  SimpleDateFormat函数语法：
 
  G 年代标志符
  y 年
  M 月
  d 日
  h 时 在上午或下午 (1~12)
  H 时 在一天中 (0~23)
  m 分
  s 秒
  S 毫秒
  E 星期
  D 一年中的第几天
  F 一月中第几个星期几
  w 一年中第几个星期
  W 一月中第几个星期
  a 上午 / 下午 标记符
  k 时 在一天中 (1~24)
  K 时 在上午或下午 (0~11)
  z 时区
 */
public class FormatDateTime {

    public static void main(String[] args) {
        SimpleDateFormat myFmt=new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒");
        SimpleDateFormat myFmt1=new SimpleDateFormat("yy/MM/dd HH:mm");
        SimpleDateFormat myFmt2=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//等价于now.toLocaleString()
        SimpleDateFormat myFmt3=new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒 E ");
        SimpleDateFormat myFmt4=new SimpleDateFormat(
                "一年中的第 D 天 一年中第w个星期 一月中第W个星期 在一天中k时 z时区");
        Date now=new Date();
        System.out.println(myFmt.format(now));
        System.out.println(myFmt1.format(now));
        System.out.println(myFmt2.format(now));
        System.out.println(myFmt3.format(now));
        System.out.println(myFmt4.format(now));
        System.out.println(now.toGMTString());
        System.out.println(now.toLocaleString());
        System.out.println(now.toString());
    }   
}
```

#### Calendar和Date

常见使用方式： 
 
Date:  
```java
Date date = new Date();
System.out.println("毫秒:"+date.getTime());//输入毫秒
 
//时间转字符串
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
String time = sdf.format(date);
System.out.println("时间转字符串:"+time);
 
//利用字符串来转时间格式（记得抛出异常）
String time02 = "2018-09-05";
SimpleDateFormat  sdf2 = new SimpleDateFormat ("yyyy-MM-dd");
Date date2 = sdf2.parse(time02);
System.out.println("字符串转时间格式："+date2);
```

Calendar:

```java
// 使用默认时区和语言环境获得一个日历
Calendar cal = Calendar.getInstance();
// 赋值时年月日时分秒常用的6个值，注意月份下标从0开始，所以取月份要+1
System.out.println("年:" + cal.get(Calendar.YEAR));
System.out.println("月:" + (cal.get(Calendar.MONTH) + 1));
System.out.println("日:" + cal.get(Calendar.DAY_OF_MONTH));
System.out.println("时:" + cal.get(Calendar.HOUR_OF_DAY));
System.out.println("分:" + cal.get(Calendar.MINUTE));
System.out.println("秒:" + cal.get(Calendar.SECOND));
//手动设置某个日期
Calendar cal02 = Calendar.getInstance();
//注意，设置时间的时候月份的下标是在0开始的
//设置时间不一定要这6个参数3个参数也是可以的
cal02.set(2018,9,1,12,0,0);//二零一八年十月一号十二点
System.out.println(cal02.getTime());
```

Date和Calendar互相转换:
```java
//calendar转date
Calendar cal = Calendar.getInstance();
Date date = cal.getTime();

Calendar cal = Calendar.getInstance();
Date date = cal.getTime();
SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");
String s = simpleDateFormat.format(date);
System.out.println("时间为===="+s);

//date转calendar
Date date2 = new Date();
Calendar cal2 = Calendar.getInstance();
cal2.setTime(date);


Date date2 = new Date();
Calendar cal2 = Calendar.getInstance();
cal2.setTime(date);
System.out.println(cal2.get(Calendar.YEAR) +"-"+(cal2.get(Calendar.MONTH)+1)+"-"+cal2.get(Calendar.DATE));
```



