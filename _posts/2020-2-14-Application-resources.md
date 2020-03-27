---
layout: 		post
title: 			"Android应用的资源"
subtitle: 		'图表造型的美化'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
> 新冠这么严重，情人节这种好日子也只能在家更新博客了

## 简介
&emsp;Android应用的源码大概可分为以下三大类：  
- 界面布局文件：XML文件，文件中每个标签都对应于相应的View标签  
- Java源文件：应用中的Activity、Service之类的代码文件  
- 资源文件：主要以各种XML文件为主，也包括*.png、*.jpg等图片资源  

&emsp;Android应用中，大多数的资源文件，如字符串资源、颜色资源、数组资源、菜单资源等都集中放在res目录中定义。还有一个assets目录，他的用途是存放应用无法直接访问的原生资源，需要通过AsserManager以二进制流的形式读取，而res目录下的资源，会由Android SDK编译时自动创建索引，能直接通过R资源清单类进行访问。  

## 概述
&emsp;按上面的说法，Android应用资源可分为两大类。
- assers目录：存放无法通过R资源清单类访问的原生资源。  
- res目录：存放可通过R资源清单类访问的资源。  

#### res目录
&emsp;Android不同资源，应存在/res/目录的不同文件夹下

<table border="1px" style="border-collapse: collapse;">
        <tr>
            <th>目录</th>
            <th>存放的资源</th>
        </tr>
        <tr>
            <td>/res/animator/</td>
            <td>存放定义属性动画的XML文件</td>
        </tr>
        <tr>
            <td>/res/anim/</td>
            <td>存放定义补间动画的XML文件</td>
        </tr>
        <tr>
            <td>/res/drawable/</td>
            <td>存放各种位图文件（如*.png、*.jpg）等，也可以是编译成如下各种Drawble对象的XML文件：
                <ul>
                    <li>BitmapDrawable对象</li>
                    <li>NinePatchDrawable对象</li>
                    <li>StateListDrawable对象</li>
					<li>ShapeDrawable对象</li>
                    <li>AnimationDrawable对象</li>
                    <li>Drawable的其他各种子类的对象</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>/res/color/</td>
            <td>存放定义不同状态下颜色列表的XML文件</td>
        </tr>
        <tr>
            <td>/res/layout/</td>
            <td>存放各种用户界面布局文件</td>
        </tr>
        <tr>
            <td>/res/menu/</td>
            <td>存放为应用程序定义各种菜单的资源，包括选项菜单、子菜单、上下文菜单资源</td>
        </tr>
        <tr>
            <td>/res/raw/</td>
            <td>存放任意类型的原生资源（比如音频文件、视频文件等）。在Java代码中可通过调用Resources对象的openRawResource(int id)方法来获取该资源的二进制输入流。也可以保存到/assets/目录下，然后在应用程序中使用AssetManager来访问这些资源</td>
        </tr>
        <tr>
            <td>/res/values/</td>
            <td>存放各种简单值的XML文件。这些简单值包括字符串值、整数值、颜色值、数组等  这些资源文件的根元素都是<resources/>,为根元素添加不同的子元素则代表不同的资源，例如：
                <ul>
                    <li>string/integer/bool子元素：代表添加一个字符串值、整数值或boolean值</li>
                    <li>color子元素：代表添加一个颜色值</li>
                    <li>array子元素或string-array、int-array子元素：代表添加一个数组</li>
                    <li>style子元素：代表添加一个样式</li>
                    <li>dimen：代表添加一个尺寸</li>
                </ul>
                为了区分清楚，Android建议用不同的文件存放，例如：
                <ul>
                    <li>arrays.xml：定义数组资源</li>
                    <li>colors.xml：定义颜色值资源</li>
                    <li>dimens.xml：定义尺寸值资源</li>
                    <li>strings.xml：定义字符串资源</li>
                    <li>styles.xml：定义样式资源</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>/res/xml/</td>
            <td>存放任意的原生XML文件。这些XML文件可以在JAVA代码中用Resources.getXML()方法进行访问</td>
        </tr>
    </table>

#### 使用资源
&emsp;由于Android SDL会在编译时在R类中为/res/目录下所有资源创建索引，因此在Java代码中访问资源主要通过R类来完成。其完整的语法格式为
	
	[<package_name>.]R.<resource_type>.<resource_name>

- <package_name>：R类所在的包，如果导入过R类所在的包，可以省略
- <resource_type>：R类中代表不同资源类型的子类，例如string代表字符串资源
- <resource_name>：指定资源名称，资源名称可能是无后缀的文件名（如图片资源），也可能是XML资源元素中由android:name属性知道的名称。

&emsp;在xml中使用资源格式如下：

	@[<package_name>：]<resource_type>/<resource_name>