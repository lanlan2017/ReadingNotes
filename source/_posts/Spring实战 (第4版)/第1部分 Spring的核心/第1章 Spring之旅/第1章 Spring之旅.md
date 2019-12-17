---
title: 第1章 Spring之旅
categories: 
  - Spring实战 (第4版)
  - 第1部分 Spring的核心
  - 第1章 Spring之旅
date: 2019-07-02 19:42:18
updated: 2019-12-17 01:44:33
abbrlink: 420ee57d
---
<div id='my_toc'><a href="/ReadingNotes/420ee57d/#第1章-Spring之旅" class="header_1">第1章 Spring之旅</a><br></div>
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
# 第1章 Spring之旅 #
本章内容：
- `Spring`的`bean`容器
- 介绍`Spring`的核心模块
- 更为强大的`Spring`生态系统
- `Spring`的新功能

对于`Java`程序员来说，这是一个很好的时代。
在`Java`近20年的历史中，它经历过很好的时代，也经历过饱受诟病的时代。尽管有很多粗糙的地方,如`applet`、企业级`JavaBean`(`Enterprise JavaBean`,`EJB`)、`Java`数据对象(`Java Data Object`,`JDO`)以及无数的日志框架,但是作为一个平台,`Java`的历史是丰富多彩的,有很多的企业级软件都是基于这个平台构建的。`Spring`是`Java`历史中很重要的组成部分。
在诞生之初,创建`Spring`的主要目的是用来替代更加重量级的企业级`Java`技术,尤其是`EJB`。相对于`EJB`来说,`Spring`提供了更加轻量级和简单的编程模型。它增强了简单老式`Java`对象(`Plain Old Java object`,`POJO`)的功能,使其具备了之前只有`EJB`和其他企业级`Java`规范才具有的功能。随着时间的推移,`EJB`以及`Java 2`企业版(`Java 2 Enterprise Edition`,J2EE)在不断演化。`EJB`自身也提供了面向简单`POJO`的编程模型。现在,`EJB`也采用了依赖注入(`Dependency Injection`,DI)和面向切面编程(`Aspect-Oriented Programming`,`AOP`)的理念,这毫无疑问是受到`Spring`成功的启发。
尽管`J2EE`(现在称之为`JEE`)能够赶上`Spring`的步伐,但`Spring`也没有停止前进。`Spring`继续在其他领域发展,而`JEE`则刚刚开始涉及这些领域,或者还完全没有开始在这些领域的创新。移动开发、社交`API`集成、`NoSQL`数据库、云计算以及大数据都是`Spring`正在涉足和创新的领域。`Spring`的前景依然会很美好。正如我之前所言,对于`Java`开发者来说,这是一个很好的时代。
本书会对`Spring`进行研究,在这一章中,我们将会在较为宏观的层面上介绍`Spring`,让你对`Spring`是什么有直观的体验。本章将让读者对`Spring`所解决的各类问题有一个清晰的认识,同时为其他章奠定基础。

