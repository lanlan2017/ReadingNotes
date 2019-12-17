---
title: Spring实战 第4版 内容提要
categories: 
  - Spring实战 (第4版)
date: 2019-07-02 18:37:20
updated: 2019-11-02 10:12:05
abbrlink: 907c6ccc
---
<div id='my_toc'><a href="/ReadingNotes/907c6ccc/#Spring实战-第4版-内容提要" class="header_1">Spring实战 第4版 内容提要</a><br><a href="/ReadingNotes/907c6ccc/#关于本书" class="header_1">关于本书</a><br><a href="/ReadingNotes/907c6ccc/#路线图" class="header_1">路线图</a><br><a href="/ReadingNotes/907c6ccc/#第1部分" class="header_2">第1部分</a><br><a href="/ReadingNotes/907c6ccc/#第2部分" class="header_2">第2部分</a><br><a href="/ReadingNotes/907c6ccc/#第3部分" class="header_2">第3部分</a><br><a href="/ReadingNotes/907c6ccc/#最后部分" class="header_2">最后部分</a><br><a href="/ReadingNotes/907c6ccc/#代码规范与下载" class="header_1">代码规范与下载</a><br></div>
<style>
    .header_1{
        margin-left: 1em;
    }
    .header_2{
        margin-left: 2em;
    }
    .header_3{
        margin-left: 3em;
    }
    .header_4{
        margin-left: 4em;
    }
    .header_5{
        margin-left: 5em;
    }
    .header_6{
        margin-left: 6em;
    }
</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}
var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}
</script>

<!--end-->
# Spring实战 第4版 内容提要 #
本书是经典的、畅销的`Spring`学习和实践指南。
第4版针对`Spring4`进行了全面更新。全书分为4部分。
- 第1部分介绍`Spring`框架的核心知识。
- 第2部分在此基础上介绍了如何使用`Spring`构建`Web`应用程序。
- 第3部分告别前端,介绍了如何在应用程序的后端使用`Spring`。
- 第4部分描述了如何使用`Spring`与其他的应用和服务进行集成。

本书适用于已具有一定`Java`编程基础的读者,以及在`Java`平台下进行各类软件的开发人员、测试人员,尤其适用于企业级`Java`开发人员。本书既可以被刚开始学习`Spring`的读者当作学习指南,也可以被那些想深入了解`Spring`某方面功能的资深用户作为参考用书。

# 关于本书 #
`Spring`框架是以简化`Java EE`应用程序的开发为目标而创建的。同样,本书是为了帮助读者更容易地使用`Spring`而编写的。我的目标不是为读者详细地列出`Spring API`,而是希望通过现实中的实际示例代码来为`Java EE`开发人员展现`Spring`框架。因为`Spring`是一个模块化的框架,所以这本书也是按照这种方式编写的。我们知道并不是所有的开发人员都有相同的需求,有些人想从头学习`Spring`,而有的可能只想排出几个主题,然后按照自己的节奏来学习。所以,本书既可以被刚开始学习`Spring`的读者当作学习指南,也可以被那些想深入了解某方面功能的读者作为参考。
本书适用于所有的`Java`开发人员,企业级`Java`开发人员将会发现更有帮助。我将会循序渐进地指导读者浏览本书中每章复杂的示例代码,但`Spring`的真正强大之处在于它能够使企业级应用程序的开发更简单。因此,企业级应用程序的开发人员会更加欣赏本书的示例代码。因为`Spring`的绝大部分内容都是提供企业级服务的,所以这里包含了许多`Spring`和`EJB`的比较。
# 路线图 #
本书分为4部分。
- 第1部分介绍`Spring`框架的核心知识。
- 第2部分在此基础上介绍如何使用`Spring`构建`Web`应用程序。
- 第3部分告别前端,介绍如何在应用程序的后端使用`Spring`。
- 第4部分描述如何使用`Spring`与其他的应用和服务进行集成。

## 第1部分 ##
在第1部分中,读者将会学习到`Spring`容器、依赖注入(`dependency injection`,`DI`)和面向切面编程(`aspect-oriented programming`,`AOP`),也就是`Spring`框架的核心。这能让读者很好地理解`Spring`的基础原理,而这些原理将会在本书各个章节都会用到。
- 第1章将会概要地介绍`Spring`,包括DI和`AOP`的一些基本样例。同时,读者还会了解到更大的`Spring`生态系统的整体情况。
- 第2章更为详细地介绍DI,展现应用程序中的各个组件(`bean`)如何装配在一起。这包括基于`XML`装配、基于`Java`装配以及自动装配。
- 在掌握了基本的`bean`装配后,第3章会介绍几种高级装配技术,读者可能并不会经常用到这些技术,但是如果用到的话,本章的内容将会告诉读者如何发挥`Spring`容器最强大的威力。
- 第4章介绍如何使用`Spring`的`AOP`来为对象解耦那些对其提供服务的横切性关注点。这一章也为后面各章提供基础,在后面读者将会使用`AOP`来提供声明式服务,如事务、安全和缓存。

## 第2部分 ##
在第2部分中,读者将会看到如何使用`Spring`来构建`Web`应用程序。
- 第5章介绍使用`Spring MVC`的基础知识，这是`Spring`中的基础`Web`框架。读者将会看到如何编写控制器来处理请求，并使用模型数据产生响应。
- 当控制器的工作完成后，模型数据必须要使用一个视图来进行渲染。第6章将会探讨在`Spring`中可以使用的各种视图技术，包括`JSP`、`Apache Tiles`以及`Thymeleaf`。
- 第7章的内容不再是`Spring MVC`的基础知识了，在本章中，读者将会学习到如何自定义`Spring MVC`配置、处理`multipart`类型的文件上传、处理在控制器中可能会出现的异常并且会通过`flash`属性在请求之间传递数据。
- 第8章将会介绍`Spring Web Flow`，这是`Spring MVC`的一个扩展，能够开发会话式的`Web`应用程序。在本章中，读者将会学习到如何构建引导用户完成特定流程的`Web`应用程序。
- 第9章读者将会学到如何使用`Spring Security`为自己的应用程序`Web`层实现安全性。

## 第3部分 ##
第3部分所关注的内容不再是应用程序的前端了,而是关注于如何处理和持久化数据。
- 第10章首先会介绍如何使用`Spring`对`JDBC`的抽象实现关系型数据库中的数据持久化。
- 第11章从另外一个角度介绍数据持久化，也就是使用`Java`持久化`API`（`JPA`）存储关系型数据库中的数据。
- 第12章将会介绍如何将`Spring`与非关系型数据库结合使用，如`MongoDB`和`Neo4j`。
- 不管数据存储在什么地方，缓存都有助于性能的提升，这是通过只有在必要的时候才去查询数据库实现的。第13章将会为读者介绍`Spring`对声明式缓存的支持。
- 第14章重新回到`Spring Security`，将会介绍如何通过`AOP`将安全性应用到方法级别。

## 最后部分 ##
本书的最后一部分会介绍如何将`Spring`应用程序与其他系统进行集成。
- 第15章将会学习如何创建与使用远程服务，包括`RMI`、`Hessian`、`Burlap`以及基于`SOAP`的服务。
- 第16章将会再次回到`Spring MVC`，我们将会看到如何创建`RESTful`服务，在这个过程中所使用的编程模型与之前在第5章中所描述的是一致的。
- 第17章将会探讨`Spring`对异步消息的支持，本章将会包括`Java`消息服务（`Java Message Service`，`JMS`）以及高级消息队列协议（`Advanced Message Queuing Protocol`，`AMQP`）。
- 在第18章中，异步消息有了新的花样，在这一章中读者会看到如何将`Spring`与`WebSocket`和`STOMP`结合起来，实现服务端与客户端之间的异步通信。
- 第19章将会介绍如何使用`Spring`发送`E-mail`。
- 第20章会关注于`Spring`对`Java`管理扩展（`Java Management Extensions`，`JMX`）功能的支持，借助这项功能可以对`Spring`应用程序进行监控和修改运行时配置。
- 最后，在第21章，读者将会看到一个全新并且会改变游戏规则的`Spring`使用方式，名为`Spring Boot`。我们将会看到`Spring Boot`如何将`Spring`应用中样板式的配置移除掉，这样就能让读者更加专注于业务功能。

# 代码规范与下载 #
本书中有大量的示例代码。这些代码将会使用固定宽度的代码字体。本书正文中的类名、方法名或`XML`片段也都使用代码字体。
很多`Spring`类和包的名字很长（不过会有较强的表达性）。鉴于此，我们有时候会用到换行符（➥）。
本书中的示例代码并不都是完整的。为了关注某个主题，我有时候只会展示类的一个或两个方法。本书所构建的应用程序完整代码可以在出版社站点上下载，地址是[https://www.manning.com/books/spring-in-action-fourth-edition](https://www.manning.com/books/spring-in-action-fourth-edition)

