---
title: 第1章 Java语言概述
categories: 
  - 7 Java经典编程300例
  - 第1章 Java语言概述
date: 2020-09-06 08:41:29
updated: 2020-09-06 08:41:29
abbrlink: 4259985c
---
<div id='my_toc'></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第1章 Java语言概述
本章读者可以学到如下实例:
- 实例001 输出“HelloWorld”
- 实例002 输出控制台传递的参数
- 实例003 输出由“*”组成的三角形
- 实例004 输出符号表情

## 实例001 输出“HelloWorld”
```java
package com.mingrisoft;

public class Test {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
## 实例002 输出控制台传递的参数
```java
package com.mingrisoft;

public class Test {
    public static void main(String[] args) {
        System.out.println(args[0]);
        System.out.println(args[1]);
    }
}
```
## 实例003 输出由“*”组成的三角形
```java
package com.mingrisoft;

public class Test {
    public static void main(String[] args) {
        System.out.println("   *");
        System.out.println("  ***");
        System.out.println(" *****");
        System.out.println("*******");
    }
}
```
#### 实例004 输出符号表情
```java
package com.mingrisoft;

public class Test {
    public static void main(String[] args) {
        System.out.println("  ╭︿︿︿╮ ");
        System.out.println("   {/ o  o /}");
        System.out.println("    ( (oo) )");
        System.out.println("    ︶ ︶︶");
    }

}
```