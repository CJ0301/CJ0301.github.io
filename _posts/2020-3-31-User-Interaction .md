---
layout: 		post
title: 			"用户基础交互"
subtitle: 		'一些基础交互的整理'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - Android
---
## Menu
Menu一共有三类：  
1.选项菜单OptionMenu:如果style为NoActionBar则不显示。  
2.上下文菜单ContextMenu:为组件提供长按弹出菜单的功能。  
3.子菜单SubMenu:为以上两个菜单加入子菜单。  

加入菜单项的方法：  
1.直接add()。  
2.使用menu资源文件。  

menu资源文件：  
1.menu资源文件需要放在\res\menu\下，没有就自己创一个。  
2.有<menu><item><group>三个标签：  
- \<menu\>:根节点  
- \<group\>:菜单项分组  
- \<item\>:菜单项  

item:  
id:表示菜单项的id。  
orderInCategory：设置整数的优先级。  
showAsAction：never显示三个点，always显示标题，ifRoom有位置就显示标题，没位置就三个点。

3.getMenuInflater().inflate(R.menu.menu_1,menu);

MainActivity.java
```java
package com.fb.menus;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.ContextMenu;
import android.view.Menu;
import android.view.MenuItem;
import android.view.SubMenu;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        TextView longPress = findViewById(R.id.longPress);

        //设置成单击
        longPress.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                openContextMenu(view);
            }
        });

        //注册
        registerForContextMenu(longPress);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {

        /* menu.add
        *
        * 选项组号(一般填0)
        * 选项ID
        * 顺序(一般填0)
        * 选项标题名
        * */
        menu.add(0,1,0,"Choice1");
        menu.add(0,2,0,"Choice2");
        menu.add(0,3,0,"Choice3");
        menu.add(0,4,0,"Choice4");
        menu.add(0,5,0,"Choice5");
        menu.add(0,6,0,"Choice6");
        SubMenu subMenu1 = menu.addSubMenu("SubMenu1");//也可以像这样只指定标题名称
        subMenu1.add(0,7,0,"subChoice1");
        subMenu1.add(0,8,0,"subChoice2");
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        String title = item.toString();
        makeToast(title);

//        switch (item.getItemId()){
//            case 1:
//
//        }

        return true;
    }

    @Override
    public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
        super.onCreateContextMenu(menu, v, menuInfo);
//        menu.add(0,1,0,"Choice1");
//        menu.add(0,2,0,"Choice2");
//        menu.add(0,3,0,"Choice3");
//        SubMenu subMenu1 = menu.addSubMenu("SubMenu1");//也可以像这样只指定标题名称
//        subMenu1.add(0,7,0,"subChoice1");
//        subMenu1.add(0,8,0,"subChoice2");
        getMenuInflater().inflate(R.menu.menu_1,menu);
    }

    @Override
    public boolean onContextItemSelected(MenuItem item) {
        makeToast(item.getTitle().toString());
        return true;
    }

    public void makeToast(String option){
        Toast.makeText(this,option+"is selected",Toast.LENGTH_SHORT).show();
    }
}

```

activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/longPress"
        android:background="#cccccc"
        android:textSize="30sp"
        android:padding="20sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="LONG PRESS ME!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

menu_1.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:id="@+id/choice1" android:title="Item1"/>
    <item android:id="@+id/choice2" android:title="Item2"/>
    <item android:id="@+id/choice3" android:title="Item3"/>
    <item android:id="@+id/choice4" android:title="Item4"/>
</menu>
```

## Toast
Toast用于给用户显示一些提示。  
默认样式
```java
Toast.makeText(this,"默认样式",Toast.LENGTH_SHORT).show();
```

设置位置

```java
Toast toast = Toast.makeText(this,"在中间",Toast.LENGTH_SHORT);
toast.setGravity(Gravity.CENTER,0,0);
toast.show();
```

加图片

```java
Toast toast = Toast.makeText(this,"加图片",Toast.LENGTH_SHORT);
toast.setGravity(Gravity.CENTER,0,0);
LinearLayout toastView = (LinearLayout) toast.getView();
ImageView imageCodeProject = new ImageView(getApplicationContext());
imageCodeProject.setImageResource(R.drawable.ic_launcher_background);
toastView.addView(imageCodeProject, 0);
toast.show();
```

自定义视图

```java
 Toast toast = Toast.makeText(this,"",Toast.LENGTH_SHORT);
View view = LayoutInflater.from(this).inflate(R.layout.toast_layout,null);
TextView title = view.findViewById(R.id.title);
title.setText("通知");
toast.setView(view);
toast.setGravity(Gravity.CENTER,0,0);
toast.show();
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="TextView" />

    <ImageView
        android:id="@+id/image"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:src="@mipmap/ic_launcher"/>
</LinearLayout>
```

## 弹窗实现
与Toast不同，Dialog是出现在当前Activity上的一个窗口，会使下方的Activity失去焦点。 

Dialog有两种类型：  
1.AlterDialog:可显示标题、提示信息、按钮、可选项列表或自定义布局等。  
2.DatePickerDialog 或 TimePickerDialog：带有允许用户选择日期或时间的预定义UI。

这些类定义了对话框的样式与结构，开发者应该使用DialogFragment(Android3.0引入，3.0以下得使用support提供的DialogFragment)作为对话框的容器。优势在于它能正确正确处理生命周期时间(例如屏幕方向变化导致的Activity重建)，同时能重复利用。

#### Dialog
AlterDialog  
1.最简易的两个选项  
```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("Make a choice");
	builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose yes",Toast.LENGTH_SHORT).show();
		}
	});
	builder.setNegativeButton("No", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose no",Toast.LENGTH_SHORT).show();
		}
	});

	builder.create().show();
}
```

2.三个选项带列表项  
```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("Make a choice");
	final String[] str = {"item1","item2","item3"};
	// 设置了列表就不能设置内容了，否则就会出问题
	builder.setItems(str, new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialog, int which) {
			Toast.makeText(MainActivity.this,"You choose"+str[which],Toast.LENGTH_SHORT).show();
		}
	}).setPositiveButton("Yes", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose yes",Toast.LENGTH_SHORT).show();
		}
	}).setNegativeButton("No", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
 			Toast.makeText(MainActivity.this,"You choose no",Toast.LENGTH_SHORT).show();
		}
	}).setNeutralButton("Neutral", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
 			Toast.makeText(MainActivity.this,"You choose neutral",Toast.LENGTH_SHORT).show();
		}
	});

	builder.create().show();
```

3.单选列表项
```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("Make a choice");
	final String[] str = {"item1","item2","item3"};
	// 设置了列表就不能设置内容了，否则就会出问题
	builder.setSingleChoiceItems(str, 1,new DialogInterface.OnClickListener() {
		@Override
        public void onClick(DialogInterface dialog, int which) {
        	Toast.makeText(MainActivity.this,"You choose"+str[which],Toast.LENGTH_SHORT).show();
        }
	}).setPositiveButton("Yes", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose yes",Toast.LENGTH_SHORT).show();
		}
	}).setNegativeButton("No", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose no",Toast.LENGTH_SHORT).show();
		}
	}).setNeutralButton("Neutral", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose neutral",Toast.LENGTH_SHORT).show();
		}
	});

	builder.create().show();
}
```

4.多选列表项
```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("Make a choice");
	final String[] str = {"item1","item2","item3"};
	// 设置了列表就不能设置内容了，否则就会出问题
	builder.setMultiChoiceItems(str, new boolean[]{true, false, false}, new DialogInterface.OnMultiChoiceClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i, boolean b) {
			Toast.makeText(MainActivity.this,"You change"+str[i],Toast.LENGTH_SHORT).show();
		}
	}).setPositiveButton("Yes", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose yes",Toast.LENGTH_SHORT).show();
		}
	}).setNegativeButton("No", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose no",Toast.LENGTH_SHORT).show();
		}
	}).setNeutralButton("Neutral", new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose neutral",Toast.LENGTH_SHORT).show();
		}
	});

	builder.create().show();
}
```

5.适配器
```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	builder.setTitle("Make a choice");
	final String[] str = {"item1","item2","item3"};
	builder.setAdapter(new ArrayAdapter(this, android.R.layout.simple_list_item_activated_1, str), new DialogInterface.OnClickListener() {
		@Override
		public void onClick(DialogInterface dialogInterface, int i) {
			Toast.makeText(MainActivity.this,"You choose"+str[i],Toast.LENGTH_SHORT).show();
		}
	});
	builder.create().show();
}
```

6.自定义布局  


```java
public void makeDialog(){
	AlertDialog.Builder builder = new AlertDialog.Builder(this);
	//将布局文件实例化
	View view = LayoutInflater.from(this).inflate(R.layout.dialog_layout,null);
	Button button = view.findViewById(R.id.dialog_logout_button_id);
	final TextView uid = view.findViewById(R.id.dialog_username_EditText_id);
	final TextView pass = view.findViewById(R.id.dialog_password_EditText_id);
	button.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View view) {
			Toast.makeText(MainActivity.this,"账号"+uid.getText().toString()+"密码"+pass.getText().toString(),Toast.LENGTH_SHORT).show();
		}
	});
	builder.setView(view);
	AlertDialog dialog = builder.create();
	//可设置动画与位置
	Window window = dialog.getWindow();
	window.setGravity(Gravity.BOTTOM);
	dialog.show();
}
```

dialog_layout.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#cccccc"
        android:orientation="vertical">

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="30dp">

            <TextView
                android:id="@+id/dialog_textView_id"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_centerInParent="true"
                android:text="自定义布局"
                android:textAppearance="?android:attr/textAppearanceLarge"
                android:textColor="#cc0000" />
        </RelativeLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginLeft="20dp"
            android:layout_marginTop="10dp"
            android:layout_marginRight="20dp"
            android:paddingLeft="20dp"
            android:paddingRight="20dp">

            <EditText
                android:id="@+id/dialog_username_EditText_id"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_gravity="center_vertical"
                android:background="@null"
                android:ems="10"
                android:hint="学号/账号"
                android:inputType="number">

                <requestFocus />
            </EditText>
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginLeft="20dp"
            android:layout_marginRight="20dp"
            android:paddingLeft="20dp"
            android:paddingRight="20dp">

            <EditText
                android:id="@+id/dialog_password_EditText_id"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_gravity="center_vertical"
                android:background="@null"
                android:ems="10"
                android:hint="密码"
                android:password="true" />
        </LinearLayout>

        <Button
            android:id="@+id/dialog_logout_button_id"
            android:layout_width="match_parent"
            android:layout_height="45dp"
            android:gravity="center_horizontal"
            android:text="确定"
            android:textColor="#535252"
            android:textSize="20sp" />
    </LinearLayout>

</RelativeLayout>
```

7.进度条
```java
public void makeDialog(){
	final ProgressDialog dialog = new ProgressDialog(this);
	dialog.setTitle("title");
	dialog.setMessage("msg");
	dialog.setCancelable(false);// 设置点击空白处也不能关闭该对话框

	dialog.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
	// dialog.setProgressStyle(ProgressDialog.STYLE_SPINNER);//设置采用圆形进度条

	dialog.setMax(100);
	// dialog.setIndeterminate(true);//设置不显示明确的进度
	dialog.setIndeterminate(false);// 设置显示明确的进度

	dialog.setButton(ProgressDialog.BUTTON_POSITIVE, "确定",
		new DialogInterface.OnClickListener() {
			public void onClick(DialogInterface dialog, int whichButton) {
				// 这里添加点击后的逻辑
			}
		});
	dialog.setButton(ProgressDialog.BUTTON_NEUTRAL, "中立",
		new DialogInterface.OnClickListener() {
			public void onClick(DialogInterface dialog, int whichButton) {
				// 这里添加点击后的逻辑
			}
		});
	dialog.setButton(ProgressDialog.BUTTON_NEGATIVE, "取消",
		new DialogInterface.OnClickListener() {
			public void onClick(DialogInterface dialog, int whichButton) {
				// 这里添加点击后的逻辑
			}
		});
	dialog.show();

	//启动线程，模拟一个耗时的操作
 	new Thread(new Runnable() {
		@Override
		public void run() {
			int Progress = 0;
				while (Progress < 100) {
				try {
					Thread.sleep(100);
					Progress++;
					// dialog.setProgress(Progress);
					dialog.incrementProgressBy(1);// 进度条一次加10
				} catch (InterruptedException e) {
                        e.printStackTrace();
				}
			}
			dialog.dismiss();// 完成后消失
		}
	}).start();
}

```
8.日期选择器
```java
public void dateDialog() {
	Calendar c = Calendar.getInstance();
	DatePickerDialog dialog = new DatePickerDialog(this,
		new DatePickerDialog.OnDateSetListener() {
			@Override
			public void onDateSet(DatePicker dp, int year, int month,
				int dayOfMonth) {
                        Toast.makeText(MainActivity.this,year + "-" + (month + 1) + "-" + dayOfMonth
							,Toast.LENGTH_SHORT).show();
			}
	}, c.get(Calendar.YEAR), c.get(Calendar.MONTH),
		c.get(Calendar.DAY_OF_MONTH));
	dialog.show();
}
```

9.时间选择器
```java
public void timeDialog() {
	Calendar c = Calendar.getInstance();
	new TimePickerDialog(this,
		new TimePickerDialog.OnTimeSetListener() {

			@Override
			public void onTimeSet(TimePicker arg0, int hourOfDay,
				int minute) {
 					Toast.makeText(MainActivity.this,hourOfDay + ":" + minute
						,Toast.LENGTH_SHORT).show();
			}
		}, c.get(Calendar.HOUR_OF_DAY), c.get(Calendar.MINUTE), true)
	.show();
}
```

#### PopupWindow
与Dialog不同的是，PopupWindow指定位置更加的灵活。  
1.构造：构造的时候必须要设置View和窗体大小
```java
//方法一：
public PopupWindow (Context context)
//方法二：
public PopupWindow(View contentView)
//方法三：
public PopupWindow(View contentView, int width, int height)
//方法四：
public PopupWindow(View contentView, int width, int height, boolean focusable)
```
2.位置：位置分为相对于某控件与相对于父控件
```java

//相对某个控件的位置（正左下方），无偏移
showAsDropDown(View anchor)
//相对某个控件的位置，有偏移;xoff表示x轴的偏移，正值表示向左，负值表示向右；yoff表示相对y轴的偏移，正值是向下，负值是向上
showAsDropDown(View anchor, int xoff, int yoff)
//相对于父控件的位置（例如正中央Gravity.CENTER，下方Gravity.BOTTOM等），可以设置偏移或无偏移
showAtLocation(View parent, int gravity, int x, int y)

```

3.其他函数
```java
//关闭窗体
public void dismiss()
//PopupWindow是否具有获取焦点的能力，默认为False。一般来讲是没有用的，因为普通的控件是不需要获取焦点的，而对于EditText则不同，如果不能获取焦点，那么EditText将是无法编辑的。
public void setFocusable(boolean focusable)
//PopupWindow是否响应touch事件
public void setTouchable(boolean touchable)
//PopupWindow以外的区域是否可点击，即如果点击PopupWindow以外的区域，PopupWindow是否会消失。
public void setOutsideTouchable(boolean touchable)
//设置背景，而且只有加了PopupWindow的setOutsideTouchable才有用，不加的话点返回键会直接推出Activity。
public void setBackgroundDrawable(Drawable background)

```
示例：

```java
/**
* @param title 标题
* @param v 参考组件
* */
public void popupWindowDialog(String title, View v) {
	// 装载布局文件
	View view = LayoutInflater.from(this).inflate(
                R.layout.dialog_layout, null);
	// 创建PopupWindow对象，添加视图，设置宽高，最后一个参数为设置点击屏幕空白处(按返回键)对话框消失。
	// 也可以用.setFocusable(true);.
	final PopupWindow pWindow = new PopupWindow(view,
                WindowManager.LayoutParams.MATCH_PARENT, WindowManager.LayoutParams.WRAP_CONTENT, true);
	pWindow.setBackgroundDrawable(new BitmapDrawable());// 为了让对话框点击空白处消失，必须有这条语句
	pWindow.setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_RESIZE);// 出现输入法时，重新布局
	//pWindow.setAnimationStyle(R.style.myAnimationstyle);// 设置动画

	TextView titleTv = (TextView) view
                .findViewById(R.id.dialog_textView_id);
	titleTv.setText(title);
	Button btn = (Button) view.findViewById(R.id.dialog_logout_button_id);
	btn.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View arg0) {
			Toast.makeText(MainActivity.this,"按钮按下",Toast.LENGTH_SHORT);
				pWindow.dismiss();
		}
	});
	// 用下拉方式显示
	pWindow.showAsDropDown(v);

	//指定显示位置
	//pWindow.showAtLocation(v, Gravity.BOTTOM, 0, 0);
}
```

#### ListPopupWindow
Popup的列表版，需要添加适配器
- setAdapter : 设置下拉列表的数据适配器。 
- setModal : 设置显示模式，设置为true响应物理键
- setWidth : 设置下拉列表窗口的宽度。 
- setHeight : 设置下拉列表窗口的高度。 
- setAnchorView : 设置下拉列表的参照控件，下拉列表在显示时将展现在参照控件的下方。注意：如果不设置参照控件就直接调用show函数，系统不知道要把下拉列表在何处展示，只能是异常退出了。 
- setDropDownGravity : 设置下拉列表的对齐方式。Gravity.START表示与参照控件左侧对齐，Gravity.END表示与参照控件右侧对齐。注意：该函数只在4.4.2及以上版本中使用。 
- setOnItemClickListener : 设置列表项的点击监听器。 
- setHorizontalOffset : 相对锚点偏移值，正值表示向右偏移
- setVerticalOffset : 相对锚点偏移值，正值表示向下偏移
- show : 显示下拉列表窗口。 
- dismiss : 关闭下拉列表窗口。 
- setOnDismissListener : 设置下拉列表的关闭监听器。

```java
/**
* @param view 设置参考组件
* */
public void listPopupWindowDialog(View view) {
	final ListPopupWindow listPopupWindow = new ListPopupWindow(this);

	final String[] str = new String[]{"item1","item2","item3"};
	ArrayAdapter listPopupWindowAdapter = new ArrayAdapter(this,android.R.layout.simple_list_item_activated_1,str);

	// 添加适配器
	listPopupWindow.setAdapter(listPopupWindowAdapter);
	// 设置弹窗的大小
	listPopupWindow.setWidth(LinearLayout.LayoutParams.WRAP_CONTENT);
	listPopupWindow.setHeight(LinearLayout.LayoutParams.WRAP_CONTENT);
	//设置参考组件
	listPopupWindow.setAnchorView(view);
	// 设置背景
 	//listPopupWindow.setBackgroundDrawable();
	//模态框，设置为true响应物理键
	listPopupWindow.setModal(true);
	listPopupWindow.setOnItemClickListener(new AdapterView.OnItemClickListener() {
		@Override
		public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
			Toast.makeText(MainActivity.this,str[i]+"is selected",Toast.LENGTH_SHORT).show();
			listPopupWindow.dismiss();
		}
	});
	listPopupWindow.show();
}
```

#### DialogFragment
DialogFragment的使用能降低Dialog使用的耦合性，同时具有完整的生命周期处理(与Fragment一致)。

创建方式：
1.覆写onCreateDialog，用于写传统的AlterDialog等。
2.覆写onCreateView，用于写自定义的窗体。

MyDialogFragment.java
```java
package com.fb.menus;

import android.content.DialogInterface;
import android.os.Bundle;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;

import androidx.fragment.app.DialogFragment;

public class MyDialogFragment extends DialogFragment{
    Button log;
    EditText uid,pass;
    LogListener logListener;
    public static MyDialogFragment newInstance(String prompt){
        MyDialogFragment mdf = new MyDialogFragment();
        Bundle b = new Bundle();
        b.putString("prompt-message", prompt);
        mdf.setArguments(b);
        return mdf;
    }

    //实现Dialog的UI
    @Override
    public View onCreateView(LayoutInflater inflater,ViewGroup container,Bundle savedInstanceState) {
        View view = LayoutInflater.from(this.getContext()).inflate(R.layout.dialog_layout,null);
        log = view.findViewById(R.id.dialog_logout_button_id);
        uid = view.findViewById(R.id.dialog_username_EditText_id);
        pass = view.findViewById(R.id.dialog_password_EditText_id);
        //加载完成之后将参数放入接口
        logListener.Login(uid,pass,log);
        return view;
    }

    @Override //仅用于状态跟踪
    public void onCancel(DialogInterface dialog) {
        showInfo("onCancel() is called");
        super.onCancel(dialog);
    }

    @Override  //仅用户状态跟踪
    public void onDismiss(DialogInterface dialog) {
        showInfo("onDismiss() is called");
        super.onDismiss(dialog);
    }

    public void setLogListener(LogListener logListener){
        this.logListener = logListener;
    }

    public interface LogListener{
        void Login(EditText uid,EditText pass,Button Log);
    }

    private void showInfo(String s){
        Log.d("PromptDialogFragment",s);
    }
}

```

界面调用
```java
MyDialogFragment fragment = MyDialogFragment.newInstance("title");
fragment.show(getSupportFragmentManager(), "MyDialog");
fragment.setLogListener(new MyDialogFragment.LogListener() {
	@Override
	public void Login(final EditText uid, EditText pass, Button Log) {
		Log.setOnClickListener(new View.OnClickListener() {
			@Override
			public void onClick(View view) {
				Toast.makeText(MainActivity.this,"uid"+uid.getText().toString(),Toast.LENGTH_SHORT).show();
			}
		});
	}
});
```

AlertDialog
```java
@Override
    public Dialog onCreateDialog(Bundle savedInstanceState) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this.getContext());
        Dialog dialog = builder.setTitle("title").setMessage("message").create();
        return dialog;
    }
```

## Notification
初始化Manager
```java
NotificationManager manager = (NotificationManager)getSystemService(Context.NOTIFICATION_SERVICE);
```

兼容性问题
```java
//解决API26版本问题
String id ="channel_1";//channel的id
String name ="channel_1";//channel的id
int importance = NotificationManager.IMPORTANCE_LOW;//channel的重要性
if (android.os.Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
	// 传入参数：通道ID，通道名字，通道优先级（类似曾经的 builder.setPriority()）
	NotificationChannel channel =
                    new NotificationChannel(id, name,importance);

	// 配置通知渠道的属性
	channel.setDescription("des");
	// 设置通知出现时声音，默认通知是有声音的
	channel.setSound(null, null);
	// 设置通知出现时的闪灯（如果 android 设备支持的话）
	channel.enableLights(true);
	channel.setLightColor(Color.RED);
	// 设置通知出现时的震动（如果 android 设备支持的话）
	channel.enableVibration(true);
	channel.setVibrationPattern(new long[]{100, 200, 300, 400, 500, 400, 300, 200, 400});

	//最后在 notificationManager 中创建该通知渠道
	manager.createNotificationChannel(channel);
}
```

点击效果准备
```java
//准备intent
Intent clickIntent = new Intent(this, MainActivity.class);
PendingIntent clickPI = PendingIntent.getActivity(this, 1,
	clickIntent,PendingIntent.FLAG_CANCEL_CURRENT);
```

设置Notification
```java
//第二个参数需要传入channel的id
NotificationCompat.Builder builder = new NotificationCompat.Builder(MainActivity.this,id);
builder.setSmallIcon(android.R.drawable.star_on)//设置小图标
	.setLargeIcon(BitmapFactory.decodeResource(getResources(),android.R.drawable.alert_light_frame))//设置大图标
	.setTicker("来了一条设置属性通知")//5.0之后开辅助功能才有用
	.setContentTitle("我是通知的标题")//设置通知标题
	.setContentText("我是一个通知")//设置通知内容
	.setWhen(System.currentTimeMillis())//不加系统会默认加
	.setAutoCancel(true)//自动取消，不加点击后通知还存在
	.setNumber(23)//显示数字，一部分不支持
	.setContentIntent(clickPI);// 设置pendingIntent,点击通知时就会用到
```

发送通知
```java
manager.notify(1,builder.build());
```