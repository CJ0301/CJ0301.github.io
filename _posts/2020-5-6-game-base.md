---
layout: 		post
title: 			"游戏基础篇(C语言实现)"
subtitle: 		'随便写写'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Game
---
## 概述
这个专题的更新只是出于兴趣，更新频率应该会比较慢吧。

## 会动的小球
首先游戏的基础肯定是定位打印啦，最简单的例如弹球游戏，首先肯定是要有一个弹球。二维空间中，弹球的定位依赖与x轴和y轴。依此我们可以成功打印出一个小球。
```c
int x = 3, y = 4;
for (int i = 0;i < x;i++)
	printf("\n");

for (int j = 0;j < y;j++)
	printf(" ");

printf("o\n");
system("pause");
```

![](https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/2020-05-06-print-ball.png)

光有个球还不够，我们当然是要让他动起来。这时我们就需要用到一个速度v。

```c
int x=3, y=4;
int v = 1;
while (1) {
	x += v;
	system("cls");
	for (int i = 0;i < x;i++) 
		printf("\n");
		
	for (int j = 0;j < y;j++) 
		printf(" ");
		
	printf("o\n");
}
system("pause");
```

然后我们发现这个球只会不断下坠，下面我们给他增加一些弹性。

```c
if (x > 10 || x < 1)
	v *= -1;
```

上面这段代码在到达边界之后会改变方向。

当然上下弹也没啥意思，我们再给他一个y方向的速度。
```
int x=3, y=4;
int vx = 1,vy=2;
while (1) {
	if (x > 10 || x < 1)
		vx *= -1;

	if (y > 10 || y < 1)
		vy *= -1;

	x += vx;
	y += vy;

	system("cls");
	for (int i = 0;i < x;i++) 
		printf("\n");
		
	for (int j = 0;j < y;j++) 
		printf(" ");
		
	printf("o\n");
}
system("pause");
```

光看他弹也没有意思，不如控制它到处跑。
```c
int x=3, y=4;
char input;
while (1) {
	system("cls");
	for (int i = 0;i < x;i++) 
		printf("\n");
		
	for (int j = 0;j < y;j++) 
		printf(" ");
		
	printf("o\n");
	input = _getch();
	if (input == 's') 
		x++;
	
	if (input == 'w') 
		x--;
		
	if (input == 'd') 
		y++;
		
	if (input == 'a') 
		y--;
		
}
system("pause");
```

注意：老版本用的是getch()，比较新的版本改成了_getch()。

## 飞机大战
这里我们写一个会射击的大飞机。
```c
int x=3, y=4;
char input;
int isFire = 0;

while (1) {
	system("cls");

	if (!isFire) {
		for (int i = 0;i < x;i++)
			printf("\n");
	}
	else {
		for (int i = 0;i < x;i++) {
			for (int j = 0;j < y;j++) 
				printf(" ");
			printf("|\n");
		}
		isFire = 0;
	}

		
	for (int j = 0;j < y;j++) 
		printf(" ");
	printf("0\n");

	for (int j = 0;j < y-2;j++)
		printf(" ");
	printf("00000\n");

	for (int j = 0;j < y-1;j++)
		printf(" ");
	printf("0 0\n");

	input = _getch();
	if (input == 's') 
		x++;
	
	if (input == 'w') 
		x--;
		
	if (input == 'd') 
		y++;
	
	if (input == 'a') 
		y--;
		
	if (input == ' ') 
		isFire=1;
	
}
system("pause");
```

#### 游戏模块化
虽然上面的代码比较短，但是实际上看起来还是很杂乱，功能全部在主函数里，这时候就需要用到模块化的思想。

合理的游戏框架
```
int main(){
	startup();//数据初始化
	while (1) {//游戏循环执行
		show();//显示画面
		updateWithoutInput();//与输入用户无关的更新
		updateWithInput();//与输入用户有关的更新
	}
	return 0;
}
```