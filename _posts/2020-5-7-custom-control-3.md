---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'属性动画'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## ValueAnimator
在Android中，动画分为两类：视图动画(View Animation)和属性动画(Property Animation)。其中视图动画包括补间动画与逐帧动画；属性动画中包括ValueAnimator和ObjectAnimator。

视图动画与属性动画的三点不同：
1. 引入时间不同：View Animation是在API Level 1引入的；而Property Animation是在API Level 11时引入的，即从Android3.0才有相关的API。
2. 包名不同：View Animation API在android.view.animation包中，而Property Animation API在android.animation包中。
3. 动画的命名不同，View Animation中的动画类都是XXXAnimation，而Property Animation中的动画类命名都是XXXAnimator。

区别：视图动画仅能对指定控件做动画，而属性动画是通过改变控件的某一属性来做动画的。

🌰：
给TextView附加平移的补间动画并加入单击弹出Toast的方法，动画结束后会发现，变换后的位置单击后没有反应，只有在原位置单击才有反应。

#### 简单使用
1）创建实例
```java
ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);
animator.start();
```

2）添加监听事件
```java
ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);

animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation) {
    	int curValue = (Integer)animation.getAnimatedValue();
        Log.i("xxxxx",curValue+"");
	}
});

animator.start();
```

从打印内容可以看到，ValueAnimator的功能是对指定区间进行动画运算，通过对运算过程的监听来自己操作控件，总结出来就两点：
- ValueAnimator只负责对指定值区间进行动画运算。
- 我们需要对运算过程进行监听，然后自己对控件执行动画操作。

使用案例：

```
final ImageView imageView = findViewById(R.id.smile);
Button button = findViewById(R.id.click);
final ValueAnimator animator = ValueAnimator.ofInt(0,400);
animator.setDuration(1000);

animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
	@Override
	public void onAnimationUpdate(ValueAnimator animation){
		int curValue = (Integer)animation.getAnimatedValue();
		imageView.layout(curValue,curValue,curValue+imageView.getWidth(),curValue+imageView.getHeight());
	}
});

imageView.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		Toast.makeText(MainActivity.this,"click",Toast.LENGTH_SHORT).show();
	}
});

button.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View v) {
		animator.start();
	}
});
```

这样变换位置原组件的点击事件是有效的。

#### 常见函数
1）offInt()与ofFloat()函数
```java
public static ValueAnimator ofInt(int... values)
public static ValueAnimator ofFloat(float... values)
```
他们的参数都是可变长参数，传进去的值就是动画的变化范围，比如ofInt(2,90,45)就表示从2变到90再变到45。

