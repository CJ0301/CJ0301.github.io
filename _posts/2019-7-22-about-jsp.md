---
layout: 		post
title: 			"一份关于JSP的小总结_1_"
subtitle: 		'前面的十几天一直再看JavaEE的知识，既然有了自己的博客，决定停下来稍微总结一下'
author: 		"CJ"
header-img: 	"img/post-bg-fblog.jpg"
header-mask: 	0.3
catalog: 		true
tags:
  - JSP
---

> 以下内容总结自《轻量级Java EE企业应用实战（第5版）》

### JSP的基本原理
JSP的本质是一个Servlet，当第一个用户访问时，该请求对应的JSP文件会由系统编译成Servlet，再由Servlet负责响应用户请求，
Servlet利用输出流动态生成HTML页面。JSP页面必须放在Web项目中才能生效，所以编写前必须要将其放入Web项目中。对于Tomcat来说，JSP生成的Servlet被存放在work路径对应的Web应用下。
包括每一个静态的HTML标签和所有在HTML页面出现的内容。总的来说，JSP由以下两部分构成：
- 静态部分：由标准的HTML标签等静态页面所具备的内容所控制
- 动态部分：受Java程序控制的内容，主要用于客户端与服务器之间的交互

![](/img/in-posts/JSP-1.png)
根据原理图我们可以得出如下四个结论：
- JSP文件必须在JSP服务器内运行。
- JSP文件必须生成对应的Servlet才能执行
- 每个JSP文件的第一个访问者速度会有点慢，因为必须要等JSP被编译成Servlet
- JSP页面的访问者无需安装任何客户端或者运行环境，因为输送到客户端的是标准的HTML页面

### JSP的4种基本语法
JSP的开发过程：编写静态HTML页面->在HTML页面种嵌套JSP的基本语法

#### JSP的注释
JSP的注释格式如下：
> <%--JSP的注释方式--%>

> <!--HTML的注释方式--!>

二者的区别就是HTML的注释可以通过源码查看，而JSP的注释不会发送到客户端，在编译的过程中被丢弃了

#### JSP的声明
JSP声明用于声明变量与方法，在编译之后声明会转换成Servlet的成员变量与成员方法，由于符合Java语法
定义也能加入public之类的访问修饰符。<br/>
JSP的声明格式如下：
> <%!JSP的声明格式%>

#### JSP输出表达式
JSP规定了一个简化out.println的输出形式
> <%=输出内容%> *输出表达式语法不能有分号

#### JSP小脚本
可以将HTML的内容嵌入JSP的语法之中使用
下面举一个栗子🌰：
```java
<%
for(int i=0;i<10;i++){
%>
<tr>
	<td>循环值：</td>
	<td><%=i%></td>
</tr>
<%
}
%>
```
也可以拿来连连数据库，输出结果集，这里就不演示了。

### JSP的3个编译指令
因为要生成Servlet类，必然会面临导入外部包的问题，同时JSP也要设置一些属性，这时就需要用到编译指令了。所有的属性基本都有默认值，只挑需要的设置就好了。

这里只介绍常见的三个：
- page：该指令是针对当前页面的指令
- include：用于指定包含另一个页面
- taglib：用于定义和访问自定义标签


编译指令的语法格式：
> <%@ 编译指令名 属性名="属性值"....%>

#### page指令：
常位于顶端指令的语法格式如下：
```
<%@ page
[language="Java"]
[extends="package.class"]
[import="package.class|package.*,..."]
[session="true|false"]
[buffer="none|8KB|size KB"]
[autoFlush="true|false"]
[isThreadSafe="true|false"]
[info="text"]
[errorPage="relativeURL"]
[contentType="mimeType[;charset=characterSet]"|"text/html;charset=ISO-8859-1"]
[pageEncoding="ISO-8859-1"]
[isErrorPage="true|false"]
%>
```
- language：声明当前JSP页面使用的脚本语言类型，默认为Java，一般无需设置.
- extends：指定编译后的Servlet类需要继承的父类.
- import：导入需要的包，默认导入的包有：java.lang.*、java.servlet.*、java.servlet.jsp.*、java.servlet.http.*。
- session：设定这个JSP页面是否需要HTTP Session
- buffer：指定输出缓冲区大小。输出缓冲区的JSP内部对象：out用于缓存JSP页面对客户浏览器的输出，默认为8KB。
- autoFlush：发明和输出缓冲区即将溢出时，是否需要强制输出缓冲区的内容，true正常输出，false产生异常。
- info：设置JSP程序的信息，也可以看作是说明，可以通过Servlet.getServletInfo()方法获取，如果是在JSP页面可直接调用getServletInfo()方法，其实质就是Servlet.
- errorPage：指定错误处理页面。如果本页发生错误与异常，若该页面没有处理代码，则会自动调用该属性指定的JSP页面。
- isErrorPage：设置本JSP页面是否为错误处理程序。如果是，通常不再指定errorPage属性。
- contentType：用于设定生成网页文件格式与编码字符集，即MIME类型和页面字符集类型，默认分别是text/html和ISO-8859-1。

#### include指令：
使用include指令，可以将一个外部文件嵌入到当前JSP文件中，被包含的文件不能加编译指令，否则会导致页面出错。
