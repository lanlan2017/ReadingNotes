---
title: A.3 使用NetBeans初始化项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: afcc5293
date: 2021-10-22 17:20:45
updated: 2021-10-22 17:20:45
---
# A.3 使用NetBeans初始化项目
要使用NetBeans创建新项目，首先要选择File菜单的New Project菜单项，如图A.10所示。

![image-20211022213836364](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213836.png)

<center>图A.10 使用NetBeans初始化一个新的Spring项目</center>

此时我们会看到新项目向导的第一页，如图A.11所示。该页面会让我们选择想要创建什么类型的项目。

![image-20211022213851422](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213851.png)

<center>图A.11 创建新的Spring Boot Initializr项目</center>

对于Spring Boot项目来说，我们要从左侧的列表中选择Maven，然后在右侧的项目列表中选择Spring Boot Initializr Project，然后点击Next按钮进入下一页。

新项目向导的第二页（见图A.12）允许我们设置项目的基本信息，比如项目名称、版本以及Maven pom.xml文件中定义项目的其他信息。

![image-20211022213902798](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213902.png)

<center>图A.12 声明项目的基本信息</center>

在声明完项目的基本信息之后，点击Next按钮进入新项目向导的依赖页，参见图A.13。

![image-20211022213921937](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213922.png)

<center>图A.13 选择项目的依赖</center>

依赖会按照分类的形式全部列在同一个列表中。如果在查找特定依赖时遇到麻烦，可以使用顶部的Filter文本框限制列表中可选项的数量。

在这个页面中，还可以指定想要使用哪个Spring Boot版本。它默认会设置为当前Spring Boot的正式版本。

在为项目选择完依赖之后，点击Next按钮会显示新项目向导的最后一页，如图A.14所示。这个页面允许我们声明项目的一些详情信息，包括项目的名称以及文件系统中的位置（Project Folder文本域是只读的，它的值会根据其他两个文本域的值衍生而来）。在这里，还允许我们通过Maven Spring Boot插件运行和调试项目，而不是使用NetBeans。我们还可以让NetBeans移除生成项目中的Maven包装器。

![image-20211022213940930](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213941.png)

<center>图A.14 指明项目的名称和位置</center>

在设置完项目的所有信息后，点击Finish按钮，项目将会创建并添加到NetBeans的工作空间中。

