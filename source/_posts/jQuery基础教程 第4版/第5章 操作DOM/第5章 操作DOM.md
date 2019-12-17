---
title: 第5章 操作DOM
categories: 
  - jQuery基础教程 第4版
  - 第5章 操作DOM
date: 2019-07-20 22:41:16
updated: 2019-11-02 10:12:04
abbrlink: 9f710941
---
<div id='my_toc'><a href="/ReadingNotes/9f710941/#第5章-操作DOM" class="header_1">第5章 操作DOM</a><br></div>
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
<!--SSTStart-->
# 第5章 操作DOM #
所谓`Web`体验,就是`Web`服务器与`Web`浏览器之间合作的结果。过去,都是由服务器生成`HTML`文档,然后浏览器负责解释并显示该文档。后来,正如我们所看到的,这种情况发生了变化,我们可以用`CSS`技术来动态修改页面的外观。然而,要想把`JavaScript`的威力真正发挥出来,还得学会修改文档本身。
本章将学习以下内容:
1. 利用`DOM`提供的接口修改文档;
2. 在网页中根据需要创建元素和文本;
3. 移动或删除元素;
4. 通过添加、删除或修改它们的属性来实现文档内容的变换。
<!--SSTStop-->


