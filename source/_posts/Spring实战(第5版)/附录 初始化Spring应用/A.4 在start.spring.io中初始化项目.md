---
title: A.4 在start.spring.io中初始化项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: cea959a6
date: 2021-10-22 17:24:18
updated: 2021-10-22 17:24:18
---
# A.4 在start.spring.io中初始化项目
到目前为止所描述的基于IDE的初始化方案可能会满足你的需求，但是有时候你可能需要完全不同的IDE，或者使用简单的文本编辑器。在这种情况下，你依然可以借助基于Web界面的Initializr来使用Spring Initializr。

首先，在Web浏览器中访问 https://start.spring.io 。我们将会看到简单版本的Spring Initializr Web用户界面，如图A.15所示。

![image-20211022214010291](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022214010.png)

<center>图A.15 简单版本的Spring Initializr Web界面</center>

在简单版本的Initializr Web应用中，我们只需要填写一些非常基本的信息，比如使用Maven还是Gradle进行构建、开发项目要使用什么语言、基于什么版本的Spring Boot进行构建以及项目的group和artifact ID。

我们还可以通过在Search for Dependencies文本框中输入搜索条件来指明依赖。例如，如图A.16所示，我们可以输入“web”来搜索带有“web”关键字的依赖。

![image-20211022214019020](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022214019.png)

<center>图A.16 搜索依赖</center>

当看到自己想要的依赖时，在键盘上按Return键来选中它，它就会添加到选中依赖的列表中。在图A.17中，Selected Dependencies文本下面显示已经选中了Web、Thymeleaf、DevTools和Lombok依赖。

![image-20211022214029301](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022214029.png)

<center>图A.17 选择依赖</center>

如果不想要某个已选中的依赖，只需要点击依赖条目右侧的×就可以将其移除。

完成之后，我们可以点击Generate Project按钮（也可以使用按钮上所显示的快捷键，不同操作系统下会有所差异），让Initializr初始化项目并下载为zip文件。然后，我们就可以解压该文件并导入你所选择的IDE或文本编辑器了。

如果你希望更细粒度地控制项目创建的过程，可以点击Generate Project下的Switch to the full version链接，这样用户界面会展现更多的输入域和所有可用依赖的复选框列表。图A.18显示了Web界面完整版本的一部分。

![image-20211022214042949](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022214043.png)

<center>图A.18 完整版本的Initializr用户界面（部分）</center>

完整版本中的大多数输入域都衍生自Group和Artifact输入域，或者在简单版本中已经有了默认值。完整版本能够让我们重写这些衍生值/默认值。

图A.18只展现了完整版本中可用依赖复选框的一部分，所以你可能需要向下滑动很久才能找到想要的依赖。不过，在完整版本的用户界面中，搜索框依然是可用的。

