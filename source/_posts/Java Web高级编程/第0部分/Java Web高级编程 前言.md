---
title: Java Web高级编程 前言
categories: 
  - Java Web高级编程
  - 第0部分
date: 2019-08-12 00:30:59
updated: 2019-12-17 02:00:55
abbrlink: 487481ea
---
<div id='my_toc'><a href="/ReadingNotes/487481ea/#代码示例" class="header_1">代码示例</a>&nbsp;<br><a href="/ReadingNotes/487481ea/#Maven依赖" class="header_1">Maven依赖</a>&nbsp;<br><a href="/ReadingNotes/487481ea/#将安全相关的内容安排在最后的原因" class="header_1">将安全相关的内容安排在最后的原因</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 代码示例 #
作为一本软件开发书籍,该书广泛地应用了代码示例,通过它们证明我们正在讨论的主题。大多数情况下,这些示例都是完整的`IDE`项目,你可以在DE中打开、编译和执行。所有的示例都可以从`wrox.com`代码下载网站和这个[网址](http://www.tupwk.com.cn/downpage)获得。请访问[网址](http://www.wrox.com/go/projavaforwebapps)并单击`Download code`选项卡。你可以将所有代码示例下载为单个ZP文件或者将每章的示例单独下载为一个ZP文件。在每章的示例中,可以找到每个示例的两个版本:一个`IntelliJ IDEA`项目和一个`Eclipse`项目。使用自己选择的IDE对应的版本即可。如果你使用的不是这两种`IDE`中的某一个,那么你的`IDE`应该能够将`IntelliJ IDEA`项目作为简单的`Maven`项目导入。
# Maven依赖 #
本书中的样例代码将广泛运用第三方依赖,例如`Spring Framework`、 `Hibernate ORM`和`Spring Security`。在下载网站的代码中包含这些依赖`JAR`,将使下载文件变大,你可能需要下载几百兆的文件。为了解决这个问题,样例代码将使用`Apache Maven`及其依赖管理功能。所有的示例项目都是`Maven`项目。在`IDE`中打开每个项目时,`IDE`将自动在本地`Maven`库中查找这些依赖,或者如果需要的话,`IDE`将下载它们到本地`Maven`库中。
在每章的首页,你将会看到一个标题为"本章新增的`Maven`依赖"的区域。该部分列出了本章中新增的`Maven`依赖。你也可以查看`pom. xml`文件来检查每个示例项目的依赖。某些章节未引入新的`Maven`依赖,但大多数章节都引入了。
每个`Maven`依赖都会有作用域,用于定义依赖在哪个类路径上可用。
- 最常见的作用域——`"compile"`作用域——表示该依赖在项目的编译类路径上、单元测试编译和执行类路径上以及运行应用程序时的最终运行时类路径上可用。在`Java EE Web`应用程序中,这意味着依赖将被复制到所部署的应用程序中。
- `" runtime"`作用域表示依赖将在单元测试执行和运行时执行类路径上可用,但不像`" compile"`作用域一样在编译应用程序或者执行单元测试时也可用。一个运行时依赖将被复制到所部署的应用程序中。
- 最后,`" provided"`作用域表示运行应用程序的容器将会提供该依赖。

在`Java EE`应用程序中,这意味着依赖已经在`Servlet`容器或应用服务器的类路径上了,因此不需要再复制到部署的应用程序中。 `Maven`和`IDE`将保证在编译应用程序和执行单元测试时,`" provided"`作用域的依赖是可用的。 `Maven`还有其他类型的作用域,但在本书中将只会用到这些。
在文本和示例项目中,有一些`Maven`依赖将会包含排除( (`exclusions)`),用于忽略某些特定的依赖——它们被称为临时依赖。很多时候这些排除都是多余的,列出它们只是为了使代码更清晰。当某个依赖依赖于另一个旧版本的依赖,而不是现在正在使用的依赖时,通过排除可以更清楚地表示这里出现了矛盾,并且避免了由`Maven`的最近算法所引起的问题。不过,某些排除的存在是由于`Java Se`或`Java ee`的新版本已经提供了依赖,或者因为依赖ID发生了变化。当出现这种情况时,文本中会进行提示。
# 将安全相关的内容安排在最后的原因 #
坦白地说,应用程序安全会影响其他内容的学习。在产品中添加认证和授权所使用的技术将会干扰你的代码,并使学习过程变得困难。安全是第一位的,而且一直记得安全问题永远也不是错误。不过,只要使用了正确的工具,在项目完成(或基本上完成之后为它添加验证和授权也是相当简单的一件事。**本书首先将关注于如何使用工业标准工具创建出高质量、特性丰富的`web`应用程序。在学会了创建强大应用程序所需的技能之后,本书的第Ⅳ部分将向你展示如何为现有的应用程序添加认证和授权,保护它不受未授权的和恶意访问的攻击**。
