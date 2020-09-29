---
layout: 		post
title: 			"Android自定义控件"
subtitle: 		'多种形式的自定义控件'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## 形式
上一篇讲到自定义控件的三种形式以及流程，这里来具体讲解一下。
![](
https://a-photo-store.oss-cn-beijing.aliyuncs.com/in-posts/20200923costume_controller_1.png)

#### 继承自存在View的控件
圆形切割图片  
解决方案一：对canvas进行切割
```java
public class RoundImageView extends AppCompatImageView {
    int diam = 720;
    int padding = 10;
    int realSize = diam+padding;
    public RoundImageView(Context context) {
        this(context,null);
    }

    public RoundImageView(Context context, AttributeSet attrs) {
        this(context, attrs,0);
    }

    public RoundImageView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        init();
    }

    private void init() {

    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        int width = MeasureSpec.getSize(widthMeasureSpec);
        int widMode = MeasureSpec.getMode(widthMeasureSpec);
        int height = MeasureSpec.getSize(heightMeasureSpec);
        int heiMode = MeasureSpec.getMode(heightMeasureSpec);

        width = measureWidth(width,widMode);
        height = measureHeight(height,heiMode);
        setMeasuredDimension(width,height);
    }

    private int measureHeight(int height, int heiMode) {
        switch (heiMode){
            case MeasureSpec.AT_MOST:
                height = realSize>height?height:realSize;
                break;
            case MeasureSpec.UNSPECIFIED:
            case MeasureSpec.EXACTLY:
                break;
        }
        return height;
    }

    private int measureWidth(int width, int widMode) {
        switch (widMode){
            case MeasureSpec.AT_MOST:
                width = realSize>width?width:realSize;
                break;
            case MeasureSpec.UNSPECIFIED:
            case MeasureSpec.EXACTLY:
                break;
        }
        return width;
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        Path path = new Path();
        Paint paint = new Paint();
        paint.setStyle(Paint.Style.STROKE);
        paint.setColor(Color.BLUE);
        paint.setStrokeWidth(12);
        path.addOval(new RectF(10,10,diam,diam), Path.Direction.CW);

        Bitmap bitmap = BitmapFactory.decodeResource(getResources(),R.drawable.lxw,null);
        canvas.clipPath(path);
        canvas.drawBitmap(bitmap,diam/2-bitmap.getWidth()/2,diam/2-bitmap.getHeight()/2,paint);
    }
}
```

解决方案二：