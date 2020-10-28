---
layout: 		post
title: 			"Volley"
subtitle: 		'使用与源码解析'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## Volley
首先Volley的请求发送需要创建一个RequestQueue队列，创建它的方法一般用`Volley.newRequestQueue(Context)`

```java
public static RequestQueue newRequestQueue(Context context, int maxDiskCacheBytes) {
	return newRequestQueue(context, (HttpStack)null, maxDiskCacheBytes);
}

public static RequestQueue newRequestQueue(Context context, HttpStack stack) {
	return newRequestQueue(context, stack, -1);
}

public static RequestQueue newRequestQueue(Context context) {
	return newRequestQueue(context, (HttpStack)null);
}

public static RequestQueue newRequestQueue(Context context, HttpStack stack, int maxDiskCacheBytes) {
	File cacheDir = new File(context.getCacheDir(), "volley");
	String userAgent = "volley/0";

	try {
		String packageName = context.getPackageName();
		PackageInfo info = context.getPackageManager().getPackageInfo(packageName, 0);
		userAgent = packageName + "/" + info.versionCode;
	} catch (NameNotFoundException var7) {
	}

	if (stack == null) {
		if (VERSION.SDK_INT >= 9) {
			stack = new HurlStack();
		} else {
			stack = new HttpClientStack(AndroidHttpClient.newInstance(userAgent));
		}
	}

	Network network = new BasicNetwork((HttpStack)stack);
	RequestQueue queue;
	if (maxDiskCacheBytes <= -1) {
		queue = new RequestQueue(new DiskBasedCache(cacheDir), network);
	} else {
		queue = new RequestQueue(new DiskBasedCache(cacheDir, maxDiskCacheBytes), network);
	}

	queue.start();
	return queue;
}
```

可以看出从一开始的newRequestQueue(Context context)一直转到了newRequestQueue(Context context, HttpStack stack, int maxDiskCacheBytes)。    
在这个构造下，一开始就是对stack进行判断，没有就根据版本进行创建。接下来开始创建Network对象，将stack传入，然后对RequestQueue进行创建，开启队列并返回。 
总结来说，Volley就是RequestQueue的静态工厂。  

## RequestQueue
RequestQueue中维护了三个容器：  
两个PriorityBlockingQueue：mCacheQueue、mNetQueue  
和一个Set：mCurrentRequests  

- mCacheQueue：用于存放缓存带请求的Request
- mNetQueue：用于存放等待发起的Request
- mCurrentRequests：用于存放当前正在进行请求的Request


首先来看构造函数  
```java
public RequestQueue(Cache cache, Network network, int threadPoolSize, ResponseDelivery delivery) {
	this.mSequenceGenerator = new AtomicInteger();
	this.mWaitingRequests = new HashMap();
	this.mCurrentRequests = new HashSet();
	this.mCacheQueue = new PriorityBlockingQueue();
	this.mNetworkQueue = new PriorityBlockingQueue();
	this.mFinishedListeners = new ArrayList();
	this.mCache = cache;
	this.mNetwork = network;
	this.mDispatchers = new NetworkDispatcher[threadPoolSize];
	this.mDelivery = delivery;
}

public RequestQueue(Cache cache, Network network, int threadPoolSize) {
	this(cache, network, threadPoolSize, new ExecutorDelivery(new Handler(Looper.getMainLooper())));
}

public RequestQueue(Cache cache, Network network) {
	this(cache, network, 4);
}
```

主要顺序就是首先在入口构造中传递network和默认的线程数4，然后再第二个构造中创建了一个ExecutorDelivery并传入了一个主线程的Handler。

接下来是start方法  
```java
public void start() {
	this.stop();
	this.mCacheDispatcher = new CacheDispatcher(this.mCacheQueue, this.mNetworkQueue, this.mCache, this.mDelivery);
	this.mCacheDispatcher.start();

	for(int i = 0; i < this.mDispatchers.length; ++i) {
		NetworkDispatcher networkDispatcher = new NetworkDispatcher(this.mNetworkQueue, this.mNetwork, this.mCache, this.mDelivery);
		this.mDispatchers[i] = networkDispatcher;
		networkDispatcher.start();
	}

}
```
主要用途是启动该Queue中的Dispatcher。
1. 首先停止所有正在运行的Dispatcher。  
2. 创建 CacheDispatcher 并启动。
3.创建前面指定个数的 NetworkDispatcher（默认为 4 个）并启动。


#### 入队
我们通过RequestQueue的add方法将一个Request入队。
```java
public <T> Request<T> add(Request<T> request) {
	request.setRequestQueue(this);
	synchronized(this.mCurrentRequests) {
		this.mCurrentRequests.add(request);
	}

	request.setSequence(this.getSequenceNumber());
	request.addMarker("add-to-queue");
	if (!request.shouldCache()) {
		this.mNetworkQueue.add(request);
		return request;
	} else {
		synchronized(this.mWaitingRequests) {
			String cacheKey = request.getCacheKey();
			if (this.mWaitingRequests.containsKey(cacheKey)) {
				Queue<Request<?>> stagedRequests = (Queue)this.mWaitingRequests.get(cacheKey);
				if (stagedRequests == null) {
					stagedRequests = new LinkedList();
				}

			((Queue)stagedRequests).add(request);
			this.mWaitingRequests.put(cacheKey, stagedRequests);
				if (VolleyLog.DEBUG) {
					VolleyLog.v("Request for cacheKey=%s is in flight, putting on hold.", new Object[]{cacheKey});
				}
			} else {
				this.mWaitingRequests.put(cacheKey, (Object)	null);
				this.mCacheQueue.add(request);
			}

			return request;
		}
	}
}
```

首先请求会统一加入mCurrentRequests中，作为当前请求的记录，然后根据请求是否需要缓存分别加入mNetworkQueue或是mCacheQueue中。

