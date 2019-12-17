---
title: 第2章 FFmpeg工具使用基础 本章概览
categories: 
  - FFmpeg从入门到精通
  - 第一部分 FFmpeg的命令行使用篇
  - 第2章 FFmpeg工具使用基础
date: 2019-09-12 22:12:09
updated: 2019-11-02 10:12:04
abbrlink: 80a8481e
---
<div id='my_toc'><a href="/ReadingNotes/80a8481e/#第2章-FFmpeg工具使用基础-本章概览" class="header_1">第2章 FFmpeg工具使用基础 本章概览</a><br></div>
<style>
    .header_1{
        margin-left: 1em;
    }
    .header_2{
        margin-left: 2em;
    }
    .header_3{
        margin-left: 3em;
    }
    .header_4{
        margin-left: 4em;
    }
    .header_5{
        margin-left: 5em;
    }
    .header_6{
        margin-left: 6em;
    }
</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}
var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}
</script>

<!--end-->
# 第2章 FFmpeg工具使用基础 本章概览 #
`FFmpeg`中常用的工具主要是`ffmpeg`、`ffprobe`、`ffplay`,它们分别用作多媒体的编解码工具、内容分析工具和播放器,本章将重点介绍这三个工具的常用命令。
本章主要介绍如下几个方面。
- 2.1节将重点介绍`ffmpeg`命令,介绍`ffmpeg`常用的参数用法并举例说明,例如如何查看`ffmpeg`的帮助信息,如何通过`ffmpeg`的帮助信息快速了解转码参数并快速上手使用。
- 2.2节将重点介绍`ffprobe`命令,介绍`ffprobe`进行音视频数据分析的常用参数,并通过实例介绍如何分析视频文件的流信息、包信息、帧信息、导出数据等。
- 2.3节将重点介绍`ffplay`命令,介绍`ffplay`常用的参数使用及示例,例如,如何使用`ffplay`定制化窗口播放视频、输出音频可视化数据、输出视频可视化数据等。


