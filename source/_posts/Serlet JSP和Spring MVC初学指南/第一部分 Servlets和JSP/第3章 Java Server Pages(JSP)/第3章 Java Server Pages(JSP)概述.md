---
title: 第3章 Java Server Pages(JSP)概述
categories: 
  - Serlet JSP和Spring MVC初学指南
  - 第一部分 Servlets和JSP
  - 第3章 Java Server Pages(JSP)
date: 2019-03-25 11:05:01
updated: 2019-11-02 01:38:59
abbrlink: 9cc208c7
---
- [第3章 Java Server Pages(JSP)概述](/ReadingNotes/9cc208c7/#第3章-Java-Server-Pages-JSP-概述)
    - [Servlet的缺点](/ReadingNotes/9cc208c7/#Servlet的缺点)
    - [JSP](/ReadingNotes/9cc208c7/#JSP)
    - [本章概述](/ReadingNotes/9cc208c7/#本章概述)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
## 第3章 Java Server Pages(JSP)概述 ##
### Servlet的缺点 ###
`Servlet`有两个缺点是无法克服的：
- 写在`Servlet`中的所有`HTML`标签必须写成`Java`字符串的形式，这使得处理`HTTP`响应报文的工作变得十分烦琐；
- 所有的文本和`HTML`标记是硬编码，导致即使是表现层的微小变化，如改变背景颜色，也需要重新编译`Servlet`。

### JSP ###
`Java Server Pages(JSP)`解决了上述两个问题。不过,`JSP`不会取代`Servlet`，相反，它们具有互补性。现代的`Java` `Web`应用会同时使用`Servlet`和`JSP`页面。

### 本章概述 ###
本章介绍了`JSP`技术，并讨论了在`JSP`页面中，隐式对象的使用意见，3个语法元素（指令、脚本元素和动作），还讨论了错误处理。可以用标准语法或`XML`语法编写`JSP`。用`XML`语法编写的`JSP`页面被称为`JSP`文档。由于很少用`XML`语法编写`JSP`，故本章不做介绍。在本章中，我们将主要学习`JSP`标准语法。

