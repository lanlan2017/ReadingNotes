---
title: 第10章 jQuery+Bootstrap 整合开发 电子拍卖系统
categories: 
  - 疯狂前端开发讲义JQuery AngularJS Bootstrap前端开发实战
  - 第10章 jQuery+Bootstrap整合开发 电子拍卖系统
  - 10.0 前言
date: 2019-08-09 23:21:57
updated: 2019-11-02 01:39:01
abbrlink: 7599622e
---
- [第10章 jQuery+Bootstrap 整合开发:电子拍卖系统](/ReadingNotes/7599622e/#第10章-jQuery-Bootstrap-整合开发-电子拍卖系统)
    - [本章要点](/ReadingNotes/7599622e/#本章要点)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
# 第10章 jQuery+Bootstrap 整合开发:电子拍卖系统 #
## 本章要点 ##
- 传统`Java EE`应用的系统设计
- 分析、提取系统的`Domain Object`
- 映射`Hibernate`的持久化对象
- 基于`Hibernate 5`实现`DAO`组件
- 在`Spring`容器中部署`DAO`组件
- 实现业务逻辑组件
- 部署业务逻辑组件
- 使用声明式事务机制为业务逻辑方法增加事务控制
- 利用`Spring`邮件抽象层发送竞价确认邮件
- 利用`Spring`任务调度处理拍卖到期的物品
- 使用`Spring MVC`暴露前端`JSON`接口
- 前端控制器的异常处理方式
- 使用`jQuery`异步装载页面片段
- 使用`Bootstrap`构建前端界面
- 使用`jQuery`发送异步请求
- 使用`jQuery`动态更新`HTML`页面

本章介绍的系统是一个前端开发+后端整合的系统,本系统前端综合使用了`jQuery+Bootstrap`,后端则整合使用了`Spring MVC`、`Spring`、`Hibernate`这些框架。
该系统是一个模拟的电子拍卖系统。注册用户可以在这里发布拍卖物品,参与竞价。非注册用户可以浏览拍卖物品,浏览流拍物品。如果到了物品的拍卖期限,系统提供后台线程判断物品是流拍了,还是被最高竞价者赢取。注册用户参与竞价后,系统会发送邮件通知竞价用户。`Spring`的任务调度负责启动后台线程来修改物品状态;`Spring`的邮件抽象层负责发送竞价通知邮件。

本系统使用`Hibernate`作为持久层的`ORM`框架,使用`Spring`管理业务层组件和持久层组件。`Spring MVC`作为前端`MVC`控制器,用于对外暴露`JSON`接口供前端界面调用,权限控制也在`Spring MVC`层完成。本应用的界面使用`Bootstrap`的样式和组件实现;使用`jQuery`作为异步交互的引擎,负责与前端和后端的交互,并通过`jQuery`封装的方法来操作`DOM`页面。

