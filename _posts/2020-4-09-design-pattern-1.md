---
layout: 		post
title: 			"设计模式"
subtitle: 		'单例设计模式'
author: 		"CJ"
header-img: 	"img/post-bg-cs.jpg"
outer-img:		"post-bg-cs.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - Computer Science
---

## 单例模式
单例模式的实质就是一个类中只有一个实例。  
实现方式：  
1.构造方法私有化，使外部无法通过new关键字实例化该类对象。  
2.类内部产生唯一实例化对象，并封装成private static类型。  
3.定义静态方法返回唯一对象。  

#### 饿汉模式
特点：在使用之前就创建。  
优点：无线程同步问题。  
缺点：一直占用内存。  
```java
package test;
public class Person {
	private static final Person person = new Person();
	private String name;
	
	
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
	//构造函数私有化
	private Person() {
	}
	
	//提供一个全局的静态方法
	public static Person getPerson() {
		return person;
	}
}
```

#### 懒汉模式
特点：延迟加载，使用时才创建。  
优点：节约内存。  
缺点：当两个线程同时判断静态单例对象为空时会出现错误，多线程不安全，需要加入synchronized进行同步。  

线程不安全：
```java
package test;
public class Person2 {
	private String name;
	private static Person2 person;
	
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
	//构造函数私有化
	private Person2() {
	}
	
	//提供一个全局的静态方法
	public static Person2 getPerson() {
		if(person == null) {
			person = new Person2();
		}
		return person;
	}
}
```

线程安全：
```java
package test;
public class Person3 {
	private String name;
	private static Person3 person;
	
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
	//构造函数私有化
	private Person3() {
	}
	
	//提供一个全局的静态方法，使用同步方法
	public static synchronized Person3 getPerson() {
		if(person == null) {
			person = new Person3();
		}
		return person;
	}
}
```

直接在方法上加锁会对性能产生影响，所以锁加在判断里。
优化:
```java
package test;
public class Person4 {
	private String name;
	private static Person4 person;
	
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
	//构造函数私有化
	private Person4() {
	}
	
	//提供一个全局的静态方法
	public static Person4 getPerson() {
		if(person == null) {
			synchronized (Person4.class) {
				if(person == null) {
					person = new Person4();
				}
			}
			
		}
		return person;
	}
}
```