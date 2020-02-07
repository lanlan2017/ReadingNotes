---
title: 第1章 快速搭建Spring Web应用
categories: 
  - 精通Spring MVC4
  - 第1章 快速搭建Spring Web应用
date: 2019-08-11 01:00:04
updated: 2019-12-17 02:00:56
abbrlink: dbeeb1cb
---
<div id='my_toc'><a href="/ReadingNotes/dbeeb1cb/#第1章快速搭建Spring-Web应用" class="header_1">第1章快速搭建Spring Web应用</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第1章快速搭建Spring Web应用 #
在本章中,我们将会直接接触代码并搭建一个`Web`应用,本书的其他章节将会基于该应用进行讲解。
在这里,我们将会使用`Spring Boot`的自动配置功能来构建应用,这样的话,就能完全避免使用样板式的配置文件。
本书将会从整体上介绍`Spring Boot`是如何运行的以及该如何对其进行配置,共有4种方式来开启一个`Spring`项目:
- 使用`Spring Tool Suite`生成`Starter`代码； 
- 使用`IntelliJ IDEA 14.1`，它对`Spring Boot`提供了良好的支持； 
- 借助`Spring`站点，从 `http://start.Spring.io`上下载可配置的`ZIP` 文件； 
- 使用到`http://start.Spring.io` 站点的`curl`命令来达到相同的效果。 

本书中将会使用`Gradle` 和`Java 8`,但是也不必为此感到担心。如果你还在使用`Maven`和更早版本的`Java`的话,相信你会发现这些技术也是很易于使用的。
很多官方的`Spring` 教程同时提供了`Gradle` 构建和`Maven` 构建,因此,如果你决定继续使用`Maven`的话,也能很容易地找到样例。`Spring 4`完全兼容`Java 8`,**如果你不采用`Lambda`表达式来简化代码库的话,那真的是很遗憾的事情**。
本书同时还会为你展示一些`Git` 命令。笔者认为,跟踪工作进展并在稳定的状态进行提交是一件好事。另外,这样还能很容易地将你的工作成果与本书提供的源码进行对比。
本书第9章将借助`Heroku`部署我们的应用,建议从一开始就使用`Git`对代码进行版本管理。在本章中,关于如何开始使用`Git`,我会给出一些建议。


