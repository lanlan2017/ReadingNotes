---
title: A.1 使用Spring Tool Suite初始化项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: '5793e489'
date: 2021-10-22 17:14:12
updated: 2021-10-22 17:14:12
---
要使用Spring Tool Suite来初始化新的Spring项目，我们需要在File > New菜单中选择Spring Starter Project菜单项，如图A.1所示。

![image-20211022213446109](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213446.png)

<center>图A.1 在Spring Tool Suite中初始化一个新项目</center>

注意：这是一个使用Spring Tool Suite初始化Spring项目的简单描述。更详细的阐述，可以参考1.2.1小节。

接下来，我们将会看到项目创建对话框的第一页（见图A.2）。在这个页面中，我们将会定义项目的基本信息，比如项目名称、坐标（group ID和artifact ID）、版本和基础包名。我们也可以确定项目使用Maven还是Gradle来构建，还可以声明构建生成JAR文件还是WAR文件，以及使用哪个版本的Java，甚至还能使用其他的JVM语言，比如Groovy或Kotlin。

![image-20211022213458149](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213458.png)

<center>图A.2 定义基本的项目信息</center>

这个页面的第一个输入域要求我们指定Spring Initializr服务的位置。如果你运行或使用自定义的Initializr实例，那么可以在这里指定Initializr服务的基础URL；否则，使用默认的http://start.spring.io就可以了。

在定义完项目的基本信息之后，点击Next按钮，会看到项目的依赖页（见图A.3）。

![image-20211022213509034](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213509.png)

<center>图A.3 指定项目的依赖</center>

在项目依赖页中，我们可以指定项目需要的所有依赖。其中，有些依赖是SpringBoot Starter依赖，有些依赖是Spring项目常用的依赖。

可用的依赖都列在左侧，以分组的形式进行组织，可以展开和收缩。如果在查找依赖时遇到麻烦，还可以对依赖进行搜索，以便于缩小可选范围。

要将某个依赖添加到所生成的项目中，我们只需要选中依赖名称前面的复选框即可。已经选中的依赖会显示在右侧Selected标题下面。如果想要移除依赖，可以点击已选中依赖前面的×，也可以点击Clear Selection按钮清除所有已选的依赖。

为了增加便利性，如果你发现在项目中特定的一组依赖始终（或者经常）会用到，那么你可以在选择完这些依赖后点击Make Default按钮，这样在下一次创建项目的时候它们会预先选中。

在选择完之后，点击Finish按钮就可以生成项目并添加到工作空间中了。

如果你想要使用http://start.spring.io之外的其他Initializr，可以点击Next按钮来设置Initializr的基础URL，如图A.4所示。

![image-20211022213533643](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022213533.png)

<center>图A.4 指定Initializr的基础URL</center>

Base Url输入域指定了Initializr API监听的URL。在这个页面中，这是唯一可以修改的输入域。Full Url输入域展现了通过Initializr请求新项目的完整URL地址。

