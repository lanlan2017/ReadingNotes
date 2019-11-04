---
title: 示例 @RequestBody接收JSON格式的数据
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.13 @RequestBody注解
date: 2019-08-20 18:45:02
updated: 2019-11-02 01:39:00
abbrlink: 78f2a207
---
- [示例 @RequestBody接收JSON格式的数据](/ReadingNotes/78f2a207/#示例-RequestBody接收JSON格式的数据)
    - [index.jsp](/ReadingNotes/78f2a207/#index-jsp)
    - [BookController.java](/ReadingNotes/78f2a207/#BookController-java)
    - [BookController.java](/ReadingNotes/78f2a207/#BookController-java)
    - [Book.java](/ReadingNotes/78f2a207/#Book-java)
    - [个人总结](/ReadingNotes/78f2a207/#个人总结)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 @RequestBody接收JSON格式的数据 #
创建一个`RequestBodyTest`项目,在`WebContent`目录下创建一个`js`目录,加入`jQuery`和`json2`的`js`文件,在`WEB-INF/lib`目录中加入`Jackson`的`jar`文件。
## index.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试接收JSON格式的数据</title>
<script type="text/javascript" src="js/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="js/json2.js"></script>
<script type="text/javascript">
	// DOM加载完毕后就直接发送请求
	$(document).ready(function() {
		testRequestBody();
	});
	function testRequestBody() {
		//发送ajax请求
		$.ajax(// 发送请求的URL字符串。
		"${pageContext.request.contextPath}/json/testRequestBody", {
			// 预期服务器返回的数据类型。
			dataType : "json",
			//  请求方式 POST或GET
			type : "post",
			//  发送信息至服务器时的内容编码类型
			contentType : "application/json",
			// 发送到服务器的数据。
			data : JSON.stringify({
				id : 1,
				name : "一本书的名字"
			}),
			// 默认设置为true，此时所有请求均为异步请求。
			// 如果设置为false，则发送同步请求
			async : true,
			// 请求成功后的回调函数。
			success : function(data) {
				console.log(data);
				//使用接收到的数据更新网页内容
				$("#id").html(data.id);
				$("#name").html(data.name);
				$("#author").html(data.author);
			},
			// 请求出错时调用的函数
			error : function() {
				alert("数据发送失败");
			}
		});
	}
</script>
</head>
<body>
    编号：
    <span id="id"></span>
    <br> 书名：
    <span id="name"></span>
    <br> 作者：
    <span id="author"></span>
    <br>
</body>
</html>
```
`index.jsp`页面代码分析如下:
(1)页面使用`jQuery`发送`JSON`数据,在页面的`<head>`部分,引入了`jQuery`和`json2`的`js`文件。
(2)页面载入时调用`testRequestBody`函数。
(3)`testRequestBody`函数的第一个参数表示要请求的URL是:`"json/testRequestBody"`,第二个参数是这次请求相关的一些设置选项,这些选项解释如下:
- `contentType`选项:`contentType : "application/json",`,其表示发送的内容编码格式为`JSON`
- `data`选项:`data : JSON.stringify({id : 1,name : "一本书的名字"}),`表示发送一个`JSON`数据;
- `success`选项表示:如果请求成功则将接到的`JSON`数据设置到页面的`<span>`当中

## BookController.java ##
```java
package org.fkit.controller;

import javax.servlet.http.HttpServletResponse;
import org.fkit.domain.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import com.fasterxml.jackson.databind.ObjectMapper;

@Controller
@RequestMapping("/json")
public class BookController
{
	// @RequestBody根据json数据，转换成对应的Object
	@RequestMapping(value = "/testRequestBody")
	// @RequestBody Book book:使用@RequestBody获取JSON数据,
	// 然后将JSON数据设置到对应的Book对象的属性之中.
	// 第二个参数 HttpServletResponse response用来输出响应数据到客户端
	public void setJson(@RequestBody Book book, HttpServletResponse response)
	        throws Exception
	{
		// ObjectMapper类是Jackson库的主要类。
		// 它提供一些功能将Java对象转换成对应的JSON格式的数据
		ObjectMapper mapper = new ObjectMapper();
		// 将book对象转换成json,并输出到控制台
		System.out.println(mapper.writeValueAsString(book));
		// 设置完整的信息
		book.setAuthor("小明");
		// 设置响应类型
		response.setContentType("text/html;charset=UTF-8");
		// 将book对象转换成json写出到客户端
		response.getWriter().println(mapper.writeValueAsString(book));
	}
}
```
## BookController.java ##
```java
package org.fkit.controller;

import javax.servlet.http.HttpServletResponse;
import org.fkit.domain.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import com.fasterxml.jackson.databind.ObjectMapper;

@Controller
@RequestMapping("/json")
public class BookController
{
	// @RequestBody根据json数据，转换成对应的Object
	@RequestMapping(value = "/testRequestBody")
	// @RequestBody Book book:使用@RequestBody获取JSON数据,
	// 然后将JSON数据设置到对应的Book对象的属性之中.
	// 第二个参数 HttpServletResponse response用来输出响应数据到客户端
	public void setJson(@RequestBody Book book, HttpServletResponse response)
	        throws Exception
	{
		// ObjectMapper类是Jackson库的主要类。
		// 它提供一些功能将Java对象转换成对应的JSON格式的数据
		ObjectMapper mapper = new ObjectMapper();
		// 将book对象转换成json,并输出到控制台
		System.out.println(mapper.writeValueAsString(book));
		// 设置完整的信息
		book.setAuthor("小明");
		// 设置响应类型
		response.setContentType("text/html;charset=UTF-8");
		// 将book对象转换成json写出到客户端
		response.getWriter().println(mapper.writeValueAsString(book));
	}
}
```
`setJson`方法中的第一个参数`@RequestBody Book book`表示,使用`@RequestBody`注解获取`JSON`数据后,将`JSON`数据设置到对应的`Book`对象的属性当中。第二个参数是`HttpServletResponse`对象,用来输出响应数据到客户端。
向前台`JSP`页面的`JSON`数据中传入了`id`和`name`,为了测试接收数据,使用`System.out.println(mapper.writeValueAsString(book));`代码将接收到的`JSON`数据中的`book`对象打印在控制台上。
为了测试传递数据到`JSP`页面,在该方法中还给`book`对象的`author`对象设置了个值,并将其写出到客户端.
## Book.java ##
```java
package org.fkit.domain;

import java.io.Serializable;

public class Book implements Serializable
{
	private static final long serialVersionUID = 1L;
	private Integer id;
	private String name;
	private String author;
	public Integer getId()
	{
		return id;
	}
	public void setId(Integer id)
	{
		this.id = id;
	}
	public String getName()
	{
		return name;
	}
	public void setName(String name)
	{
		this.name = name;
	}
	public String getAuthor()
	{
		return author;
	}
	public void setAuthor(String author)
	{
		this.author = author;
	}
	@Override
	public String toString()
	{
		return "Book [id=" + id + ", name=" + name + ", author=" + author + "]";
	}
}
```
在`Book`类中定义了3个属性:`id`、`name`和`author`,用于接收向`JSP`页面传入的`JSON`数据`toString`方法用来输出获取的数据对象信息.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">

    <!-- spring可以自动去扫描base-pack下面的包或者子包下面的java文件， -->
    <!-- 如果扫描到有Spring的相关注解的类，则把这些类注册为Spring的bean -->
    <context:component-scan
        base-package="org.fkit.controller" />
    <!-- 默认配置方案 -->
    <mvc:annotation-driven />
    <!-- 静态资源处理 -->
    <mvc:default-servlet-handler />
    <!-- 视图解析器 p:prefix属性表示前缀 p:suffix 表示后缀 -->
    <bean id="viewResolver"
        class="org.springframework.web.servlet.view.InternalResourceViewResolver"
        p:prefix="/WEB-INF/content/" p:suffix=".jsp" />
</beans>
```
在引入静态文件,例如`jQuery.js`时,需要加入`<mvc:default-servlet-handler />`从而使用默认的`Servlet`来响应静态文件。如果没有加入该配置,则执行时页面会报404错误,而控制台会提出警告:

部署`RequestBodyTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/RequestBodyTest/
```
载入`index.jsp`页面时会发送`Ajax`请求,并传递`JSON`数据, `BookController`接收到请求后,`@Request body`注解会将接收到的`JSON`数据设置到`Book`形式参数对应的属性当中。控制台输出如下:
```
{"id":1,"name":"一本书的名字","author":null}
```
可以看到,`JSON`数据传递的`id`和`name`被赋值到`Book`对象的属性中。接下来, `setJson`方法给`Book`对象的`author`属性设置了值,并将`Book`对象转换成`JSON`写出到客户端。
此时客户端显示效果如下:
```
 编号： 1
书名： 一本书的名字
作者： 小明
```
这表示`Spring MVC`成功将`Book`对象被以`JSON`数据格式成功写到客户端了。

## 个人总结 ##
使用`JSON`交换的步骤:
1. 使用`jQuery`发送`ajax`请求,并将数据以`JSON`格式发送.
2. 引入`Jackson`的`jar`包,使用`@RequstBody`接收数据,该注解可以解析请求体中的`JSON`数据,并设置到其后面的对象上。
3. 使用`Jackson`包中的`ObjectMapper`对象`.writeValueAsString(Java`对象)方法,将`Java`对象转为`JSON`字符串.
4. 使用`HttpServletResponse`写到客户端即可.
5. `jQuery`根据接收到的`JSON`数据操作`DOM`即可。

<!--SSTStop-->

