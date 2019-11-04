---
title: 示例 @CrossOrigin注解的使用
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.6 @CrossOrigin注解
date: 2019-08-19 16:49:35
updated: 2019-11-02 01:39:00
abbrlink: 559cdc31
---
- [示例 @CrossOrigin注解的使用](/ReadingNotes/559cdc31/#示例-CrossOrigin注解的使用)
    - [总结](/ReadingNotes/559cdc31/#总结)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 @CrossOrigin注解的使用 #
接下来测试跨域发送请求,再新建一个项目`CrossOriginTest`,加入所需的`jar`文件,示例代码如下:
```java
package org.fkit.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;

// 允许所有域发送过来的请求
@CrossOrigin(maxAge = 3600)
@Controller
public class CrossOriginController
{
	// 只允许origins属性中指定的域的请求
	@CrossOrigin(origins = "http://localhost:8080/VariableTest")
	@GetMapping(value = "/welcome")
	public String welcome()
	{
		System.out.println("处理跨域请求");
		return "welcome";
	}
}
```
`CrossOriginController`类和`welcome`方法上都使用了`@CrossOrigin`注解。 `welcome`方法接收到`跨域请求`进行简单处理后,跳转到`welcome.jsp`。
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试@CrossOrigin注解</title>
</head>
<body>
	<br>恭喜您，测试跨域访问成功!
</body>
</html>
```
此外,还需要在`web.xml`文件中配置`Spring MVC`的前端控制器`DispatcherServlet`,因为每次配置基本一致,此处不再赘述,读者可自行配置。
同时部署`VariableTest`和`CrossOriginTest`两个`Web`应用,在浏览器中输入如下`URL`来测试进入`VariableTest`应用:
```
http://localhost:8080/VariableTest/
```
然后`测试@CrossOrigin注解`超链接:
```html
<!-- 跨域请求 -->
<a href="http://localhost:8080/CrossOriginTest/welcome">测试@CrossOrigin注解</a>
```
向另一个`Web`应用`CrossOriginTest`发送跨域请求,`CrossOriginTest`应用的`CrossOriginController`控制器的`welcome`方法将会处理这个跨域请求,控制台输出结果如下:
```
处理跨域请求
```
同时浏览器上将显示`CrossOriginTest`应用的`welcome.jsp`页面。

## 总结 ##
`@CrossOrigin`注解可以接收从另一个`Web`应用发来的跨域请求。
<!--SSTStop-->

