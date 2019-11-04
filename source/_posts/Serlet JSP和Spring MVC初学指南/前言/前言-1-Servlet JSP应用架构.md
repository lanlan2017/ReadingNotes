---
title: 前言-1-Servlet JSP应用架构
categories: 
  - Serlet JSP和Spring MVC初学指南
  - 前言
date: 2019-04-25 14:51:26
updated: 2019-11-02 10:12:45
abbrlink: 17e72ee2
---
- [前言 1Servlet/JSP应用架构](/ReadingNotes/17e72ee2/#前言-1Servlet-JSP应用架构)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
## 前言 1Servlet/JSP应用架构 ##
`Servlet`是一个`Java`程序，一个`Servlet`应用有一个或多个`Servlet`程序。`JSP`页面会被转换和编译成`Servlet`程序。
`Servlet`应用无法独立运行，必须运行在`Servlet`容器中。`Servlet`容器将用户的请求传递给`Servlet`应用，并将`Servlet`应用生成的结果返回给用户。由于大部分`Servlet`应用都包含多个 `JSP`页面，因此更准确地说是“`Servlet/JSP`应用”。
`Web`用户通过`Web`浏览器例如`IE`、`Mozilla Firefox `或者谷歌`Chrome`来访问`Servlet`应用。通常，`Web`浏览器又叫`Web`客户端。
**`Web`服务器和`Web`客户端间通过`HTTP`协议通信**， 因此**`Web`服务器也叫`HTTP`服务器**。下面会详细讨论 `HTTP`协议。

**`Servlet/JSP`容器是一个可以同时处理`Servlet`和静态内容的`Web`容器**。过去，由于通常认为`HTTP`服务器比 `Servlet/JSP`容器更加可靠，因此人们习惯将`Servlet/JSP `容器作为`HTTP`服务器如`Apache HTTP`服务器的一个模块。这种模式下，`HTTP`服务器用来处理静态资源，而 `Servlet/JSP`容器则负责生成动态内容。如今， `Servlet/JSP`容器更加成熟可靠，并被广泛地独立部署。 `Apache Tomcat`和`Jetty`是当前最流行的`Servlet/JSP`容器， 并且它们是免费而且开源的。你可以访问 [http://tomcat.apache.org](http://tomcat.apache.org) 以及[http://www.eclipse.org/jetty](http://www.eclipse.org/jetty) 下载。
**`Servlet`和`JSP`只是`Java`企业版中众多技术中的两个**，其他`Java EE`技术还有`Java`消息服务，企业`Java`对象、`JavaServer Faces`以及`Java`持久化等，完整的`Java EE `技术列表可以访问如下地址：
[http://www.oracle.com/technetwork/java/javaee/tech/index.html](http://www.oracle.com/technetwork/java/javaee/tech/index.html) 
**要运行`Java EE`应用，需要一个`Java EE`容器**，例如 `GlassFish`、`JBoss`、`Oracle Weblogic`或者`IBM WebSphere`。诚然，我们可以将一个`Servlet/JSP`应用部署到一个`Java EE`容器上，但一个`Servlet/JSP`容器就已经满足需要了，并且更加轻量。当然，`Tomcat`和`Jetty`不是 `Java EE`容器，因此无法运行`EJB`或`JMS`技术。

