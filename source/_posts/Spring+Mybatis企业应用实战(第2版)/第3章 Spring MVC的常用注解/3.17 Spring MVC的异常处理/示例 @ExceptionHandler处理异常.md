---
title: 示例 @ExceptionHandler处理异常
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.17 Spring MVC的异常处理
date: 2019-08-21 15:45:26
updated: 2019-11-02 01:39:00
abbrlink: a0f3b85b
---
- [示例 @ExceptionHandler处理异常](/ReadingNotes/a0f3b85b/#示例-ExceptionHandler处理异常)
    - [index.jsp](/ReadingNotes/a0f3b85b/#index-jsp)
    - [TestController.java](/ReadingNotes/a0f3b85b/#TestController-java)
    - [error.jsp](/ReadingNotes/a0f3b85b/#error-jsp)
- [更好一点的做法](/ReadingNotes/a0f3b85b/#更好一点的做法)
    - [BaseExceptionController.java](/ReadingNotes/a0f3b85b/#BaseExceptionController-java)
    - [UserController.java](/ReadingNotes/a0f3b85b/#UserController-java)
    - [BookController.java](/ReadingNotes/a0f3b85b/#BookController-java)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 @ExceptionHandler处理异常 #
新建一个项目`ExceptionHandlerTest`,加入所需的`jar`文件,示例代码如下:
## index.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>异常处理示例</title>
</head>
<body>
    <a href="test">@ExceptionHandler处理异常</a>
    <br>
    <a href="login">UserController：使用从父类继承来的异常处理方法</a>
    <br>
    <a href="find">BookController：使用从父类继承来的异常处理方法</a>
    <br>
</body>
</html>
```
`index.jsp`中有3个超链接,分别用于测试`@ExceptionHandler`异常处理和使用父级`Controller`异常处理。
## TestController.java ##
```java
package org.fkit.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class TestController
{
	@GetMapping("/test")
	public String test() throws Exception
	{
		// 模拟异常,调用本类中定义的异常处理方法
		@SuppressWarnings("unused")
		int i = 5 / 0;
		return "success";
	}
	// 在异常抛出的时候，Controller会使用@ExceptionHandler注解的方法去处理异常
	// value=Exception.class表示处理所有的Exception类型异常。
	@ExceptionHandler(value = Exception.class)
	public ModelAndView testErrorHandler(Exception e)
	{
		ModelAndView mav = new ModelAndView();
		mav.setViewName("error");
		mav.addObject("ex", e);
		return mav;
	}
}
```
`TestController`中`test()`方法是`index.jsp`页面的超链接`"@ExceptionHandler处理异常`"的请求处理方法,模拟了一个除数不能为0的异常。
`testErrorHandler()`方法使用了`@ExceptionHandler`注解, `value = Exception.class`表示处理所有的`Exception`类型异常。**当`TestController`类抛出异常的时候,会使用`@ExceptionHandler`注解的方法去处理异常,而不会直接抛给浏览器**。 `testErrorHandler()`方法将捕捉到的异常对象保存到`ModelAndView`当中,传递到`JSP`页面。
## error.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试@ExceptionHandler注解</title>
</head>
<body>
    <h3>异常处理页面</h3>
    抛出异常信息：${requestScope.ex.message}
</body>
</html>
```
部署`ExceptionHandlerTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/ExceptionHandlerTest/
```
单击`"@ExceptionHandler处理异常`"超链接,发送`"test"`请求,`TestController`的`test()`方方法在处理请求抛出异常,异常会被同一类中的`@ExceptionHandler`注解修饰的`testErrorHandler`方法捕获,处理之后跳转到`error.jsp`页面。


# 更好一点的做法 #
基于`Controller`的`@ExceptionHandler`注解方法在进行异常处理时,对于每个`Controller`都需要写`@ExceptionHandler`注解的异常处理方法,在实际开发当中这非常烦琐。可以写一个父类,在父类中完成`@ExceptionHandler`注解的异常处理方法,所有的`Controller`继承这个父类,则所有的`Controller`就都拥有了`@ExceptionHandler`注解的异常处理方法。
## BaseExceptionController.java ##
```java
package org.fkit.controller;

import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.servlet.ModelAndView;
public class BaseExceptionController
{
	// 表示这是一个异常处理方法
	// value = Exception.class表示处理的异常类型为Exception
	// 也就是处理所有的异常
	@ExceptionHandler(value = Exception.class)
	public ModelAndView defaultErrorHandler(Exception e) throws Exception
	{
		ModelAndView mav = new ModelAndView();
		// 设置模型数据
		mav.addObject("ex", e);
		// 设置视图
		mav.setViewName("error");
		return mav;
	}
}
```
`BaseController`作为父类,定义了一个`@ExceptionHandler`注解修饰的方法。
## UserController.java ##
```java
package org.fkit.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class UserController extends BaseExceptionController
{
	@GetMapping("/login")
	public String login(String username) throws Exception
	{
		if (username == null)
		{
			// 调用本类的异常处理方法
			throw new NullPointerException("用户名不存在!");
		}
		return "success";
	}
}
```
`UserController`继承`BaseController`,如果抛出异常,将使用父类的`ExceptionHandler`注解修饰的方法处理异常。
## BookController.java ##
```java
package org.fkit.controller;

import java.sql.SQLException;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
@Controller
public class BookController extends BaseExceptionController
{
	@GetMapping("/find")
	public String find() throws Exception
	{
		try
		{
			// 除零异常,调用继承得到的异常处理方法
			@SuppressWarnings("unused")
			int i = 5 / 0;
			return "success";
		} catch (Exception e)
		{
			throw new SQLException("查找图书信息失败!");
		}
	}
}
```
`BookController`继承`BaseController`,如果抛出异常,将使用父类的`@ExceptionHandler`注解修饰的方法处理异常.
再次部署`Exception2Test`这个`Web`应用,在浏览器中输入如下`URL`来测试应用,单击`"UserController:父级Controller异常处理`"超链接,发送`login`请求,异常处理之后跳转到`error.jsp`页面.浏览器显示内容如下:
```
异常处理页面
抛出异常信息：用户名不存在! 
```
再次请求`index.jsp`页面,单击`BookController：使用从父类继承来的异常处理方法`超链接,发送`"find"`请求,异常处理之后跳转到`error.jsp`页面.此时浏览器显示内容如下:
```
异常处理页面
抛出异常信息：查找图书信息失败! 
```
<!--SSTStop-->

