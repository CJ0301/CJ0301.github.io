---
layout: 		post
title: 			"安卓持久化存储"
subtitle: 		'sqlite和sharedpreferences'
author: 		"CJ"
header-img: 	"img/post-bg-android.jpg"
outer-img:		"post-bg-android.jpg"
header-mask: 	0.3
catalog: 		true
mermaid:   		true
tags:
  - Android
---
## sqlite
#### SQLiteOpenHelper
SQlite是Android自带的一个数据库。  
首先我们需要继承SQLiteOpenHelper.java，用于帮助我们实现数据库的操纵。需要实现三个方法：构造函数，onCreate,onUpgrade。

```java
public class SQLiteHelper extends SQLiteOpenHelper {

    public SQLiteHelper(Context context,  String name,SQLiteDatabase.CursorFactory factory, int version) {
        super(context, name, factory, version);
    }

    //建表
    @Override
    public void onCreate(SQLiteDatabase db) {
        String sql = "create table user(name varchar(20))";
        db.execSQL(sql);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

    }
}
```

