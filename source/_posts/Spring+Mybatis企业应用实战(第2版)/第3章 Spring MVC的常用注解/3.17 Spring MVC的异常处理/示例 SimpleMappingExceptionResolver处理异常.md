---
title: 示例 SimpleMappingExceptionResolver处理异常
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.17 Spring MVC的异常处理
date: 2019-08-21 12:21:58
updated: 2019-11-02 01:39:00
abbrlink: 463618c5
---
- [示例 SimpleMappingExceptionResolver处理异常](/ReadingNotes/463618c5/#示例-SimpleMappingExceptionResolver处理异常)
    - [index.jsp](/ReadingNotes/463618c5/#index-jsp)
    - [TestController.java](/ReadingNotes/463618c5/#TestController-java)
    - [error.jsp](/ReadingNotes/463618c5/#error-jsp)
    - [sqlerror.jsp](/ReadingNotes/463618c5/#sqlerror-jsp)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 SimpleMappingExceptionResolver处理异常 #
新建一个项目`SimpleMappingExceptionResolverTest`,加入所需的`jar`文件,示例代码如下:
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
    <br>
    <a href="hello">没有异常处理</a>
    <br>
    <a href="test">使用简单异常处理器处理异常</a>
    <br>
    <a href="find">使用简单异常处理器处理特定异常</a>
    <br>
</body>
</html>
```
`index.jsp`中有3个超链接,分别测试`没有异常处理`、`有异常处理`、`特定异常处理`3种情况。
## TestController.java ##
```java
package org.fkit.controller;

import java.sql.SQLException;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class TestController
{
	@GetMapping("/hello")
	public String hello() throws Exception
	{
		// 抛出异常
		throw new Exception();
	}
	@GetMapping("/test")
	public String test() throws Exception
	{
		// 模拟异常
		@SuppressWarnings("unused")
		int i = 5 / 0;
		return "success";
	}
	@GetMapping("/find")
	public String find() throws Exception
	{
		try
		{
			// 模拟异常
			@SuppressWarnings("unused")
			int i = 5 / 0;
			return "success";
		} catch (Exception e)
		{
			throw new SQLException("查找数据失败!");
		}

	}
}
```
`TestController`中有3个方法,分别对应`index.jsp`页面的3个请求:
1. `hello`方法什么都没做,直接抛出一个异常。
2. `test`方法模拟了一个除数不能为0异常。
3. `find`方法模拟了一个除数不能为0异常之后,在`catch`块中抛出了一个`SQLException`异常。

部署`SimpleMappingExceptionResolverTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/SimpleMappingExceptionResolverTest/
```
单击"`没有异常处理`"超链接,发送`"hello"`请求,此时没有异常处理程序,异常被直接抛给了浏览器.
异常被直接抛到浏览器,页面上显示一大堆错误堆栈信息,用户看到这些错误堆栈信息,往往都会一头雾水,抱怨这个设计实在太不友好。而且错误堆栈信息由于暴露了后台方法的调用关系,对应用来说这是存在一定潜在风险的。虽然在`web.xml`中可以配置处理异常的`jsp`页面,但这还是远远不够的。 `Spring MVC`对错误处理提供了更好的解决方案
接下来,在`springmvc-config.xml`中加入异常处理的配置。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
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

    <!-- p:defaultErrorView="error"表示所有没有指定的异常都跳转到异常处理页面error, -->
    <!-- p:exceptionAttribute="ex"表示在异常处理页面中可以访问的异常对象变量名是ex。 -->
    <bean
        class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver"
        p:defaultErrorView="error" p:exceptionAttribute="ex">

        <!-- 异常映射 exceptionMappings表示映射的异常， -->
        <!-- 接受参数是一个Properties key是异常类名，value是处理异常的页面 -->
        <property name="exceptionMappings">
            <props>
                <prop key="IOException">ioerror</prop>
                <prop key="SQLException">sqlerror</prop>
            </props>
        </property>
    </bean>

</beans>
```
<!--replace:ex=E X-->
重点是异常处理的配置。 `SimpleMappingExceptionResolver`是`Spring`提供的处理异常的类,所有抛岀的异常都会被该类捕获。
- `p:defaultErrorView="error"`属性表示所有没有指定的异常都跳转到异常处理页面`error`。
- `p:exceptionAttribute="ex"`属性表示在异常处理页面中可以访问的异常对象变量名是`ex`。
- 如果需要为一些特定的异常指定异常处理页面,可以使用`exceptionMappings`属性,该属性接受的参数是一个`Properties`对象,:
    - `key`是异常类名或者包名加类名,
    - `value`是异常处理页面。

<!--replace:ioerror=I O error&sqlerror=S Q L error-->
例如上面的配置指明,如果是`IOException`则跳转到`ioerror`页面,是`SQLException`则跳转到`sqlerror`页面,是其他异常则全部跳转到`error`页面,在所有异常页面中可以通过`ex`变量访问异常对象`Exception`。
## error.jsp ##
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
    <h3>异常处理页面</h3>
    抛出异常信息：${requestScope.ex.message}
</body>
</html>
```
## sqlerror.jsp ##
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
    <h3>特定异常处理页面</h3>
    抛出异常信息：${requestScope.ex.message}
</body>
</html>
```
再次运行`SimpleMappingExceptionResolverTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用：
```
http://localhost:8080/SimpleMappingExceptionResolverTest/
```
单击"`使用简单异常处理器处理异常`"超链接,发送`"test"`请求抛出的异常被`SimpleMappingExceptionResolver`捕获,转发到异常处理页面`error.jsp`
单击"`使用简单异常处理器处理特定异常`"超链接,发送`"find"`请求,请求处理方法抛出的是`SQLException`异常,被`SimpleMappingExceptionResolver`捕获,转发到异常处理页面`sqlerror.jsp`。
<!--SSTStop-->

