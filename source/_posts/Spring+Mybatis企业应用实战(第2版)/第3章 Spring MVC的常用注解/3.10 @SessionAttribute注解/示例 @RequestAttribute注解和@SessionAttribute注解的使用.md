---
title: 示例 @RequestAttribute注解和@SessionAttribute注解的使用
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.10 @SessionAttribute注解
date: 2019-08-19 19:42:55
updated: 2019-11-02 01:39:00
abbrlink: 6d3c96b0
---
- [示例 @RequestAttribute注解和@SessionAttribute注解的使用](/ReadingNotes/6d3c96b0/#示例-RequestAttribute注解和-SessionAttribute注解的使用)
    - [index.jsp](/ReadingNotes/6d3c96b0/#index-jsp)
    - [AttributeController.java](/ReadingNotes/6d3c96b0/#AttributeController-java)
    - [TestAttributeFilter.java](/ReadingNotes/6d3c96b0/#TestAttributeFilter-java)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 @RequestAttribute注解和@SessionAttribute注解的使用 #
新建一个项目`AttributeTest`,加入所需的`jar`文件,示例代码如下:
## index.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>@RequestAttribute和@SessionAttribute测试</title>
</head>
<body>
	<h2>@RequestAttribute和@SessionAttribute测试</h2>
	<a href="attrbuteTest">测试@RequestAttribute和@SessionAttribute</a>
	<br>
</body>
</html>
```
## AttributeController.java ##
```java
package org.fkit.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.SessionAttribute;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class AttributeController
{
	// 测试@CookieValue注解
	// 该方法映射的请求为 /cookieValueTest
	@GetMapping(value = "/attrbuteTest")
	public ModelAndView attrbuteTest(ModelAndView mv)
	{
		System.out.println("attributeTest方法被调用...");
		// 客户端重定向到main请求，会被自定义过滤器拦截
		mv.setViewName("redirect:main");
		return mv;
	}
	/*
	 * 该方法映射的请求为/main
	 * @RequestAttribute("name") String
	 * name会获取request作用范围中名为"name"的属性的值赋给方法的参数name
	 * @SessionAttribute("sex") String sex会获取session作用范围中名为"sex"的属性的值赋给方法的参数sex
	 */
	@RequestMapping("/main")
	public String main(@RequestAttribute("name") String name,
			@SessionAttribute("sex") String sex)
	{
		System.out.println("main方法被调用...");
		// 输出@RequestAttribute获得的name
		System.out.println("name: " + name);
		// 输出@SessionAttribute获得的sex
		System.out.println("sex: " + sex);
		return "welcome";
	}
}
```
`attributeTest`方法处理请求后重定向到`main`请求,`main`请求会被自定义过滤器拦截,在过滤器中会分别设置两个属性到`request`作用域和`session`作用域。在`main`方法中使用`@RequestAttribute`和`@SessionAttribute`进行赋值。
## TestAttributeFilter.java ##
```java
package org.fkit.filter;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;
import javax.servlet.http.HttpServletRequest;

// 过滤器拦截/main请求
@WebFilter(value = "/main")
public class TestAttributeFilter implements Filter
{
	@Override
	public void destroy()
	{
	}
	@Override
	public void doFilter(ServletRequest request, ServletResponse response,
			FilterChain chain) throws IOException, ServletException
	{
		System.out.println("进入AuthFilter过滤器的doFilter方法");
		// 将ServletRequest对象强转成HttpServletRequest对象
		HttpServletRequest httpRequest = (HttpServletRequest) request;
		// 在request作用范围域中设置一个name属性
		httpRequest.setAttribute("name", "小明");
		// 在session作用范围域中设置一个sex属性
		httpRequest.getSession().setAttribute("sex", "男");
		// 如果还有过滤器执行过滤器，否则进入请求处理方法
		chain.doFilter(httpRequest, response);
	}
	@Override
	public void init(FilterConfig arg0) throws ServletException
	{
	}
}
```
`TestAttributeFilter`过滤器拦截`"main"`请求,在`dofilter`方法中分别设置两个属性到`request`作用域和`session`作用域。
部署`AttributeTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/AttributeTest/
```
单击测试`@RequestAttribute和@SessionAttribute"`超链接发送请求,将调用`attrbuteTest`方法,然后经过过滤器,重定向到`main`方法,控制台输出结果如下:
```
attributeTest方法被调用...
进入AuthFilter过滤器的doFilter方法
main方法被调用...
name: 小明
sex: 男
```
浏览器显示内容:
```
name:小明
sex:男 
```
可以看到, `request`作用域中的`name`的值被传递到请求处理方法`main`的`name`变量, `session`作用域中的`sex`的值被传递到请求处理方法`main`的`sex`变量,并输出打印在控制台。
<!--SSTStop-->

