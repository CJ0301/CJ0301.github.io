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

#### Activity状态更改
1、当配置发生更改时  
Activity在经历横竖屏变化，语言或输入设备改变时，Activity会被销毁并重新创建， onPause()、onStop() 和 onDestroy() 回调。系统将创建新的 Activity 实例，并触发 onCreate()、onStart() 和 onResume() 回调。  
结合使用 ViewModels、onSaveInstanceState() 方法和/或持久性本地存储，可使 Activity 的界面状态在配置发生更改后保持不变。

2、Activity 或对话框显示在前台  
如果有新的Activity或对话框出现在前台，并且局部覆盖正在进行的Activity，则被覆盖的Activity会市区焦点进入已暂停状态，系统自动调用onPause()。  
当重新获得焦点时，会调用onResume()。
如果有新的Activity或对话框出现在前台，夺取焦点且完全覆盖了正在进行的Activity，则被覆盖的Activity会失去焦点进入已停止状态，然后系统会调用onPause()和onStop()方法。  
当被覆盖的Activity的同一实例返回到前台时，系统会对该Activity调用onRestart()、onStart() 和 onResume()。如果被覆盖的 Activity 的新实例进入后台，则系统不会调用 onRestart()，而只会调用 onStart() 和 onResume()。  
注意：当用户点按“概览”或主屏幕按钮时，系统的行为就好像当前 Activity 已被完全覆盖一样。  

3、用户点返回按钮(有返回虚拟按键的手机)  
如果Activity位于前台，并且用户点按了返回按钮，Activity将一次经历onPause()、onStop() 和 onDestroy() 回调。活动不仅会被销毁，还会从返回堆栈中移除。    
需要注意的是，在这种情况下，默认不会触发 onSaveInstanceState() 回调。此行为基于的假设是，用户点按返回按钮时不期望返回 Activity 的同一实例。不过，您可以通过替换 onBackPressed() 方法实现某种自定义行为，例如“confirm-quit”对话框。  
如果替换 onBackPressed() 方法，我们仍然强烈建议您从被替换的方法调用 super.onBackPressed()。否则，返回按钮的行为可能会让用户感觉突兀。

#### 保存和恢复界面瞬态  
当Activity因系统限制遭到销毁时，应组合使用ViewModel、onSaveInstanceState() 和/或本地存储来保留用户的界面瞬态。 

用户发起的状态解除：  
- 按返回按钮   
- 从最近使用关闭Activity
- 从Activity向上导航
- 从设置屏幕中中止应用
- Activity.finish()

系统发起的状态解除：
-  配置变更(屏幕方向等)  
-  应用切换，同时可能导致系统直接销毁。销毁后会带着存储状态一起销毁

<table>
    <thead>
    <tr>
    <th></th>
    <th>ViewModel</th>
    <th>已保存实例状态</th>
    <th>持久性存储空间</th>
    </tr>
    </thead>

    <tbody>
    <tr>
    <td>存储位置</td>
    <td>在内存中</td>
    <td>已序列化到磁盘</td>
    <td>在磁盘或网络上</td>
    </tr>
    <tr>
    <td>在配置更改后继续存在</td>
    <td>是</td>
    <td>是</td>
    <td>是</td>
    </tr>
    <tr>
    <td>在系统发起的进程终止后继续存在</td>
    <td>否</td>
    <td>是</td>
    <td>是</td>
    </tr>
    <tr>
    <td>在用户完成 Activity 关闭/onFinish() 后继续存在</td>
    <td>否</td>
    <td>否</td>
    <td>是</td>
    </tr>
    <tr>
    <td>数据限制</td>
    <td>支持复杂对象，但是空间受可用内存的限制</td>
    <td>仅适用于基元类型和简单的小对象，例如字符串</td>
    <td>仅受限于磁盘空间或从网络资源检索的成本/时间</td>
    </tr>
    <tr>
    <td>读取/写入时间</td>
    <td>快（仅限内存访问）</td>
    <td>慢（需要序列化/反序列化和磁盘访问）</td>
    <td>慢（需要磁盘访问或网络事务）</td>
    </tr>
    </tbody>
</table>

## Service与AIDL
Service是Android中实现程序后台，与Activity一样执行在UI线程中。
两种状态：
- 启动状态
当应用组件(如Activity)通过调用s

- 绑定状态

## Broadcast
广播是一种广泛运用在应用程序之间传输信息的机制，而BroadcastReceiver是对发送出来的广播进行过滤接收并相应的组件。
