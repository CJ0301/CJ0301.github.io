---
layout: 		post
title: 			"OpenCV 0"
subtitle: 		'环境安装'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## 环境
依赖包去[官网](https://opencv.org/releases/)下就好了

#### 导入依赖
选择Import Module，选择解压缩好的目录中的sdk\java。  

把native\libs下面所有文件与文件夹复制到libs中，删除所有以*.a后缀的文件。

openCVLibrary模块和项目的sdkVersion要保持一致(调成Android模式可看到两个build.gradle)。

在项目的build.gradle脚本中添加：
```
task nativeLibsToJar(type: Jar,description:'create a jar archive of the native libs'){
    destinationDir file("$buildDir/native-libs")
    baseName 'native-libs'
    from fileTree(dir: 'libs',include:  '**/*.so')
    into 'lib/'
}

tasks.withType(JavaCompile){
    compileTask -> compileTask.dependsOn(nativeLibsToJar)
}
```

在编译片段添加：
```
implementation fileTree(dir: "$buildDir/native-libs",include: 'native-libs.jar')
```

测试范例：灰度值调整

activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/picture"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="9"
        android:src="@drawable/picture"/>
    <Button
        android:id="@+id/change"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:text="灰度"/>

</LinearLayout>
```

MainActivity.java
```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    private final String CV_TAG = "OpenCV------------";
    private ImageView mPicture;
    private Button mChange;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initLoadOpenCV();
        initView();

    }

    private void initView() {
        mPicture = (ImageView) findViewById(R.id.picture);
        mChange = (Button) findViewById(R.id.change);
        mChange.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.change:
                Bitmap bitmap = BitmapFactory.decodeResource(this.getResources(),R.drawable.picture);
                Mat src = new Mat();
                Mat dst = new Mat();
                Utils.bitmapToMat(bitmap,src);
                Imgproc.cvtColor(src,dst,Imgproc.COLOR_BGRA2GRAY);
                Utils.matToBitmap(dst,bitmap);
                mPicture.setImageBitmap(bitmap);
                src.release();
                dst.release();
                break;
        }
    }

	//加载本地库
    private void initLoadOpenCV(){
        boolean success = OpenCVLoader.initDebug();
        if(success){
            Log.i(CV_TAG,"OpenCV Libraries loaded...");
        }else{
            Toast.makeText(MainActivity.this,"Warning:Could not load OpenCV Libraries",Toast.LENGTH_SHORT).show();
        }
    }


}
```

## 拍照与图像获取
调用Android拍照功能，并返回图像
```java

```