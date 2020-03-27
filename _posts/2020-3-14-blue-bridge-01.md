---
layout: 		post
title: 			"蓝桥杯竞赛准备"
subtitle: 		'关于一些Java常用技巧整理'
author: 		"CJ"
header-img: 	"img/post-bg-java.jpg"
outer-img:		"post-bg-java.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Java
---

## 日期类问题处理
#### 例题1
曾有邪教称1999年12月31日是世界末日。当然该谣言已经不攻自破。

还有人称今后的某个世纪末的12月31日，如果是星期一则会....

有趣的是，任何一个世纪末的年份的12月31日都不可能是星期一!! 

于是，“谣言制造商”又修改为星期日......

1999年的12月31日是星期五，请问：未来哪一个离我们最近的一个世纪末年（即xx99年）的12月31日正好是星期天（即星期日）？

请回答该年份（只写这个4位整数，不要写12月31等多余信息）

思路1：利用Calendar
```java
public class Test {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();// 可用于1970年后操作日期用
		for (int year = 1999; year < 10000; year += 100) {
			calendar.set(Calendar.YEAR, year);
			calendar.set(Calendar.MONTH, 11);// 12月 只有月份是0开始的，0对应1月
			calendar.set(Calendar.DAY_OF_MONTH, 31);
			if (calendar.get(Calendar.DAY_OF_WEEK) == 1) {// 1：星期天 2：星期一 外国人的第一天是星期天
				System.out.println("年份为："+year);
				break;
			}
		}
	}
}
```
知识点：Calendar常见用法如下

1.获取时间
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
```

2.设置时间
```java
	//多字段设置
	Calendar cal = Calendar.getInstance();
    // 如果想设置为某个日期，可以一次设置年月日时分秒，由于月份下标从0开始赋值月份要-1
    // cal.set(year, month, date, hourOfDay, minute, second);
    cal.set(2018, 1, 15, 23, 59, 59);

	//单字段设置
	    // 或者6个字段分别进行设置，由于月份下标从0开始赋值月份要-1
    cal.set(Calendar.YEAR, 2018);
    cal.set(Calendar.MONTH, Calendar.FEBRUARY);
    cal.set(Calendar.DAY_OF_MONTH, 15);
    cal.set(Calendar.HOUR_OF_DAY, 23);
    cal.set(Calendar.MINUTE, 59);
    cal.set(Calendar.SECOND, 59);
    System.out.println(cal.getTime());
```

3.日期加减
```java
    Calendar cal = Calendar.getInstance();
    System.out.println(cal.getTime());
    cal.set(2018, 1, 15, 23, 59, 59);
    cal.add(Calendar.SECOND, 1);
    System.out.println(cal.getTime());
```