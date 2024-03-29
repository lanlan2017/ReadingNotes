---
title: 3 关于本书_Spring实战(第5版)
categories:
  - Spring实战(第5版)
  - 第0部分 内容提要 译者序 关于本书 前言 致谢 资源与支持
abbrlink: 873f91b0
date: 2021-10-03 18:59:11
updated: 2021-10-03 20:00:19
---
# 关于本书
编写《Spring实战（第5版）》的目的是让读者学会使用Spring框架、Spring Boot以及Spring生态系统中各种辅助部分构建令人赞叹的应用程序。本书首先介绍如何使用Spring和Spring Boot开发基于Web、以数据库作为后端的Java应用；随后进行必要的扩展，展现如何与其他应用进行集成、使用反应式类型进行编程，以及将应用拆分为离散的微服务；最后讨论如何准备应用的部署。

尽管Spring生态系统中的每个项目都提供了完善的文档，但是本书所做的是所有参考文档都无法做到的事情：提供一个实用的、项目驱动的指南，将Spring的各种元素组合起来形成一个真正的应用。

## 谁应该阅读这本书
《Spring实战（第5版）》适用于刚刚开始学习Spring Boot和Spring框架的Java开发人员，也适用于想要超越基础知识并学习Spring新特性的经验丰富的Spring开发者。

## 这本书是如何组织的：路线图
本书分成了5个部分，共计19章。
第1部分涵盖构建Spring应用的基础话题。
- 第1章介绍Spring和Spring Boot以及如何初始化Spring项目。在本章中，我们迈出构建Spring应用的第一步，在本书后续各章中，我们会对这个应用进行扩展。
- 第2章讨论如何使用Spring MVC构建应用的Web层。在本章中，我们将会构建处理Web请求的控制器以及在浏览器中渲染信息的视图。
- 第3章会深入探讨Spring应用的后端，在这里数据会持久化到关系型数据库中。
- 在第4章中，我们会使用Spring Security认证用户并防止未认证的用户访问应用。
- 第5章介绍如何使用Spring Boot的配置属性功能来配置Spring应用。我们还会学习如何使用profile选择性地应用配置。

第2部分讨论如何将Spring应用与其他应用进行集成。
- 第6章延续第2章对Spring MVC的讨论，我们将会学习如何在Spring中编写REST API。
- 第7章讨论了和第6章相对立的主题，展现Spring应用如何消费REST API。
- 第8章会讨论如何使用异步通信技术让Spring应用发送和接收消息，这里会用到Java Message Service、RabbitMQ或Kafka。
- 第9章讨论如何使用Spring Integration进行声明式的应用集成。

第3部分探讨Spring对反应式编程提供的全新支持。
- 第10章介绍Reactor项目。这是一个反应式编程库，支撑了Spring 5的反应式特性。
- 第11章重新探讨REST API开发，介绍全新的Web框架Spring WebFlux。该框架借用了很多Spring MVC的理念，但是为Web开发提供了新的反应式模型。
- 第12章将会看一下如何使用Spring Data编写反应式数据持久化，我们将会读取和写入Cassandra与Mongo数据库。

第4部分将会拆分单体应用模型，介绍Spring Cloud和微服务开发。
- 第13章会深入介绍服务发现，组合使用Spring和Netflix的注册中心实现Spring微服务的注册和发现。
- 第14章将展现如何在配置服务器中实现中心化的应用配置，从而实现跨微服务共享配置。
- 第15章会介绍Hystrix的断路器模式。它能够让微服务在面临失败时更有弹性。

在第5部分中，我们将会讨论如何做好将应用投入生产环境的准备，并看一下如何进行部署。
- 第16章会介绍Spring Boot Actuator。它是Spring Boot的一个扩展，通过REST端点的形式暴露Spring应用内部的运行状况。
- 第17章将会介绍如何使用Spring Boot Admin。它是构建在Actuator之上的一个用户友好的基于浏览器的管理应用。
- 第18章将会讨论如何将Spring bean暴露为JMX MBean以及如何消费它们。
- 在第19章中，我们会看到如何将Spring应用部署到各种生产环境中。

通常来讲，刚刚接触Spring的开发人员应该从第1章开始，并按顺序阅读每一章；经验丰富的Spring开发人员可能更愿意在任何感兴趣的时候参与进来。即便如此，每一章都是建立在前一章内容的基础上的，所以如果从中间开始阅读，那么可能会漏掉一些上下文信息。

## 关于代码
本书包含许多源代码的样例，有的是编号的程序清单，有的是普通文本内嵌的源码。在这两种情况下，源代码都使用固定宽度的字体排版，以便将其与普通文本分开。有时代码也会使用粗体显示，以便于强调此处代码与本章前面步骤的变更，比如为已有的代码行添加新的特性。

在许多情况下，原始源代码会重新格式化；我们添加了换行符和重新缩进，以适应书中可用的页面空间。在极少数情况下，这样做依然是不够的，在这种情况下程序清单会包括换行符(➥)。此外，当在文中描述代码的时候，源码中的注释通常会被移除。许多程序清单会有代码标注，用来突出强调重要的概念。

本书中样例的源码可以通过异步社区的本书页面下载。
## 其他在线资源
还需要其他帮助吗？
- Spring的Web站点有很多有用的起步指南（其中一部分就是由本书的作者编写的）。
- StackOverflow上的Spring标签和Spring Boot是一个询问Spring问题和帮助别人的好地方。帮助解决别人的Spring问题是学习Spring的好办法。

## 关于作者
克雷格·沃斯（Craig Walls）是Pivotal的首席工程师。他是Spring框架的热心推动者，经常在本地用户组和会议上发言，撰写关于Spring的文章。在不琢磨代码的时候，Craig正在计划去迪士尼世界或迪士尼乐园的下一次旅行，他希望尽可能多地陪伴他的妻子和两个女儿。

## 关于封面
《Spring实战（第5版）》的封面人物是“Le Caraco”，也就是约旦西南部卡拉克（Karak）省的居民。该省的首府是Al-Karak，那里的山顶有座城堡，对死海和周边的平原有着极佳的视野。这幅图出自1796年出版的法国旅游图书，Encyclopédiedes Voyages，由J.G.St.Sauveur编写。在那时，为了娱乐而去旅游还是相对新鲜的做法，而像这样的旅游指南是很流行的，它能够让旅行家和足不出户的人们了解法国其他地区和国外的居民。

Encyclopédiedes Voyages中多种多样的图画生动描绘了200年前世界上各个城镇和地区的独特魅力。在那时，相隔几十千米的两个地区着装就不相同，可以通过着装判断人们究竟属于哪个地区。这本旅行指南展现了那个时代和其他历史时代的隔离感和距离感，这与我们这个运动过度的时代是截然不同的。

从那以后，服装风格发生了改变，富有地方特色的多样性开始淡化。现在，有时很难说一个洲的居民和其他洲的居民有什么不同。可能，从积极的方面来看，我们用原来文化和视觉上的多样性换来了个人风格的多变性，或者可以说是更为多样化和有趣的知识科技生活。这本旅行指南中的图片反映了两个世纪前各个地区生活的多样性，我们现在用图书封面的方式对其进行了再现。Manning出版社的员工都认为这是计算机行业中一个很有意思的创意。
