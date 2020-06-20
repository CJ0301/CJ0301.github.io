---
layout: 		post
title: 			"Android WebView"
subtitle: 		'最近遇到webview的需求了，更新一波'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
> WebView是一个基于webkit引擎、展现web页面的控件。


## 使用
载入
```java
//方式1. 加载一个网页：
webView.loadUrl("http://www.google.com/");

//方式2：加载apk包中的html页面
webView.loadUrl("file:///android_asset/test.html");

//方式3：加载手机本地的html页面
webView.loadUrl("content://com.android.htmlfileprovider/sdcard/test.html");

// 方式4： 加载 HTML 页面的一小段内容
WebView.loadData(String data, String mimeType, String encoding);
// 参数说明：
// 参数1：需要截取展示的内容
// 内容里不能出现 ’#’, ‘%’, ‘\’ , ‘?’ 这四个字符，若出现了需用 %23, %25, %27, %3f 对应来替代，否则会出现异常
// 参数2：展示内容的类型
// 参数3：字节码
```

状态
```java
//激活WebView为活跃状态，能正常执行网页的响应
webView.onResume();

//当页面被失去焦点被切换到后台不可见状态，需要执行onPause
//通过onPause动作通知内核暂停所有的动作，比如DOM的解析、plugin的执行、JavaScript执行。
webView.onPause();

//当应用程序(存在webview)被切换到后台时，这个方法不仅仅针对当前的webview而是全局的全应用程序的webview
//它会暂停所有webview的layout，parsing，javascripttimer。降低CPU功耗。
webView.pauseTimers();
//恢复pauseTimers状态
webView.resumeTimers();

//销毁Webview
//在关闭了Activity时，如果Webview的音乐或视频，还在播放。就必须销毁Webview
//但是注意：webview调用destory时,webview仍绑定在Activity上
//这是由于自定义webview构建时传入了该Activity的context对象
//因此需要先从父容器中移除webview,然后再销毁webview:
rootLayout.removeView(webView); 
webView.destroy();
```

前进后退
```java
//是否可以后退
Webview.canGoBack();
//后退网页
Webview.goBack();

//是否可以前进                     
Webview.canGoForward();
//前进网页
Webview.goForward();

//以当前的index为起始点前进或者后退到历史记录中指定的steps
//如果steps为负数则为后退，正数则为前进
Webview.goBackOrForward(intsteps);
```

将Back键改为网页后退  
```java
public boolean onKeyDown(int keyCode, KeyEvent event) {
    if ((keyCode == KEYCODE_BACK) && mWebView.canGoBack()) { 
        mWebView.goBack();
        return true;
    }
    return super.onKeyDown(keyCode, event);
}
```

清除缓存
```java
//清除网页访问留下的缓存
//由于内核缓存是全局的因此这个方法不仅仅针对webview而是针对整个应用程序.
Webview.clearCache(true);

//清除当前webview访问的历史记录
//只会webview访问历史记录里的所有记录除了当前访问记录
Webview.clearHistory();

//这个api仅仅清除自动完成填充的表单数据，并不会清除WebView存储到本地的数据
Webview.clearFormData();
```

## 常用工具类
#### WebSrtting类
1.添加网络权限
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

2.生成WebView组件
```java
//方式1：直接在在Activity中生成
WebView webView = new WebView(this);

//方法2：在Activity的layout文件里添加webview控件：
WebView webview = (WebView) findViewById(R.id.webView1);
```

3.配置并利用WebSetting子类
```java
//声明WebSettings子类
WebSettings webSettings = webView.getSettings();

//如果访问的页面中要与Javascript交互，则webview必须设置支持Javascript
webSettings.setJavaScriptEnabled(true);  
// 若加载的 html 里有JS 在执行动画等操作，会造成资源浪费（CPU、电量）
// 在 onStop 和 onResume 里分别把 setJavaScriptEnabled() 给设置成 false 和 true 即可

//支持插件
webSettings.setPluginsEnabled(true); 

//设置自适应屏幕，两者合用
webSettings.setUseWideViewPort(true); //将图片调整到适合webview的大小 
webSettings.setLoadWithOverviewMode(true); // 缩放至屏幕的大小

//缩放操作
webSettings.setSupportZoom(true); //支持缩放，默认为true。是下面那个的前提。
webSettings.setBuiltInZoomControls(true); //设置内置的缩放控件。若为false，则该WebView不可缩放
webSettings.setDisplayZoomControls(false); //隐藏原生的缩放控件

//其他细节操作
webSettings.setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK); //关闭webview中缓存 
webSettings.setAllowFileAccess(true); //设置可以访问文件 
webSettings.setJavaScriptCanOpenWindowsAutomatically(true); //支持通过JS打开新窗口 
webSettings.setLoadsImagesAutomatically(true); //支持自动加载图片
webSettings.setDefaultTextEncodingName("utf-8");//设置编码格式
```

常见用法：  
当加载 html 页面时，WebView会在/data/data/包名目录下生成 database 与 cache 两个文件夹，请求的 URL记录保存在WebViewCache.db，而 URL的内容是保存在 WebViewCache 文件夹下。

是否启用缓存
```java
//优先使用缓存: 
WebView.getSettings().setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK); 
//缓存模式如下：
//LOAD_CACHE_ONLY: 不使用网络，只读取本地缓存数据
//LOAD_DEFAULT: （默认）根据cache-control决定是否从网络上取数据。
//LOAD_NO_CACHE: 不使用缓存，只从网络获取数据.
//LOAD_CACHE_ELSE_NETWORK，只要本地有，无论是否过期，或者no-cache，都使用缓存中的数据。

//不使用缓存: 
WebView.getSettings().setCacheMode(WebSettings.LOAD_NO_CACHE);
```

结合使用（离线加载）
```java
if (NetStatusUtil.isConnected(getApplicationContext())) {
    webSettings.setCacheMode(WebSettings.LOAD_DEFAULT);//根据cache-control决定是否从网络上取数据。
} else {
    webSettings.setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);//没网，则从本地获取，即离线加载
}

webSettings.setDomStorageEnabled(true); // 开启 DOM storage API 功能
webSettings.setDatabaseEnabled(true);   //开启 database storage API 功能
webSettings.setAppCacheEnabled(true);//开启 Application Caches 功能

String cacheDirPath = getFilesDir().getAbsolutePath() + APP_CACAHE_DIRNAME;
webSettings.setAppCachePath(cacheDirPath); //设置  Application Caches 缓存目录
```

#### WebViewClient类
处理通知与请求事件

1.shouldOverrideUrlLoading()  
打开网页时不调用系统浏览器，而是在本WebView中显示，网页上所有加载都经过这个方法。
```java
//步骤1. 定义Webview组件
Webview webview = (WebView) findViewById(R.id.webView1);

//步骤2. 选择加载方式
//方式1. 加载一个网页：
webView.loadUrl("http://www.google.com/");

//方式2：加载apk包中的html页面
webView.loadUrl("file:///android_asset/test.html");

//方式3：加载手机本地的html页面
webView.loadUrl("content://com.android.htmlfileprovider/sdcard/test.html");

//步骤3. 复写shouldOverrideUrlLoading()方法，使得打开网页时不调用系统浏览器， 而是在本WebView中显示
webView.setWebViewClient(new WebViewClient(){
	@Override
	public boolean shouldOverrideUrlLoading(WebView view, String url) {
		view.loadUrl(url);
		return true;
	}
});
```

2.onPageStarted()
载入页面调用时，可设定一个loading的页面。
```java
webView.setWebViewClient(new WebViewClient(){
	@Override
	public void  onPageStarted(WebView view, String url, Bitmap favicon) {
		//设定加载开始的操作
	}
});
```

3.onPageFinished()
在页面加载结束时调用。关闭loading条，切换程序动作。
```java
webView.setWebViewClient(new WebViewClient(){
	@Override
	public void onPageFinished(WebView view, String url) {
		//设定加载结束的操作
	}
});
```

4.onLoadResource()
在加载页面资源时会调用，每一个资源（比如图片）的加载都会调用一次。
```java
webView.setWebViewClient(new WebViewClient(){
	@Override
	public boolean onLoadResource(WebView view, String url) {
		//设定加载资源的操作
	}
});
```

5.onReceivedError()
加载页面的服务器出现错误时（如404）调用。
加载本地404页面
```java
//步骤1：写一个html文件（error_handle.html），用于出错时展示给用户看的提示页面
//步骤2：将该html文件放置到代码根目录的assets文件夹下

//步骤3：复写WebViewClient的onRecievedError方法
//该方法传回了错误码，根据错误类型可以进行不同的错误分类处理
webView.setWebViewClient(new WebViewClient(){
	@Override
	public void onReceivedError(WebView view, int errorCode, String description, String failingUrl){
		switch(errorCode){
			case HttpStatus.SC_NOT_FOUND:
				view.loadUrl("file:///android_assets/error_handle.html");
				break;
		}
	}
});
```

6.onReceivedSslError()
处理https请求  
webView默认是不处理https请求的，页面显示空白，需要进行如下设置：
```java
webView.setWebViewClient(new WebViewClient() {    
	@Override    
	public void onReceivedSslError(WebView view, SslErrorHandler handler, SslError error) {    
		handler.proceed();    //表示等待证书响应
        // handler.cancel();      //表示挂起连接，为默认方式
        // handler.handleMessage(null);    //可做其他处理
	}    
});  

// 特别注意：5.1以上默认禁止了https和http混用，以下方式是开启
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) 
	mWebView.getSettings().setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW);

```

## 与js的交互
在WebView的JavaScript中调用Android方法只要如下三个步骤。
1. 调用WebView关联的WebSetting的setJavaScriptEnable(true)启用JavaScript调用功能。
2. 调用WebView的addJavascriptInterface(Object object,String name)方法将object对象暴露给JavaScript脚本。
3. 在JavaScript脚本中通过刚才暴露的name对象调用Android方法。

MainActivity
```java
WebView mWebView = findViewById(R.id.webView);

WebSettings webSettings = mWebView.getSettings();
// 设置与Js交互的权限
webSettings.setJavaScriptEnabled(true);
// 设置允许JS弹窗
        webSettings.setJavaScriptCanOpenWindowsAutomatically(true);
// 格式规定为:file:///android_asset/文件名.html
mWebView.loadUrl("file:///android_asset/AndroidWeb/Test.html");
//将MyObject对象暴露给JS脚本
mWebView.addJavascriptInterface(new MyObject(this),"mObj");
```

MyObject
```java
public class MyObject {
    Context mContext;

    public MyObject(Context mContext) {
        this.mContext = mContext;
    }

    @JavascriptInterface
    public void showToast(String word){
        Toast.makeText(mContext,word,Toast.LENGTH_SHORT).show();
    }
}
```

Test.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style type="text/css">
        html, body {
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        img{
            margin: 0 auto;
        }
    </style>

</head>
<body>
    <img id="img" src="tag.png">
    <script>
        var img = document.getElementById("img");
        img.onclick = function(){
            mObj.showToast("积分+100")
        };
    </script>
</body>
</html>
```