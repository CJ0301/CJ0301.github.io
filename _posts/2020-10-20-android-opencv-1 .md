---
layout: 		post
title: 			"OpenCV 1"
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
## Mat
Mat是OpenCV中用来存储图像信息的内存对象，可通过Imgcodecs.imread()方法从文件读入图像，或是用Utils.bitmapToMat()。  
Mat对象除了存储图像的像素数据外，还会存储图像具体宽、高、类型、维度、大小、深度等。可通过API获取这些数据。
 
#### 加载图像与读取基本信息
OpenCV中加载图像需要用Imgcodecs.imread()函数。   
此方法可以通过指定图像文件路径，也可以指定加载类型。  
默认是加载三通道顺序为BGR的彩色图像。

```java
public static Mat imread(String filename)
public static Mat imread(String filename, int flags)
```

加载类型参数有：
- IMREAD_UNCHANGED = -1，表示不改变加载图像类型
- IMREAD_GRAYSCALE = 0，表示加载图像为灰度图像
- IMREAD_COLOR = 1，表示加载图像为彩色图像

获取图像的宽、高、维度、通道数、深度、类型信息：
```java
Mat src = Imgcodecs.imread(fileUri.getPath());
int width = src.cols();
int height = src.rows();
int dims = src.dims();
int channels = src.channels();
int depth = src.depth();
int type = src.type();
```

通道数
图像深度
U 无符号整型
S 符号整型
F 浮点数
<table>
	<tr>
		<td>图像深度</td>
		<td>Java中对应的数据类型</td>
	</tr>
	<tr>
		<td>CV_8U=0</td>
		<td>8位byte</td>
	</tr>
	<tr>
		<td>CV_8S=1</td>
		<td>8位byte</td>
	</tr>
	<tr>
		<td>CV_16U=2</td>
		<td>16位char</td>
	</tr>
	<tr>
		<td>CV_16S=3</td>
		<td>16位char</td>
	</tr>
	<tr>
		<td>CV_32S=4</td>
		<td>32位整型int</td>
	</tr>
	<tr>
		<td>CV_32F=5</td>
		<td>32位float</td>
	</tr>
	<tr>
		<td>CV_64F=6</td>
		<td>64位double</td>
	</tr>
</table>

图像类型
<table>
	<tr>
		<td>单通道</td>
		<td>双通道</td>
		<td>三通道</td>
		<td>四通道</td>
	</tr>
	<tr>
		<td>CV_8UC1</td>
		<td>CV_8UC2</td>
		<td>CV_8UC3</td>
		<td>CV_8UC4</td>
	</tr>
	<tr>
		<td>CV_8SC1</td>
		<td>CV_8SC2</td>
		<td>CV_8SC3</td>
		<td>CV_8SC4</td>
	</tr>
	<tr>
		<td>CV_16UC1</td>
		<td>CV_16UC2</td>
		<td>CV_16UC3</td>
		<td>CV_16UC4</td>
	</tr>
	<tr>
		<td>CV_16SC1</td>
		<td>CV_16SC1</td>
		<td>CV_16SC1</td>
		<td>CV_16SC1</td>
	</tr>
	<tr>
		<td>CV_32SC1</td>
		<td>CV_32SC2</td>
		<td>CV_32SC3</td>
		<td>CV_32SC4</td>
	</tr>
	<tr>
		<td>CV_32FC1</td>
		<td>CV_32FC2</td>
		<td>CV_32FC3</td>
		<td>CV_32FC4</td>
	</tr>
	<tr>
		<td>CV_64FC1</td>
		<td>CV_64FC2</td>
		<td>CV_64FC3</td>
		<td>CV_64FC4</td>
	</tr>
</table>
调用imread函数时，如果只使用文件路径加载，那么默认值是三通道的CV_8UC3，图像深度为CV_8U，CV表示计算机视觉，8表示八位，UC表示无符号char，3表示三个通道。

#### Mat创建与初始化
1）通过create方法实现Mat对象的创建
```java
Mat m1 = new Mat();
m1.create(new Size(3,3),CvType.CV_8UC3);
Mat m2 = new Mat();
m2.create(3,3,CvType.CV_8UC3)
```

2）通过ones、eye、zeros方法创建
```java
Mat m3 = Mat.eye(3,3,CvType.CV_8UC3);
Mat m4 = Mat.eye(new Size(3,3),CvType.CV_8UC3);
Mat m5 = Mat.zeros(new Size(3,3),CvType.CV_8UC3);
Mat m6 = Mat.ones(new Size(3,3),CvType.CV_8UC3);
```

3）先定义，再通过setTo的方法实现初始化
```java
Mat m7 = new Mat(3,3,CvType.CV_8UC3);
m7.setTo(new Scalar(255,255,255));
```
与第一种类似，但第一种没指定颜色值。在OpenCV中，颜色向量通过Scalar表示，这里new Scalar(255,255,255)表示白色。

4）通过Mat的copyTo()与clone方法实现对象的创建，Mat中的克隆与拷贝方法会复制一份相同的Mat。
```java
Mat m8 = new Mat(500,500,CvType.CV_8UC3);
m8.setTo(new Scalar(127,127,127));
Mat result = new Mat();
m8.copyTo(result);
```

#### Mat对象保存
创建好的Mat图像可以通过imwrite函数将对象保存为图像。
```java
Mat m8 = new Mat(500,500,CvType.CV_8UC3);
m8.setTo(new Scalar(127,127,127));
ImageSelectUtils.saveImage(image);
```

保存部分代码
```java
File fileDir = new File(Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES),"myBook");
if(!fileDir.exists())
	fileDir.mkdirs();
String name = String.valueOf(System.currentTimeMillis()+"_book.jpg");
File tempFile = new File(fileDir.getAbsoluteFile()+File.separator,name);
Imgcodecs.imwrite(tempFile.getAbsolutePath(),image);
```

## Bitmap
加载
```java
Bitmap bitmap = BitmapFactory.decodeResource(this.getResources(),R.drawable.picture);
```

读写像素
Bitmap获取图像宽高配置
```java
public final int getWidth()
public final int getHeight()
public final int getConfig()
```

Config是枚举类型，具体类型如下：
- Bitmap.config.ALPHA_8：表示只有透明通道没有颜色通道，通常作为mask。
- Bitmap.config.ARGB_4444：表示每个通道占四位，总计两个字节，表示一个像素的图像。
- Bitmap.config.RGB_565：表示每个通道分别占5位、6位、5位，总计两个字节，表示一个像素的图像。
- Bitmap.config.ARGB_8888：表示每个通道占八位，总计四个字节，表示一个像素的图像(最常见)。

循环修改每个像素每个通道
```java
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture).copy(Bitmap.Config.ARGB_8888, true);
int height = bitmap.getHeight();
int width = bitmap.getWidth();
int a,r,g,b;
for(int row=0;row<height;row++){
	for(int col=0;col<width;col++){
		//读取像素
		int pixel = bitmap.getPixel(col,row);
		a = Color.alpha(pixel);
		r = Color.red(pixel);
		g = Color.green(pixel);
		b = Color.blue(pixel);

		//修改
		r = 255 - r;
		g = 255 - g;
		b = 255 - b;

		//保存
		bitmap.setPixel(col,row,Color.argb(a,r,g,b));

	}
}
```

```java
bitmap = BitmapFactory.decodeResource(MainActivity.this.getResources(),R.drawable.picture).copy(Bitmap.Config.ARGB_8888, true);
int height = bitmap.getHeight();
int width = bitmap.getWidth();
int[] pixels = new int[height*width];
bitmap.getPixels(pixels,0,width,0,0,width,height);
int a,r,g,b;
int index;
for(int row=0;row<height;row++){
	for(int col=0;col<width;col++){
		index = width*row+col;
		a = (pixels[index]>>24)&0xff;
		r = (pixels[index]>>16)&0xff;
		g = (pixels[index]>>8)&0xff;
		b = (pixels[index])&0xff;

		//修改像素
		r = 255 - r;
		g = 255 - g;
		b = 255 - b;

		//保存到bitmap
		pixels[index] = (a<<24)|(r<<16)|(g<<8)|b;
	}
}
```

第二种方法用的更多，先将像素存放在数组中，处理完之后再赋值给bitmap，注意Bitmap有immutable的问题，之后会详细分析。

#### 释放内存
Bitmap需要调用`bitmap.recycle();`释放内存  
Mat需要调用`mat.release()`来释放内存  

