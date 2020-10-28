---
layout: 		post
title: 			"OpenCV 2"
subtitle: 		'Mat与Bitmap'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## 像素读写
Mat是图像的容器，获取数据时会根据类型与通道数目，开辟适当大小的内存空间。  
像素的读写主要通过get与put方法进行操作。
<table>
	<tr>
		<td>方法</td>
		<td>支持类型</td>
	</tr>
	<tr>
		<td>double[] get(int row,int col)</td>
		<td>全部</td>
	</tr>
	<tr>
		<td>int get(int row,int col,double[] data)</td>
		<td>CV_64FC1~CV64FC4</td>
	</tr>
	<tr>
		<td>int get(int row,int col,float[] data)</td>
		<td>CV_32FC1~CV32FC4</td>
	</tr>
	<tr>
		<td>int get(int row,int col,int[] data)</td>
		<td>CV_32SC1~CV_32SC4</td>
	</tr>
	<tr>
		<td>int get(int row,int col,short[] data)</td>
		<td>CV_16SC1~CV_16SC4</td>
	</tr>
	<tr>
		<td>int get(int row,int col,byte[] data)</td>
		<td>CV_8UC1~CV_8UC4</td>
	</tr>
</table>

循环读取Mat像素点数据(CV_8UC3)
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}
int channels = src.channels();
int width = src.cols();
int height = src.rows();
byte[] data = new byte[channels];
int b,g,r;
for(int row = 0;row<height;row++){
	for(int col = 0;col<width;col++){
		//读取
		src.get(row,col,data);
		b = data[0]&0xff;
		g = data[1]&0xff;
		r = data[2]&0xff;

		//修改
		b = 255 - b;
		g = 255 - g;
		r = 255 - r;

		//写入
		data[0] = (byte)b;
		data[1] = (byte)g;
		data[2] = (byte)r;
		src.put(row,col,data);
	}
	Log.i("载入行",row+"-------");
	Utils.matToBitmap(src,bitmap);
	Message message = handler.obtainMessage();
	message.what = 1;
	handler.sendMessage(message);
}
```

每次读取一行像素数据
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}
int channels = src.channels();
int width = src.cols();
int height = src.rows();
byte[] data = new byte[channels*width];
int pv;
for(int row = 0;row<height;row++){
	src.get(row,0,data);
	for(int col=0;col<data.length;col++){
		//读取
		pv = data[col]&0xff;

		//修改
		pv = 255 - pv;
		data[col] = (byte)pv;
}
src.put(row,0,data);
Log.i("载入行",row+"-------");
Utils.matToBitmap(src,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

读取全部像素数据
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}
int channels = src.channels();
int width = src.cols();
int height = src.rows();
byte[] data = new byte[channels*width*height];
int pv;
src.get(0,0,data);
for(int i=0;i<data.length;i++){
	pv = data[i]&0xff;
	pv = 255 - pv;
	data[i] = (byte)pv;
}
src.put(0,0,data);
Utils.matToBitmap(src,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

## 图像通道与均值方差
#### 图像通道的分离与合并
分离与合并需要用到split与merge方法
```java
//m表示多通道图像，mv表示分离后的多个单通道图像
split(Mat,List<Mat> mv)

//mv表示多个待合并的单通道图像，dst表示合并后的多通道图像
merge(List<Mat> mv,Mat dst)
```

🌰:
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}
List<Mat> mv = new ArrayList<>();
Core.split(src,mv);
for(Mat m:mv){
	int pv;
	int channels = m.channels();
	int width = m.cols();
	int height = m.height();
	byte[] data = new byte[channels*width*height];
	m.get(0,0,data);
	for(int i=0;i<data.length;i++){
		pv = data[i]&0xff;
		pv = 255 - pv;
		data[i] = (byte)pv;
	}
	m.put(0,0,data);
}
Core.merge(mv,src);
Log.i("转换","-------");
Utils.matToBitmap(src,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

#### 均值方差的计算与应用
```java
//src表示输入的Mat
//mean表示各个通道的均值，数组长度与通道数一致
//stddev表示计算处各个通道的标准方差，数组长度与通道树木一致
meanStdDev(Mat src,MatOfDouble mean,MatOfDouble stddev)

//mask表示只有当mask中对应位置的像素值不为零，src相同位置的像素点才参与计算均值与标准方差
meanStdDev(Mat src,MatOfDouble mean,MatOfDouble stddev,Mat mask)
```

基于均值的二值分割
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}
//转为灰度图像
Mat gray = new Mat();
Imgproc.cvtColor(src,gray,Imgproc.COLOR_BGRA2GRAY);

//计算均值与标准方差
MatOfDouble means = new MatOfDouble();
MatOfDouble stddevs = new MatOfDouble();
Core.meanStdDev(gray,means,stddevs);

//显示均值与标准方差
double[] mean = means.toArray();
double[] stdDev = stddevs.toArray();
Log.i("MainActivity------","gray image means:"+mean[0]);
Log.i("MainActivity------","gray image stddev:"+stdDev[0]);

//读取像素数组
int width = gray.cols();
int height = gray.height();
byte[] data = new byte[width*height];
gray.get(0,0,data);
int pv = 0;

//根据均值进行二值分割
int t = (int)mean[0];
for(int i=0;i<data.length;i++){
	pv = data[i] & 0xff;
	if(pv>t){
		data[i] = (byte)255;
	}else{
		data[i] = (byte)0;
	}
}
gray.put(0,0,data);
	
Utils.matToBitmap(gray,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

#### 算术操作与调整图像的亮度与对比度
算数操作可以在两个Mat对象中进行，也可以在Mat对象与Scalar对象之间进行。
```java
//src1表示输入图像1，src2表示输入图像2，dst表示输出图像
add(Mat src1,Mat src2,Mat dst)
subtract(Mat src1,Mat src2,Mat dst)
multiply(Mat src1,Mat src2,Mat dst)
divide(Mat src1,Mat src2,Mat dst)
```
src2的类型还可以是Scalar类型，这时表示图像的每个像素点都与Scalar中的每个向量完成指定的算数操作。

两个Mat对象叠加结果输出：
```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);

//图像1
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}

//图像2
Mat moon = Mat.zeros(src.rows(),src.cols(),src.type());
int cx = src.cols() - 600;
int cy = 600;
Imgproc.circle(moon,new Point(cx,cy),300,new Scalar(90,95,234),-1,8,0);

//加法运算
Mat dst = new Mat();
Core.add(src,moon,dst);

Utils.matToBitmap(dst,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

#### 基于权重的图像叠加
```
//src1表示输入的第一个Mat对象
//alpha表示混合时第一个Mat对象所占权重大小
//src2表示输入的第二个Mat对象
//beta表示混合时第二个Mat对象所占权重大小
//gamma表示混合之后是否进行亮度校正(提升或降低)
//dst表示输出权重叠加后的Mat图像
addWeighted(Mat src1,double alpha,Mat src2,double beta,double gamma,Mat dst)
```

权重调整的满足条件为alpha+beta=1.0，假设src2为黑色背景，beta为正值，则对比度降低；若beta为负值，则画面对比度提升。如果gamma为正整数，则画面亮度变亮。
dst = src1*alpha+src2*beta+gamma

```java
Log.i("加载开始","-------");
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture);

//图像1
Mat src = new Mat();
Utils.bitmapToMat(bitmap,src);
if(src.empty()){
	return;
}

double alpha = 0.5;

//黑色背景
Mat black = Mat.zeros(src.size(),src.type());
Mat dst = new Mat();

//像素混合(基于权重)
Core.addWeighted(src,alpha,black,1.0-alpha,20,dst);

Utils.matToBitmap(dst,bitmap);
Message message = handler.obtainMessage();
message.what = 1;
handler.sendMessage(message);
```

