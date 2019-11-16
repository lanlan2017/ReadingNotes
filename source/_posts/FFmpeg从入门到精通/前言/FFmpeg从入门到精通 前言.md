---
title: FFmpeg从入门到精通 前言
categories: 
  - FFmpeg从入门到精通
  - 前言
date: 2019-09-11 16:55:27
updated: 2019-11-02 01:38:59
abbrlink: ae3baeda
---
- [FFmpeg从入门到精通 前言](/ReadingNotes/ae3baeda/#FFmpeg从入门到精通-前言)
    - [如何阅读本书](/ReadingNotes/ae3baeda/#如何阅读本书)
    - [本书源码](/ReadingNotes/ae3baeda/#本书源码)
    - [相关文档](/ReadingNotes/ae3baeda/#相关文档)
        - [官方文档资料](/ReadingNotes/ae3baeda/#官方文档资料)
        - [中文经典资料](/ReadingNotes/ae3baeda/#中文经典资料)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# FFmpeg从入门到精通 前言#
## 如何阅读本书 ##
本书一共包含10章,按照所讲述的内容以及所面向读者的不同层次,可以划分为两大部分,具体如下。
- 第一部分为`FFmpeg`的命令行使用篇,包括第1章到第7章,介绍了`FFmpeg`的基础组成部分、`FFmpeg`工具使用、`FFmpeg`的封装操作、`FFmpeg`的转码操作、`FFmpeg`的流媒体操作、`FFmpeg`的滤镜操作和`FFmpeg`的设备操作。
- 第二部分为`FFmpeg`的`API`使用篇,包括第8章到第10章,介绍了`FFmpeg`封装部分的`API`使用操作、`FFmpeg`编解码部分的`API`使用操作和`FFmpeg`滤镜部分的`API`使用操作,相关操作均以实例方式进行说明,包括新`API`及旧`API`的操作。

如果你已经能够通过源代码独立安装`FFmpeg`,那么可以跳过第1章直接从第2章开始阅读;如果你对命令行使用没有兴趣,或者希望使用`FFmpeg`的`API`开发,那么可以跳过前7章直接从第8章开始阅读。笔者建议最好是从第1章开始阅读。

## 本书源码 ##
另外,本书代码相关的举例均可以在`FFmpeg`的源代码目录的`doc/examples`中获得,也可以通过`FFmpeg`官方网站的[文档](https://ffmpeg.org/doxygen/trunk/examples.html)获得
## 相关文档 ##
`FFmpeg`发展了至少17年,积累了极其丰富的资料,能够满足大部分的需求。由于`FFmpeg`的更新与版本的迭代,不同版本之间使用的参数相对来说会稍微有所不同,由于本书篇幅有限,所以`FFmpeg`的很多交流社区的资源同样值得参考。
### 官方文档资料 ###
- `FFmpeg`[官方文档](http://ffmpeg.org/documentation.html)
- `FFmpeg`[官方wiki](https://trac.ffmpeg.org)

### 中文经典资料 ###
- [雷霄骅博士总结的资料](http://blog.csdn.net/leixiaohua1020)
- [罗索实验室](http://www.rosoo.net)
- [ChinaFFmpeg](http://bbs.chinaffmpeg.com)

除了以上这些信息，还可以通过Google、百度等搜索引擎获得大量相关资料。
`FFmpeg`本身也提供了命令参数的详细说明,读者可以查看`FFmpeg`的帮助信息,后面的章节将会对此进行详细的介绍。
<!--SSTStop-->

