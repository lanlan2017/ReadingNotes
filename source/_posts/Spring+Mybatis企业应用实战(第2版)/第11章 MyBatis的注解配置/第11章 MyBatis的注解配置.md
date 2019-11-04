---
title: 第11章 MyBatis的注解配置
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第11章 MyBatis的注解配置
date: 2019-06-13 18:29:24
updated: 2019-11-02 01:38:59
abbrlink: 408525dd
---
- [第11章 MyBatis的注解配置](/ReadingNotes/408525dd/#第11章-MyBatis的注解配置)
    - [本章要点](/ReadingNotes/408525dd/#本章要点)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
# 第11章 MyBatis的注解配置 #
## 本章要点 ##
- `MyBatis`注解插入、修改、删除和査询操作.
- `MyBatis`注解一对对多和多对多操作.
- `MyBatis`注解动态`SQL`.
- `MyBatis`注解调用存储过程.
- `MyBatis`注解使用二级缓存.
前面的章节介绍了`MyBatis`的基本用法、关联映射、动态`SQL`和缓存机制等知识,其所有的配置都使用`XML`完成,但是大量的`XML`配置文件的编写是非常烦琐的,因此`MyBatis`也提供了更加简便的基于注解(`annotation`)的配置方式。本章将重点介绍`MyBatis`的注解配置.

