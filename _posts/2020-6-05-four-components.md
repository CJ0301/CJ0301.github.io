---
layout: 		post
title: 			"Android四大组件"
subtitle: 		'Activity、Service、Broadcast、Content Provider'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---

## Activity
Activity在应用中就是一个用户界面，加载与显示各类的UI组件。  
应用加载启动会有一个默认的Activity作为启动项，必须要有这个配置：  
```xml
<intent-filter>
	<action android:name="android.intent.action.MAIN" />
	<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

#### 生命周期
![Activity 生命周期的简化图示](https://developer.android.com/guide/components/images/activity_lifecycle.png)

Activity 类提供六个核心回调：onCreate()、onStart()、onResume()、onPause()、onStop() 和 onDestroy()。当 Activity 进入新状态时，系统会调用每个回调。

1.onCreate()    
第一次创建Activity时调用，通常完成Activity的初始化操作。

2.onStart()  
在onCreate()之后调用，此时Activity还处于不可见，他的下一个状态就是Activity可见的时候。

3.onResume()  
这个函数在Activity变为可见时被调用，执行完后，Activity会请求AMS渲染它所管理的视图。此时Activity一定位于返回栈的栈顶，并且处于运行状态。  

4.onPause()  
这个函数在系统准备去启动或恢复另一个Activity时调用，也就是Activity即将从可见状态变为不可见状态时。通常会在这个函数将一些消耗CPU的资源释放吊，以及保存一些关键数据。

5.onStop()
这个函数在Activity完全不可见时调用。它和onPause()函数的区别在于，如果新启动的Activity是一个对话框式的Activity，那么onPause()函数会得到执行，而onStop()函数并不会执行。

6.onDestory()
这个函数在Activity被销毁时调用，之后Activity的状态将变为销毁状态。

7.onRestart()
这个函数在Activity由停止状态重新变为运行状态时调用。

#### 信息传递
1.Intent传输
MainActivity
```java
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
intent.putExtra("data","Hello");
startActivity(intent);
```

SecondActivity
```java
Intent intent = getIntent();
String message = intent.getStringExtra("data");
```

2.Bundle传输
MainActivity
```java
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
Bundle b = new Bundle();
b.putString("name","cj");
b.putInt("age",2);

//第一种
//intent.putExtras(b);

//第二种
intent.putExtra("data",b);

startActivity(intent);
```

SecondActivity
```java
Intent intent = getIntent();

//第一种
//Bundle data = intent.getExtras();

//第二种
Bundle data = intent.getBundleExtra("data");

String message = data.getString("name");//也可以加一个默认参数防止数据不存在
```

3.对象直接传输
MainActivity
```java
Intent intent = new Intent(MainActivity.this,SecondActivity.class);
intent.putExtra("user",new User("xxx",2));
```

SecondActivity
```java
User user = (User)i.getSerializableExtra("user");
```

User.java
```java
public class User implements Serializable {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

4.自己实现序列化接口
```java
public class User implements Parcelable {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(getName());
        dest.writeInt(getAge());
        //如果有多个同类型属性，就用writeBundle
    }

    public static final Creator<User> CREATOR = new Creator<User>(){

        @Override
        public User createFromParcel(Parcel source) {

            return new User(source.readString(),source.readInt());
        }

        @Override
        public User[] newArray(int size) {
            return new User[size];
        }
    };
}

```

SecondActivity改一行就好了
```java
User user = intent.getParcelableExtra("user");
```

这个写法效率比Serializable高，就是麻烦点。

回传数据
MainActivity
```java
startActivityForResult(i,0);
```

```java
@Override
protected void onActivityResult(int requestCode, int resultCode,Intent data) {
	super.onActivityResult(requestCode, resultCode, data);
    if(resultCode == 1)
		Log.i("result",requestCode+"   "+data.getStringExtra("data"));
	 
}
```

SecondActivity
```java
Intent i = new Intent();
i.putExtra("data","xxx");
setResult(1,i);
finish();
```