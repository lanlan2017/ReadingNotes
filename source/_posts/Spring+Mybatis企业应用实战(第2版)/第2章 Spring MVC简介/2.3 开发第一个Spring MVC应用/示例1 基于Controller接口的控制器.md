---
title: 示例1 基于Controller接口的控制器
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第2章 Spring MVC简介
  - 2.3 开发第一个Spring MVC应用
date: 2019-08-16 22:39:26
updated: 2019-11-02 01:39:00
abbrlink: 3447f8a3
---
- [示例1:基于Controller接口的控制器](/ReadingNotes/3447f8a3/#示例1-基于Controller接口的控制器)
    - [1.增加Spring的支持](/ReadingNotes/3447f8a3/#1-增加Spring的支持)
        - [复制Spring的jar包到项目lib目录](/ReadingNotes/3447f8a3/#复制Spring的jar包到项目lib目录)
        - [复制commons-logging的jar包到项目lib目录](/ReadingNotes/3447f8a3/#复制commons-logging的jar包到项目lib目录)
    - [2. 配置前端控制器DispatcherServlet](/ReadingNotes/3447f8a3/#2-配置前端控制器DispatcherServlet)
    - [3 配置Spring MVC的Controller](/ReadingNotes/3447f8a3/#3-配置Spring-MVC的Controller)
    - [4. Controller类的实现](/ReadingNotes/3447f8a3/#4-Controller类的实现)
    - [5. View页面](/ReadingNotes/3447f8a3/#5-View页面)
    - [6.测试应用](/ReadingNotes/3447f8a3/#6-测试应用)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例1:基于Controller接口的控制器 #
## 1.增加Spring的支持 ##
首先,使用`Eclipse`新建一个`Dynamic Web Pro ject`,也就是新建一个动态`Web`项目,命名为`SpringMVCTest`。
### 复制Spring的jar包到项目lib目录 ###
为了让`Web`应用具有`Spring`支持的功能,将`spring-framework-5.0.1.RELEASE`解压文件夹下的`libs`文件夹下所有`Spring`框架的`class`文件的`jar`包和`Spring`所依赖的`commons- logging-1.2.jar`复制到`Web`应用的`lib`文件夹下,也就是`SpringMVCTest\WebContent\WEB-INF`路径下.
可以在`libs`目录下打开`cmd`,使用如下`copy`命令复制即可:
```cmd
copy *.RELEASE.jar E:\workspace_shizhan\SpringMVCTest\WebContent\WEB-INF\lib
```
复制效果:
```cmd
G:\Desktop\随书源码\库文件\spring-framework-5.0.1.RELEASE\libs>copy *.RELEASE.jar E:\workspace_shizhan\SpringMVCTest\WebContent\WEB-INF\lib
spring-aop-5.0.1.RELEASE.jar
spring-aspects-5.0.1.RELEASE.jar
spring-beans-5.0.1.RELEASE.jar
spring-context-5.0.1.RELEASE.jar
spring-context-indexer-5.0.1.RELEASE.jar
spring-context-support-5.0.1.RELEASE.jar
spring-core-5.0.1.RELEASE.jar
spring-expression-5.0.1.RELEASE.jar
spring-instrument-5.0.1.RELEASE.jar
spring-jcl-5.0.1.RELEASE.jar
spring-jdbc-5.0.1.RELEASE.jar
spring-jms-5.0.1.RELEASE.jar
spring-messaging-5.0.1.RELEASE.jar
spring-orm-5.0.1.RELEASE.jar
spring-oxm-5.0.1.RELEASE.jar
spring-test-5.0.1.RELEASE.jar
spring-tx-5.0.1.RELEASE.jar
spring-web-5.0.1.RELEASE.jar
spring-webflux-5.0.1.RELEASE.jar
spring-webmvc-5.0.1.RELEASE.jar
spring-websocket-5.0.1.RELEASE.jar
已复制        21 个文件。
```
### 复制commons-logging的jar包到项目lib目录 ###
下载`commons-logging-1.2`然后进入解压后的目录,输入如下`copy`命令来复制`commons-logging-1.2.jar`到项目路径中.
```cmd
G:\Desktop\随书源码\库文件\commons-logging-1.2>copy *1.2.jar E:\workspace_shizhan\SpringMVCTest\WebContent\WEB-INF\lib
commons-logging-1.2.jar
已复制         1 个文件。
```
此时`libs`目录下的文件如下所示:
```cmd
E:\workspace_shizhan\SpringMVCTest\WebContent\WEB-INF\lib
├─commons-logging-1.2.jar
├─spring-aop-5.0.1.RELEASE.jar
├─spring-aspects-5.0.1.RELEASE.jar
├─spring-beans-5.0.1.RELEASE.jar
├─spring-context-5.0.1.RELEASE.jar
├─spring-context-indexer-5.0.1.RELEASE.jar
├─spring-context-support-5.0.1.RELEASE.jar
├─spring-core-5.0.1.RELEASE.jar
├─spring-expression-5.0.1.RELEASE.jar
├─spring-instrument-5.0.1.RELEASE.jar
├─spring-jcl-5.0.1.RELEASE.jar
├─spring-jdbc-5.0.1.RELEASE.jar
├─spring-jms-5.0.1.RELEASE.jar
├─spring-messaging-5.0.1.RELEASE.jar
├─spring-orm-5.0.1.RELEASE.jar
├─spring-oxm-5.0.1.RELEASE.jar
├─spring-test-5.0.1.RELEASE.jar
├─spring-tx-5.0.1.RELEASE.jar
├─spring-web-5.0.1.RELEASE.jar
├─spring-webflux-5.0.1.RELEASE.jar
├─spring-webmvc-5.0.1.RELEASE.jar
└─spring-websocket-5.0.1.RELEASE.jar
```
这样该`Web`应用已经加入了`Spring`的必需类库。但还需要修改`web.xml`文件,让该文件负责加载`Spring`框架。
## 2. 配置前端控制器DispatcherServlet ##
进入`WebContent\WEB-INF`目录,打开`web.xml`文件,如果没有`web.xml`文件,可以在项目上右键,选择`Java EE Tools`,然后选择`Generate Deployment Descriptor Stub`即可生成`web.xml`文件.
在人在该文件中配置`Spring MVC`的前端控制器`DispatcherServlet`,如下所示:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xmlns="http://xmlns.jcp.org/xml/ns/javaee" 
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
	http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" 
	id="WebApp_ID" version="3.1">
	<!-- 定义Spring MVC的前端控制器 -->
    <servlet>
        <!-- 默认去应用程序文件夹下的`WEB-INF`文件夹下査找对应的`springmvc-servlet.xml`作为配置文件 -->
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!-- Spring MVC配置文件的路径 -->
            <param-value>/WEB-INF/springmvc-config.xml</param-value>
        </init-param>
        <!-- 在启动时立即加载 -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <!-- 让Spring MVC的前端控制器拦截所有请求 -->
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```
`web.xml`文件的内容告诉`Web`容器,将使用`Spring MVC`的`DispatcherServlet`,并通过配置`url-pattern`元素的值为`"/"`,将所有的`URL`都映射到该`Servlet`。
## 3 配置Spring MVC的Controller ##
接下来是`Spring MVC`的配置文件,配置信息如下:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
       
    <!-- 配置Handle，映射"/hello"请求 -->
    <bean name="/hello" class="org.fkit.controller.HelloController"/>

	<!-- 处理映射器将bean的name作为url进行查找，需要在配置Handle时指定name（即url） -->
	<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>

	<!-- SimpleControllerHandlerAdapter是一个处理器适配器，所有处理适配器都要实现 HandlerAdapter接口-->
	<bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
	
	<!-- 视图解析器 -->
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"/>
</beans>
```
`springmvc-config.xml`文件声明了`HelloController`业务控制器类,并将其映射到`/hello`请求。
此处还配置了一个**处理器映射器**`BeanNameUrlHandlerMapping`,这样可以`Bean`的名称为`URL`进行查找;同时配置了**处理器适配器**`SimpleControllerHandlerAdapter`,来完成对`HelloController`类的`handleRequest`方法的调用;最后配置了视图解析器`InternalResourceViewResolver`来解析视图,将`View`呈现给用户。需要注意的是,在`Spring4.0`之后,如果不配置处理器映射器、处理器适配器和视图解析器,也会使用默认的完成`Spring`内部`MVC`工作,笔者在此处显示配置处理过程,是希望读者能够了解`Spring MVC`的每一个动作,之后可以更好地理解`Spring MVC`的工作流程。
## 4. Controller类的实现 ##
`HelloController`类实现了`Controller`接口,用来处理`/hello`请求。示例代码如下:
```java
package org.fkit.controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;

/**
 * HelloController是一个实现Controller接口的控制器, 可以处理一个单一的请求动作
 */
public class HelloController implements Controller
{
	/**
	 * handleRequest是Controller接口必须实现的方法。
	 * 该方法的参数是对应请求的HttpServletRequest和对应响应的HttpServletResponse。
	 * 该方法必须返回一个包含视图路径或视图路径和模型的ModelAndView对象。
	 */
	@Override
	public ModelAndView handleRequest(HttpServletRequest request,
			HttpServletResponse response) throws Exception
	{
		System.out.println("handleRequest 被调用");
		// 创建准备返回的ModelAndView对象，该对象通常包含了返回视图的路径、模型的名称以及模型对象
		ModelAndView mv = new ModelAndView();
		// 添加模型数据 可以是任意的POJO对象
		mv.addObject("message", "Hello World!");
		// 设置逻辑视图名，视图解析器会根据该名字解析到具体的视图页面
		mv.setViewName("/WEB-INF/content/welcome.jsp");
		// 返回ModelAndView对象。
		return mv;
	}
}
```
`HelloController`是一个实现`Controller`接口的控制器,它可以处理一个单的请求动作。 `handleRequest`是`Controller`接口必须实现的方法, `Controller`调用该方法来处理请求。该方法的参数是对应请求的`HttpServletRequest`和`HttpServletResponse`,该方法必须返回一个包含视图名或视图名和模型的`ModelAndView`对象。本例返回的模型中包含了一个名为`message`的字符串对象,返回的视图路径为`/WEB-INF/content/welcome.jsp`,因此,请求将被转发到`welcome.jsp`页面。
**提示:**`Spring MVC`建议把所有的视图页面存放在`WEB-INF`文件夹下,这样可以保护视图页面,避免直接向视图页面发送请求。上面的`HelloController`类的`handleRequest`方法处理完请求后, `Spring MVC`会调用`/WEB-INF/content/`文件夹下的`welcome.jsp`呈现视图.
## 5. View页面 ##
`SpringMVCTest`包含一个视图页面`welcome.jsp`,用来显示欢迎信息。

此处的`JSP`页面使用了`EL`表达式来简化页面开发,关于`EL`表达式的使用可参考附录A `EL`表达式和`JSTL`标签库"的内容
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>欢迎页面</title>
</head>
<body>
	<!-- 页面可以访问Controller传递传递出来的message -->
	${requestScope.message}
</body>
</html>
```
## 6.测试应用 ##
使用`Eclipse`部署`SpringMVCTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用,
```
http://localhost:8080/SpringMVCTest/hello
```
浏览器上将会显示`Hello World!`这个字符串,这表示`Spring MVC`访问成功。

提示:使用`MVC`框架就应该严格遵守MVC思想。MC框架不赞成浏览器直接访问`Web`应用的视图页面,用户的所有请求都只应向控制器发送,由控制器调用模型组件、视图组件向用户呈现数据.
<!--SSTStop-->

