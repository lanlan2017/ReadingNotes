---
title: A.5 使用命令行初始化项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: e2edb360
date: 2021-10-22 17:33:08
updated: 2021-10-22 17:33:08
---
# A.5 使用命令行初始化项目
Spring Initializr的IDE和基于浏览器的用户界面可能是初始化项目的常见方式。它们都是Initializr应用程序提供的REST服务的客户端。在某些特殊情况下（例如，在脚本化场景中），我们可能会发现直接从命令行使用Initializr服务也很有用。

我们有两种消费该API的方式：


- 使用curl命令（或者类似的命令行REST客户端）；
- 使用Spring Boot的命令行接口（又称为Spring Boot CLI）。

下面我们看一下这两种方案，先从curl命令开始。

A.5.1 curl和Initializr API

使用curl初始化Spring项目的最简单方式是按照如下格式消费该API：

```
% curl https://start.spring.io/starter.zip -o demo.zip
```

在本例中，我们请求了Initializr的“/starter.zip”端点，它将会生成一个Spring项目并下载为zip文件。生成的项目是使用Maven构建的，并且除了Spring Bootstarter依赖外并没有其他的依赖，pom.xml文件中的所有项目信息都是默认值。

如果不进行特殊指定，文件名将会是starter.zip。在本例中，-o选项将下载的文件命名为demo.zip。

对外公开的Spring Initializr服务器托管在https://start.spring.io上，如果你想要使用自定义Initializr，那么需要对应地修改URL。

除了默认值之外，我们可能还想要指定一些详情信息和依赖。表A.1列出了消费Spring Initializr REST服务所有可用的参数（及其默认值）。

<center>表A.1 Initializr API支持的请求参数</center>

![epub_29101559_157](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022212716.jpeg)

我们可以通过发送请求至基础Initializr URL获取参数列表和可用依赖项的列表：

```
% curl https://start.spring.io
```

在这些参数中，我们可能会发现dependencies是最常用的。例如，我们想要创建一个使用Spring的简单Web项目。如下使用curl的命令行将会生成一个包含webstarter依赖的项目zip包：

```
% curl https://start.spring.io/starter.zip \
      -d dependencies=web \
      -o demo.zip
```

假设有一个更复杂的样例：我们想要开发一个使用Spring Data JPA进行数据持久化的Web应用程序，使用Gradle构建，位于zip文件中名为my-dir的目录下，并且我们不仅想要下载zip文件，还希望在下载时将项目解压到文件系统中。在这种情况下，下面的命令可以解决该问题:

```
% curl https://start.spring.io/starter.tgz \
       -d dependencies=web,data-jpa \
       -d type=gradle-project
       -d baseDir=my-dir | tar -xzvf -
```

在这里，下载的zip文件将会以管道的方式传递给tar命令进行解压。

A.5.2 Spring Boot命令行接口

Spring Boot CLI是另一种初始化Spring应用的方案。我们能够以多种方式安装Spring Boot CLI，最简单的（也是我最喜欢的）方式可能是使用SDKMAN：

```
% sdk install springboot
```

Spring Boot CLI安装完成之后，我们就可以使用它来生成项目了。使用方式与curl非常类似，这里我们要使用的命令是spring init。实际上，使用Spring Boot CLI生成项目的最简单方式为：

```
% spring init
```

这样会生成一个Spring Boot项目的骨架，并且会下载成名为demo.zip的zip文件。

有时我们可能想要指明一些详情信息和依赖，表A.2列出了spring init命令所有可用的参数。

<center>表A.2 spring init命令支持的所有请求参数</center>

![epub_29101559_158](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211022212941.jpeg)

通过使用--list参数，我们可以列出参数的列表以及可用依赖：

```
% spring init --list
```

假设我们希望创建一个基于Java 1.7的Web应用，那么如下使用--dependencies和--java命令即可：

```
% spring init --dependencies=web --java-version=1.7
```

假设我们想要创建一个使用Spring Data JPA进行数据持久化的Web应用程序，并且还希望使用Gradle构建它，而不是使用Maven，那么我们可以使用如下的命令：

```
% spring init --dependencies=web,jpa --type=gradle-project
```

你可能已经发现，spring init的很多参数与curl方案的参数相同或相似。也就是说，spring init并没有支持curl方案中的所有参数（比如baseDir），而且参数是中划线分割的而不是采用驼峰命名（例如package-name与packageName）。

