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

DCL(Double Check Lock)实现单例
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

#### 静态内部类单例模式
DCL在某种情况下还是会出现失效的情况，建议用以下代码代替。
```java
public class Singleton{
	private Singleton(){}
	public static Singleton getInstance(){
		return SingletonHolder.sInstance;
	}

	//静态内部类
	private static class SingletonHolder{
		private static final Singleton sInstance = new Singleton();
	}
}
```

当第一次加载Singleton类并不会初始化sInstance，只有调用getInstance时才会导致sInstance被初始化。

#### 枚举单例
有一种更简单的实现单例的方法。
```java
public enum SingletonEnum{
	INSTANCE;
	public void doSomething(){
		
	}
}
```

枚举实例的创建默认都是线程安全的，而上述的其他单例模式实现中，都可以用反序列化来重新创建对象。  
杜绝这种情况就要重写readResolve方法。  
```java
private Object readResolve() throws ObjectStreamException{
	return sInstance;
}
```

#### 容器实现单例模式
```java
public class SingletonManager{
	private static Map<String,Object> objMap = new HashMap<String,Object>();

	private SingletonManager(){}
	public static void registerService(String key,Object instance){
		if(!objMap.containsKey(key)){
			objMap.put(key,instance);
		}
	}
	
	public static Object getService(){
		return objMap.get(key);	
	}
}
```

直接将单例对象存入一个集合中统一管理，使用时也可以用统一的接口操作，降低使用成本。