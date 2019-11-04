---
title: 第8章 Java集合 本章要点
categories: 
  - 疯狂Java讲义 (第4版)
  - 第8章 Java集合
  - 8.0 本章要点
date: 2019-07-06 12:58:24
updated: 2019-11-02 01:39:01
abbrlink: 7956ffc8
---
- [第8章 Java集合 本章要点](/ReadingNotes/7956ffc8/#第8章-Java集合-本章要点)
    - [java集合用途](/ReadingNotes/7956ffc8/#java集合用途)
    - [java集合分类](/ReadingNotes/7956ffc8/#java集合分类)
    - [java集合中来存放对象的引用](/ReadingNotes/7956ffc8/#java集合中来存放对象的引用)
    - [Java5对集合的增强](/ReadingNotes/7956ffc8/#Java5对集合的增强)
    - [本章重点](/ReadingNotes/7956ffc8/#本章重点)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->

# 第8章 Java集合 本章要点 #
- 集合的概念和作用
- 使用`Lambda`表达式遍历集合
- `Collection`集合的常规用法
- 使用`Predicate`操作集合
- 使用`Iterator`和`foreach`循环遍历`Collection`集合
- `HashSet`、 `LinkedHashSet`的用法
- 对集合使用`Stream`进行流式编程
- `EnumSet`的用法
- `TreeSet`的用法
- `ArrayList`和`Vector`
- `List`集合的常规用法
- `Queue`接口与`Deque`接口
- 固定长度的`List`集合
- `ArrayDeque`的用法
- `PriorityQueue`的用法
- `Map`的概念和常规用法
- `LinkedList`集合的用法
- `TreeMap`的用法
- `HashMap`和`HashTable`
- 几种特殊的`Map`实现类
- `Hash`算法对`HashSet`、`HashMap`性能的影响
- `Collections`工具类的用法
- `Java9`新增的不可变集合
- `Enumeration`迭代器的用法
- `Java`的集合体系

## java集合用途 ##
- `Java`集合类是一种特别有用的工具类,可**用于存储`数量不等`的对象**,
- 并可以`实现常用的数据结构`,如`栈`、`队列`等。
- `Java`集合还可用于保存具有映射关系的`关联数组`。

## java集合分类 ##
**`Java`集合大致可分为`Set`、`Lits`、 `Queue`和`Map`四种体系**,其中
- `Set`代表`无序`、`不可重复`的集合;
- `List`代表`有序`、`可以重复`的集合;
- `Map`代表具有`映射`关系的集合,
- `Java 5`增加了`Queue`体系集合,代表一种`队列`集合实现。

## java集合中来存放对象的引用 ##
`Java`集合就像一种容器,可以把多个对象的引用"丢进"该容器中,虽然集合中存放的是对象的引用,但习惯上也以认为存放的是对象。
## Java5对集合的增强 ##
在`Java 5`之前,`Java`集合会丢失容器中所有对象的数据类型,把所有对象都当成`Object`类型处理;
从`Java5`增加了`泛型`以后,`Java`集合可以记住容器中对象的数据类型,从而可以编写出更简洁、健壮的代码。
本章不会介绍泛型的知识,本章重点介绍`Java`的4种集合体系的功能和用法。
## 本章重点 ##
本章将详细介绍`Java`的4种集合体系的常规功能,深入介绍各集合实现类所提供的独特功能,深入分析各实现类的实现机制,以及用法上的细微差别,并给出**不同应用场景选择哪种集合实现类**的建议。

<!--SSTStop-->
