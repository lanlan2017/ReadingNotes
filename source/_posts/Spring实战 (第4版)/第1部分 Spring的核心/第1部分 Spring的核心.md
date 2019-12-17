---
title: 第1部分 Spring的核心
categories: 
  - Spring实战 (第4版)
  - 第1部分 Spring的核心
date: 2019-07-02 19:36:57
updated: 2019-12-17 01:44:33
abbrlink: 2967a704
---
<div id='my_toc'><a href="/ReadingNotes/2967a704/#第1部分-Spring的核心" class="header_1">第1部分 Spring的核心</a><br></div>
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
# 第1部分 Spring的核心 #
`Spring`可以做很多事情，它为企业级开发提供给了丰富的功能，但是这些功能的底层都依赖于它的两个核心特性，也就是依赖注入（`dependency injection`，`DI`）和面向切面编程（`aspect-oriented programming`，`AOP`）。

- 在第1章“`Spring`之旅”中，我将快速介绍一下`Spring`框架，包括`Spring DI`和`AOP`的概况，以及它们是如何帮助读者解耦应用组件的。
- 在第2章“装配`Bean`”中，我们将深入探讨如何将应用中的各个组件拼装在一起，读者将会看到`Spring`所提供的自动配置、基于`Java`的配置以及`XML`配置。
- 在第3章“高级装配”中，将会告别基础的内容，为读者展现一些最大化`Spring`威力的技巧和技术，包括条件化装配、处理自动装配时的歧义性、作用域以及`Spring`表达式语言。
- 在第4章“面向切面的`Spring`”中，展示如何使用`Spring`的`AOP`特性把系统级的服务（例如安全和审计）从它们所服务的对象中解耦出来。本章也为后面的第9章、第13章和第14章做了铺垫，这几章将会分别介绍如何将`Spring AOP`用于声明式安全以及缓存。

