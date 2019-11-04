---
title: 第8章 深入使用Spring
categories: 
  - 轻量级Java EE企业应用实战(第5版)
  - 第8章 深入使用Spring
  - 8.0 本章要点
date: 2019-08-31 09:55:21
updated: 2019-11-02 01:39:03
abbrlink: 4676c7d7
---
- [第8章 深入使用Spring](/ReadingNotes/4676c7d7/#第8章-深入使用Spring)
    - [本章要点](/ReadingNotes/4676c7d7/#本章要点)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 第8章 深入使用Spring #
## 本章要点 ##
- 利用`后处理器`扩展`Spring`容器
- `Bean`后处理器和容器后处理器
- `Spring`的"零配置"支持
- `Spring`的资源访问策略
- 在`ApplicationContext`中使用资源
- `AOP`的基本概念
- `AspectJ`使用入门
- 生成`AOP`代理和`AOP`代理的作用
- 基于注解的"零配置"方式
- 基于`XML`配置文件的管理方式
- `Spring`的事务策略
- `Spring`的事务配置
- `Spring`整合`MVC`框架的策略
- `Spring`整合`Struts2`
- `Spring`整合`Hibernate`
- `Spring`整合`JPA`

上一章已经介绍了`Spring`框架的基础内容,详细介绍了**`Spring`容器的核心机制:依赖注入**,并介绍了`Spring`容器对`Bean`的管理。实际上,上一章介绍的内容是大部分项目都需要使用的基础部分,很多时候,即使不使用`Spring`框架,实际项目也都会采用相同的策略。
但`Spring`框架的功能绝不是只有这些部分, `Spring`框架允许开发者使用两种后处理器扩展`loC`容器,这两种后处理器可以后处理`IoC`容器本身,或者对容器中所有的`Bean`进行后处理。`loC`容器还提供了`AOP`功能,极好地丰富了`Spring`容器的功能。
`Spring AOP`是`Spring`框架另一个吸引人的地方,`AOP`本身是一种非常前沿的编程思想,它从动态角度考虑程序运行过程,专门用于处理系统中分布于各个模块(不同方法)中的交叉关注点的问题,能更好地抽离出各模块的交叉关注点。
`Spring`的声明式事务管理正是通过`AOP`来实现的。当然,如果仅仅想使用`Spring`的声明式事务管理,其实完全无须掌握`AOP`,但如果希望开发出结构更优雅的应用,例如集中处理应用的权限控制、系统日志等需求,则应该使用`AOP`来处理。
除此之外,本章还将详细介绍`Spring`与`Hibernate/JPA`和`Struts2`框架的整合。

<!--SSTStop-->

