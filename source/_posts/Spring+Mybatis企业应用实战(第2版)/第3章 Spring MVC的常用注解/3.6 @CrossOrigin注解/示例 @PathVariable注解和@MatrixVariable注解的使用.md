---
title: 示例 @PathVariable注解和@MatrixVariable注解的使用
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.6 @CrossOrigin注解
date: 2019-08-19 13:23:24
updated: 2019-11-02 01:39:00
abbrlink: 8ad4e730
---
- [示例 @PathVariable注解和@MatrixVariable注解的使用](/ReadingNotes/8ad4e730/#示例-PathVariable注解和-MatrixVariable注解的使用)
    - [index.jsp](/ReadingNotes/8ad4e730/#index-jsp)
    - [VariableController.java](/ReadingNotes/8ad4e730/#VariableController-java)
    - [springmvc-config.xml](/ReadingNotes/8ad4e730/#springmvc-config-xml)
    - [测试](/ReadingNotes/8ad4e730/#测试)
        - [测试@PathVariable注解](/ReadingNotes/8ad4e730/#测试-PathVariable注解)
        - [测试@MatrixVariable注解](/ReadingNotes/8ad4e730/#测试-MatrixVariable注解)
        - [@MatrixVariable注解完成复杂的参数注入](/ReadingNotes/8ad4e730/#-MatrixVariable注解完成复杂的参数注入)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 @PathVariable注解和@MatrixVariable注解的使用 #
新建一个项目`VariableTest`,加入所需的`jar`文件,示例代码如下:
## index.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>处理请求URL注解测试</title>
</head>
<body>
	<h2>处理请求URL注解测试</h2>
	<a href="pathVariableTest/1">测试@PathVariable注解</a>
	<br>
	<a href="matrixVariableTest/1;name=jack;age=23">测试@MatrixVariable注解</a>
	<br>
	<a href="productTest/computer;brand=apple,acer;low=2000;height=10000">商品条件查询（品牌，价格区间）</a>
	<br>
	<!-- 跨域请求 -->
	<a href="http://localhost:8080/CrossOriginTest/welcome">测试@CrossOrigin注解</a>
	<br>
</body>
</html>
```
## VariableController.java ##
```java
package org.fkit.controller;

import java.io.IOException;
import java.util.List;
import javax.servlet.http.HttpServletResponse;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.MatrixVariable;
import org.springframework.web.bind.annotation.PathVariable;

@Controller
public class VariableController
{

	// 测试@PathVariable注解
	// 该方法映射的请求为/VariableTest/pathVariableTest/1
	@GetMapping(value = "/pathVariableTest/{userId}")
	public void pathVariableTest(@PathVariable Integer userId,
			HttpServletResponse response)
	{
		// 直接响应不跳转页面
		try
		{
			response.setContentType("text/html;charset=UTF-8");
			response.setCharacterEncoding("UTF-8");
			response.getWriter().write("通过@PathVariable获得数据： userId=" + userId);
		} catch (IOException e)
		{
			e.printStackTrace();
		}
	}

	// 测试@MatrixVariable注解
	// 该方法映射的请求为/VariableTest/matrixVariableTest/1;name=jack;age=23
	@GetMapping(value = "/matrixVariableTest/{userId}")
	public void matrixVariableTest(@PathVariable Integer userId,
			@MatrixVariable(value = "name", pathVar = "userId") String name,
			@MatrixVariable(value = "age", pathVar = "userId") Integer age,
			HttpServletResponse response)
	{
		// 直接响应不跳转页面
		try
		{
			response.setContentType("text/html;charset=UTF-8");
			response.setCharacterEncoding("UTF-8");
			response.getWriter().write("通过@PathVariable获得数据： userId=" + userId);
			response.getWriter().write(
					"通过@MatrixVariable获得数据： name=" + name + " age=" + age);
		} catch (IOException e)
		{
			e.printStackTrace();
		}
	}

	// 测试@MatrixVariable注解的复杂例子
	// 该方法映射的请求为//VariableTest/productTest/computer;brand=apple,acer;low=2000;height=10000
	@GetMapping(value = "/productTest/{goods}")
	public void productTest(@PathVariable String goods,
			@MatrixVariable(value = "brand", pathVar = "goods") List<String> brand,
			@MatrixVariable(value = "low", pathVar = "goods") Integer low,
			@MatrixVariable(value = "height", pathVar = "goods") Integer height,
			HttpServletResponse response)
	{
		// 直接响应不跳转页面
		try
		{
			response.setContentType("text/html;charset=UTF-8");
			response.setCharacterEncoding("UTF-8");
			response.getWriter().println("通过@PathVariable获得数据： goods=" + goods+"<br>");
			response.getWriter().println("通过@MatrixVariable获得数据：brand=" + brand+"<br>");
			response.getWriter().println(
					"通过@MatrixVariable获得数据： low=" + low + " height=" + height+"<br>");
		} catch (IOException e)
		{
			e.printStackTrace();
		}
	}
}
```
## springmvc-config.xml ##
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

	<!-- spring可以自动去扫描base-pack下面的包或者子包下面的java文件， 如果扫描到有Spring的相关注解的类，则把这些类注册为Spring的bean -->
	<context:component-scan
		base-package="org.fkit.controller" />
	<!-- 默认装配方案 -->
	<!-- @MatrixVariable注解功能在SpringMVC中默认是不启用的 -->
	<!-- 启用它需要设置enable-matrix-variables="true" -->
	<mvc:annotation-driven
		enable-matrix-variables="true" />
	<!-- 静态资源处理 -->
	<mvc:default-servlet-handler />

	<!-- 视图解析器 p:prefix属性表示前缀 p:suffix 表示后缀 -->
	<bean id="viewResolver"
		class="org.springframework.web.servlet.view.InternalResourceViewResolver"
		p:prefix="/WEB-INF/content/" p:suffix=".jsp" />

</beans>
```
此外,还需要在`web.xml`文件中配置`Spring MVC`的前端控制器`DispatcherServlet`,因为每次配置基本相同此处不再赘述,读者可自行配置。
部署`VariableTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/VariableTest/
```
此时`Spring MVC`会跳转到`index.jsp`
## 测试 ##
### 测试@PathVariable注解 ###
`VariableController`类的`pathVariableTest`方法用于测试`@PathVariable`注解,它会将请求路径`/pathVariableTest/1"`中`userId`的值"1"赋给方法参数的`userId`变量。单击"`测试@PathVariable注解`"超链接发送请求,将调用`pathVariableTest`方法,此时浏览器显示效果如下:
```
通过@PathVariable获得数据： userId=1
```
### 测试@MatrixVariable注解 ###
`VariableController`类的`matrixVariableTest`方法用于测试`@MatrixVariable`注解,它会将请求路径`"/matrixVariableTest/1;name=jack;age=23"`中的`name`参数的值`"jack"`赋给方法形式参数`name`,将`age`参数的值`23`赋给方法参数的形式参数`age`。单击"`测试@Matrixvariable注解`"超链接发送请求,将调用`matrixVariableTest`方方法.此时浏览器显示的效果如下:
```
通过@PathVariable获得数据： userId=1通过@MatrixVariable获得数据： name=jack age=23
```
可以看到,`< a href=" matrixVariableTest/1;name=jack;age=23">测试MatrixVariable注解</a>`的参数`name`的值`"jack"`被传递到方法形式参数`name`,参数`age`的值"23"被传递到方法的`age`变量,并显示在浏览器上.
### @MatrixVariable注解完成复杂的参数注入 ###
`MatrixVariable`注解还可以完成复杂的参数注入,非常方便地进行`多条件组合查询`。本例以商品查询为例,详细介绍`MatrixVariable`的使用。
`VariableController`类的`productTest`方法用于商品条件查询,传递的参数包括`商品`、`品牌`和`价格区间`,它会将请求路径`"/productTest/computer;brand=apple,acer;low=2000;height=10000"`之中的:
- `brand`参数的值`" apple,acer"`赋给方法参数的`brand`变量,该变量是一个`List`集合;
- 将`low`参数的值`"2000"`赋给方法参数的`low`变量;
- 将`height`参数的值`"10000"`赋给方法参数的`height`变量。

该请求表示一个商品的条件组合查询,商品名称是`computer`,查询的品牌是`apple`和`acer`,价格区间是从`2000`到`10000`

单击"商品条件査询(品牌,价格区间)"超链接发送请求,将调用`product Test`方,浏览器显示结果如下:
```
通过@PathVariable获得数据： goods=computer
通过@MatrixVariable获得数据：brand=[apple, acer]
通过@MatrixVariable获得数据： low=2000 height=10000
```
可以看到,`< a href="productTest/computer;brand=apple,acer;low=2000;height=10000">商品条件查询(品牌,价格区间)</a>`的:
- 参数`brand`的值`" apple,acer"`被传递到方法的`brand`集合变量,
- 参数`low`的值"2000"被传递到方法的`low`变量参数
- 参数`height`的值"10000"被传递到方法的`height`变量,最后输出在浏览器上
<!--SSTStop-->


