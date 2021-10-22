---
title: A.7 构建和运行项目
categories:
  - Spring实战(第5版)
  - 附录 初始化Spring应用
abbrlink: eb68ec1b
date: 2021-10-22 17:35:24
updated: 2021-10-22 17:35:24
---
# A.7 构建和运行项目
不管你采用什么方式初始化项目，都可以在命令行中使用java -jar命令来运行应用：

```
% java -jar demo.jar
```

即使不采用JAR文件而使用WAR文件来进行分发，这样做也依然是可行的：

```
% java -jar demo.war
```

我们还可以使用Spring Boot Maven或Gradle插件来运行应用。比如，项目使用Maven构建的话，可以这样运行：

```
% mvn spring-boot:run
```

使用Gradle进行构建的话，可以按照如下方式运行项目：

```
% gradle bootRun
```

不管是采用Maven还是Gradle，构建工具都会构建（还没有构建的话）并运行项目。
