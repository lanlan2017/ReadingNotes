---
title: 第5章 Hibernate的基本用法
categories: 
  - 轻量级Java EE企业应用实战(第5版)
  - 第5章 Hibernate的基本用法
  - 5.0 前言
date: 2019-08-09 22:56:57
updated: 2019-11-02 01:39:03
abbrlink: ecadf082
---
- [第5章 Hibernate的基本用法](/ReadingNotes/ecadf082/#第5章-Hibernate的基本用法)
    - [本章要点](/ReadingNotes/ecadf082/#本章要点)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 第5章 Hibernate的基本用法 #
## 本章要点 ##
- `ORM`的基本知识
- `ORM`和 `Hibernate`的关系
- `Hibernate`的基本映射思想
- `Hibernate`入门知识
- 使用 `Eclipse`开发 `Hibernate`应用
- `Hibernate`的体系和核心`API`
- `Hibernate`的配置文件
- 持久化类的基本要求
- 持久化对象的状态
- `Hibernate`的基本映射
- 数据库对象映射
- `List`、`Set`和`Map`等集合属性映射
- 组件属性映射
- 集合元素为复合类型的映射
- 复合主键映射
- 使用传统`XML`映射文件管理映射信息

`Hibernate`是轻量级`Java EE`应用的持久层解决方案, `Hibernate`不仅管理`Java`类到数据库表的映射(包括`Java`数据类型到`SQL`数据类型的映射),还提供数据査询和获取数据的方法,可以大幅度缩短处理数据持久化的时间。
目前的主流数据库依然是`关系数据库`,而`Java`语言则是`面向对象的编程语言`,当把二者结合在起使用时相当麻烦,而`Hibernate`则减少了这个问题的困扰,它完成对象模型和基于`SQL`的关系模型的映射关系,使得应用开发者可以完全采用面向对象的方式来开发应用程序。
`Hibernate`较之另一个持久层框架`MyBatis, Hibernate`更具有面向对象的特征;受`Hibernate`的影响,`Java EE5`规范抛弃了传统的`Entity EJB`,改为使用`JPA`作为持久层解决方案。而`JPA`实体完全可以当成`Hibernate PO(Persistent Object`,持久化对象)使用,由此可见`Hibernate`的影响深远。 `Hibernate`倡导低侵入式的设计,完全采用**普通的`Java`对象**(`POJO)`编程,**不要求PO继承`Hibernate`的某个超类或实现`Hibernate`的某个接口**。
`Hibernate`充当了面向对象的程序设计语言和关系数据库之间的桥梁,** `Hibernate`允许程序开发者采用面向对象的方式来操作关系数据库**。因为有了`Hibernate`的支持,使得`Java EE`应用的`OOA`(面向对象分析)、`OOD`(面向对象设计)和`OOP`(面向对象编程)三个过程一脉相承,成为一个整体。
<!--SSTStop-->

