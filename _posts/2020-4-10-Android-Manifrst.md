---
layout: 		post
title: 			"Android的配置"
subtitle: 		'安卓常见配置信息'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## Manifest
#### 全局
应用的报名以及版本信息管理  
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp"
    android:versionCode="1"
    android:versionName="1.0" >
    ...
</manifest>
```
xmlns:android、package  
xmlns:android与package都是由系统默认生成的，一般不需要修改。  
package在构建APK的时候，系统会做两件事：
1. 生成R.java类，🌰：com.example.myapp会生成com.example.myapp.R
2. 用来生成定义类的完整类名，🌰：<activity android:name=".MainActivity">，完整的类名就是com.example.myapp.MainActivity
注意：在APK构建的最后一步，package会被build.gradle中的applicationId属性取代，所以二者要保持一致。

android:versionCode  
内部版本号，不显示给用户

android:versionName  
显示给用户看的版本号。

#### 组件

###### application
 > 组件由\<application\>\</application\>标签包裹  

application的属性：  

android:allowBackup  
表示是否允许APP加入到备份还原的结构中。如果设置成false，那么应用就不会备份还原。默认值为true。

android:fullBackupContent  
这个属性指向了一个xml文件，该文件中包含了在进行自动备份时的完全备份规则。这些规则定义了哪些文件需要备份。此属性是一个可选属性。默认情况下，自动备份包含了大部分app文件。

android:supportsRtl  
声明你的APP是否支持RTL（Right To Left）布局。如果设置成true，并且targetSdkVersion被设置成17或更高。很多RTL API会被集火，这样你的应用就可以显示RTL布局了。如果设置成false或者targetSdkVersion被设置成16或更低。哪些RTL API就不起作用了。
该属性的默认的值是false。

android:icon  
APP的图标，以及每个组件的默认图标。可以在组价中自定义图标。这个属性必须设置成一个引用，指向一个可绘制的资源，这个资源必须包含图片。系统不设置默认图标。例如mipmap/ic_launcher引用的就是下面的资源

android:label  
一个用户可读的标签，以及所有组件的默认标签。子组件可以用他们的label属性定义自己的标签，如果没有定义，那么就用这个标签。
标签必须设置成一个字符串资源的引用。这样它们就能和其他东西一样被定位，比如@string/app_name。当然，为了开发方便，你也可以定义一个原始字符串。

android:theme  
该属性定义了应用使用的主题的，它是一个指向style资源的引用。各个activity也可以用自己的theme属性设置自己的主题。

android:name  
Application子类的全名。包括前面的路径。例如com.sample.teapot.TeapotApplication。当应用启动时，这个类的实例被第一个创建。这个属性是可选的，大多数APP都不需要这个属性。在没有这个属性的时候，Android会启动一个Application类的实例。

对于在应用中创建的每个应用组件，您必须在清单文件中声明相应的 XML 元素：

注：  
<activity> 用于 Activity 的每个子类。  
<service> 用于 Service 的每个子类。  
<receiver> 用于 BroadcastReceiver 的每个子类。  
<provider> 用于 ContentProvider 的每个子类。  
如果您创建此类组件的任何子类，但未在清单文件中对其进行声明，则系统便无法启动该子类。  

###### activity
属性：  
android:name
指定注册的类名

android:label  
对属性的设置要求和<application>中一样。

注：入口activity需在activity标签内加入
```xml
<intent-filter>
	<action android:name="android.intent.action.MAIN" />

	<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

其他三个组件与activity配置类似。

#### 系统权限
<uses-permission/>标签用于申请权限   
🌰：<uses-permission android:name="android.permission.INTERNET"/>

