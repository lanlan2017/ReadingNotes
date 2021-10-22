---
title: A.2 使用IntelliJ IDEA初始化项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: faac6e04
date: 2021-10-22 17:17:29
updated: 2021-10-22 17:17:29
---
# A.2 使用IntelliJ IDEA初始化项目
如果要使用IntelliJ IDEA初始化Spring项目，就在File > New菜单下选择Project菜单项，如图A.5所示。

![image-20211022213640922](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213640.png)

<center>图A.5 在IntelliJ IDEA中初始化一个新的Spring项目</center>

此时，将会打开新Spring Initializr项目向导的第一页（参见图A.6）。在本页中，通常我们会直接点击Next按钮进入下一页。如果你想要使用与 https://start.spring.io 不同的Spring Initializr，就可以选中Custom单选框，并输入想要使用的Spring Initializr的基础URL。

![image-20211022213653302](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213653.png)

<center>图A.6 选择Spring Initializr的位置</center>

点击Next按钮之后，我们将会看到一个输入项目基本信息的页面，如图A.7所示。你会发现，这个页面上有很多输入域与Maven pom.xml中的信息是一致的。实际上，在Type输入域中选择Maven Project，就能发现这些输入域的用途所在。如果你更喜欢Gradle，也可以选择Gradle Project。

![image-20211022213733109](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213733.png)

<center>图A.7 在IntelliJ IDEA中指明必要的项目信息</center>

在填写完必要的项目信息后，点击Next按钮将会展现项目依赖页（见图A.8）。

![image-20211022213747989](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213748.png)

<center>图A.8 选择项目依赖</center>

在最左侧，依赖是按照分类来组织的。选中某个分类时，这个分类对应的可选项会显示在中间区域。已经选中的依赖将会（按照分类）列在最右侧。

在选择完依赖之后，点击Next按钮，我们将会看到项目向导的最后一页，如图A.9所示。在这个页面中，我们要输入项目的名称并指定项目要放到磁盘的什么位置。

![image-20211022213758124](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213758.png)

<center>图A.9 设置项目的名称和位置</center>

点击Finish按钮，项目将会创建并加载到IntelliJ IDEA的工作空间中。

