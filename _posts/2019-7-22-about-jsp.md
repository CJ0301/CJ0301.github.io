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
- 静态部分：由标准的HTML标签等静态页面所具备的内容所控制。
- 动态部分：受Java程序控制的内容，主要用于客户端与服务器之间的交互。

![](/img/in-posts/JSP-1.png)
根据原理图我们可以得出如下四个结论：
- JSP文件必须在JSP服务器内运行。
- JSP文件必须生成对应的Servlet才能执行。
- 每个JSP文件的第一个访问者速度会有点慢，因为必须要等JSP被编译成Servlet。
- JSP页面的访问者无需安装任何客户端或者运行环境，因为输送到客户端的是标准的HTML页面。

### JSP的4种基本语法
JSP的开发过程：编写静态HTML页面->在HTML页面种嵌套JSP的基本语法

#### JSP的注释
JSP的注释格式如下：
```
<%--JSP的注释方式--%>
```
```
<!--HTML的注释方式--!>
```
二者的区别就是HTML的注释可以通过源码查看，而JSP的注释不会发送到客户端，在编译的过程中被丢弃了。

#### JSP的声明
JSP声明用于声明变量与方法，在编译之后声明会转换成Servlet的成员变量与成员方法，由于符合Java语法
定义也能加入public之类的访问修饰符。<br/>
JSP的声明格式如下：
```
<%!JSP的声明格式%>
```
#### JSP输出表达式
JSP规定了一个简化out.println的输出形式。
```
<%=输出内容%> *输出表达式语法不能有分号
```
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
```
<%@ 编译指令名 属性名="属性值"....%>
```
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
- language：声明当前JSP页面使用的脚本语言类型，默认为Java，一般无需设置。
- extends：指定编译后的Servlet类需要继承的父类。
- import：导入需要的包，默认导入的包有：java.lang. *、java.servlet. *、java.servlet.jsp. *、java.servlet.http. *。
- session：设定这个JSP页面是否需要HTTP Session。
- buffer：指定输出缓冲区大小。输出缓冲区的JSP内部对象：out用于缓存JSP页面对客户浏览器的输出，默认为8KB。
- autoFlush：发明和输出缓冲区即将溢出时，是否需要强制输出缓冲区的内容，true正常输出，false产生异常。
- info：设置JSP程序的信息，也可以看作是说明，可以通过Servlet.getServletInfo()方法获取，如果是在JSP页面可直接调用getServletInfo()方法，其实质就是Servlet。
- errorPage：指定错误处理页面。如果本页发生错误与异常，若该页面没有处理代码，则会自动调用该属性指定的JSP页面。
- isErrorPage：设置本JSP页面是否为错误处理程序。如果是，通常不再指定errorPage属性。
- contentType：用于设定生成网页文件格式与编码字符集，即MIME类型和页面字符集类型，默认分别是text/html和ISO-8859-1。

#### include指令：
使用include指令，可以将一个外部文件嵌入到当前JSP文件中，被包含的文件不能加编译指令，否则会导致页面出错，这里的导入是静态导入。


### JSP的7个动作指令
动作指令与编译指令不同，编译指令时在编译过程通知Servlet引擎处理的内容，而动作指令是运行时的动作，通常可被替换成JSP小脚本，属于JSP小脚本的标准化写法。
JSP动作指令主要有如下7个：
- jsp:forward ：执行页面的转向，将请求的处理转发到下一个页面。
- jsp:param ：用于传递参数，必须与其他支持参数的标签一起使用。
- jsp:include ：用于动态包含一个JSP页面。
- jsp:plugin ：用于下载JavaBean或Applet到客户端执行。
- jsp:useBean ：创建一个JavaBean的实例。
- jsp:setProperty ：设置JavaBean实例的属性值。
- jsp:getProperty ：输出JavaBean实例的属性值。

#### forward指令
forward指令用于将页面响应转发到另外的页面。既可转发到静态的HTML页面，
也可以转发到动态的JSP页面，或者转发到容器的Servlet。<br/>
JSP 1.0使用如下语法：
```
<jsp:forward page="{relativeURL|<%=expression%>}"/>
```

JSP 1.1以上使用如下语法：
```
<jsp:forward page="{relativeURL|<%=expression%>}">
	{<jsp:param.../>}
</jsp:forward>
```
第二种语法用于在转发时增加额外的请求参数。可通过HttpServletRequest的getParameter()方法获取
执行forward指令时，用户请求的地址依然没变，但页面内容却完全变成forward目标页的内容。

#### include指令
include指令是一条动态的include指令，也用于包含某个页面，他不会被include页面的编译指令，仅仅将被导入页面的body内容插入本页面<br/>
include的语法格式：
```
<jsp:include page="{relativeURL|<%=expression%>}" flush="true"/>
```
或者
```
<jsp:include page="{relativeURL|<%=expression%>}" flush="true">
	{<jsp:param name="parameterName" value="parameterValue"/>}
</jsp:include>	
```
flush属性用于指定输出缓存是否转移到被导入文件中，true则包含，false则不包含，1.1之前只能选择false

静态导入与动态导入的区别：
- 静态导入是将被导入页面的代码完全融入，两个页面融合成一个Servlet；而动态导入则是在Servlet中使用include方法来引入被导入页的内容
- 静态导入时被导入页面的编译指令会起作用；而动态导入时被导入页面的编译指令则失去作用，只是插入被导入页面的body内容
- 动态导入还可以增加额外的参数。

>实际上，forward动作指令与include动作指令十分相似，都采用方法来引入目标页面。区别在于：执行forward时，
被forward的页面将完全替代原有页面；而执行include时，被include的页面只是插入原有的页面。

#### useBean、setProperty、getProperty指令
这三个指令都是与JavaBean相关的指令，useBean用于在JSP页面中初始化一个Java实例；setProperty用于为JavaBean实例的属性设置值；
getProperty指令用于输出JavaBean实例的属性值。
useBean的语法格式如下：
```
<jsp:useBean id="name" class="classname" scope="page|request|session|application/>
```
其中id属性是JavaBean的实例名，class属性确定JavaBean的实现类。scope属性用于指定JavaBean实例的作用范围，范围有以下四个值：
- page：该JavaBean实例仅在该页面有效。
- request：该JavaBean实例在本次请求有效。
- request：该JavaBean实例在本次session内有效。
- request：该JavaBean实例在本应用内一直有效。

setProperty指令的语法格式如下：
```
<jsp:setProperty name="BeanName" property="propertyName" value="value"/>
```
name属性设定JavaBean的实例名，property属性设定属性名，value属性设定属性值。

getProperty指令的语法格式如下：
```
<jsp:setProperty name="BeanName" property="propertyName"/>
```
name属性设定JavaBean的实例名，property属性设定属性名。

#### plugin指令
plugin指令主要用于下载服务器端的JavaBean或Applet到客户端执行。由于程序在客户端执行，因此客户端需要安装虚拟机。现在用的少，这里不多做介绍了。

#### param指令
param指令用于设置参数值，这个指令本身不能单独使用，因为单独的param指令没有实际意义。param指令可以与以下三个指令结合使用：
- jsp:include    参数值传入被导入页面
- jsp:forward	 参数值传入转向页面
- jsp:plugin	 参数值传入页面中的JavaBean实例或Applet实例

param指令的语法格式如下：
```
<jsp:param name="paramName" value="parameterValue"/>
```
使用方式[点击此处](/2019/07/22/about-jsp/#jsp的7个动作指令)向上跳转

### JSP的9个内置对象
- application：javax.servlet.ServletContext的实例，该实例代表JSP所属的Web应用本身，可用于JSP页面或是Servlet之间交换信息，
常用的方法有getAttribute(String attName)、setAttribute(String attName,String attValue)和getInitParameter(String paramName)等。
- config：java.servlet.ServletConfig的实例，该实例代表该JSP的配置信息。常用的方法有getInitParameter(String paramName)和getInitParameters()等方法。
事实上，JSP通常无需配置。该对象更多的在Servlet中有效。
- exception：java.lang.Throwable的实例，该实例代表其他页面中的异常和错误。只有当页面时错误处理页面，即编译指令的isErrorPage属性为true时，该对象才能使用。
常用的方法有getMessage()和printStackTrace()等。
- out：javax.servlet.jsp.JspWriter的实例，该实例代表JSP页面的输出流，用于输出内容，形成HTML页面。实际使用被等号代替。
- page：代表页面本身，通常没多大用处。也就是Servlet中的this。二者可以进行替换。
- pageContext：javax.servlet.jsp.pageContext的实例，该对象代表JSP页面的上下文，使用该对象可以访问页面中的共享数据。
常用的方法有getServletContext()和getServletConfig()等。
- request：javax.servlet.http.HTTPServletRequest的实例，该对象封装了一次请求，客户端的请求参数都被封装在该对象中。
常用的方法有：getParameter(String paramName)、getParameterValues(String paraName)、setAttribution(String attName,Object attValue)、
getAttribute(String attName)和setCharacterEncoding(String env)等
- response：javax.servlet.http.HTTPServletResponse的实例,代表服务器对客户端的响应。通常很少使用该对象的直接响应，而是使用out对象，除非需要生成非字符的响应。response对象常用于重定向，
常用的方法有getOutputStream()、sendRedirect(String location)等。
- session：javax.servlet.http.HTTPServletSession的实例，该对象代表一次会话。当客户端浏览器与站点建立连接时，会话开始。关闭浏览器时，会话结束。
常用方法有：getAttribution(String attName)、setAttribute(String attName,Object attValue)等。

上面对象在编译之后会变成Servlet类中_jspService()方法的局部变量。所以只能在JSP小脚本、输出表达式中使用这些内置对象。

