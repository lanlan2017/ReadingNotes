---
title: Serlet JSP和Spring MVC初学指南 前言
categories: 
  - Serlet JSP和Spring MVC初学指南
  - 前言
date: 2019-03-14 20:46:47
updated: 2019-11-02 10:46:35
abbrlink: 7819a34e
---
- [前言](/ReadingNotes/7819a34e/#前言)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
## 前言 ##
`Java Servlet`技术简称`Servlet`技术，是`Java`开发`Web `应用的底层技术。由`Sun`公司于1996年发布，用来代替 `CGI`的一门技术,`CGI`是当时生成`Web`动态内容的主流技术。`CGI`技术的主要问题是每个`Web`请求都需要新启动一个进程来处 理。创建进程会消耗不少`CPU`周期，导致难以编写可扩 展的`CGI`程序。而`Servlet`有着比`CGI`程序更好的性能， 因为`Servlet`在处理第一个请求时被创建后就一直保持 在内存中。此后，`SUN`公司发布了`Java Server Pages`（`JSP`）技术，以进一步简化`servlet`程序开发。 

自从`Servlet`和`JSP`技术诞生后，涌现出大量的基于 `Java`的`Web`框架来帮助开发人员快速编写`Web`应用。这 些框架构建于`Servlet`和`JSP`之上，帮助开发人员更加关 注业务逻辑，无须编写重复性（技术）代码。目前， `Spring MVC`是最为流行的可扩展`Java Web`应用开发框 架。
`Spring MVC`又叫`Spring Web MVC`，是`Spring`框架 的一个模块，用于快速开发`Web`应用。`MVC`代表 `Model-View-Controller`，是一个广泛应用于`GUI`开发的 设计模式。该模式不局限于`Web`开发，也广泛应用在桌 面开发技术上，如`Java Swing`和`JavaFX`。 下面将简要介绍`HTTP`、基于`Servlet`和`JSP`的`Web`编 程，以及本书的章节内容编排。

**注意**
本书中所有示例代码基于`Servlet 3.0`、`JSP 2.3`以及`Spring MVC 4`。 本书假定读者已有`Java`以及面向对象编程基础。对于`Java`新手，我们建 议阅读由`Budi Kurniawan`编写的《`Java : A Beginner's Tutorial (Fourth Edition)》(ISBN 9780992133047)`一书。




