---
title: 第2章 Eclipse开发工具
categories: 
  - 7 Java经典编程300例
  - 第2章 Eclipse开发工具
date: 2020-09-06 08:49:36
updated: 2020-09-06 08:49:36
abbrlink: 4d2eea0f
---
<div id='my_toc'></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第2章 Eclipse开发工具
本章读者可以学到如下实例:
- 实例005 下载并运行`Eclipse`工具
- 实例006 为`Eclipse`安装汉化包
- 实例007 使用`Eclipse`注释代码
- 实例008 使用`Eclipse`格式化代码
- 实例009 安装`WindowBuilder`插伫
- 实例010 开发计算器界面

## 实例006 为Eclipse安装汉化包
(1)在浏览栏中输入[www.eclipse.org/babel/](http://www.eclipse.org/babel/)",按`Enter`键将打开`Babel`的网图25所示。单击`Downloads`超链接
(2)在打开的`Eclipse Babel`下载页面中单击`Helios`超链接,如图26所示。
(3)在新页面中,单击`Language: Chinese(Simplified)`中的`BabelLanguagePack-Eclipse-zh360.V20101211043401,zip(9291`%)超链接进行下载。
(4)完成下载后,将其解压到`eclipse`文件夹中,即将`Eclipse`和`Eclipse`汉化的压缩包解压在同一个位置。这样就完成了汉化。

## 实例009 安装WindowBuilder插件
默认的`Eclipse`工具并没有提供图形化的`Swing`程序开发工具。本实例将演示如何安装`WindowBuilder`插件,它是`Google`公司提供的图形化`Swing`程序开发插件。使用它来开发`Swing`程序的界面如图2.11所示。

(1)在浏览器的地址栏中输入网址“`hp:/Code.Google.Com/intl/Zh-CN/javadevtools/downloadwipro.Html`”,按`Enter`键进入`WindowBuilder`插件的下载页面,根据`Eclipse`的版本,选择对应的更新网址。
(2)打开`Eclipse`,选择“帮助”/`InstallNewSoftware`命令,如图2.12所示
(3)多中输入在第(1)步中输入的网址,最后单击“确定”按钮,如图2.13所示。3)在打开的增加更新仓库对话框的`Name`文本框中输入“`WindowBuilder`”,在`Location`

## 实例010 开发计算器界面
计算器是各种操作系统提供的经典程序之一,在安装完`WindowBuilder`插件后,将演示如何使用它来开发计算器界面。实例的运行效果如图215所示。
### 实现过程
(1)在`Eclipse`中创建项目010,并在该项目中创建`com.mingrisoft`包。
(2)在`com.mingrisoft`包中创建`JFrame`类型的文件,名称为`Calculator`,并在屏幕下方选`Design`选项卡切换到设计界面。
(3)在窗体的顶部增加一个**文本框控件**,在窗体的中央增加一个面板,然后将该面板设置成4行4列的网格布局,并增加16个按钮,效果如图2.16所示。
(4)修改按钮上的文本内容及字体,调整窗体的大小,完毕后程序的运行效果如图2.15所示。

## 技术要点
`Swing`中控件上的文本非常灵活,不仅能够设置字体,还能够设置颜色。此外,还可以在按钮控件中使用`HIML`代码实现复杂的样式。
