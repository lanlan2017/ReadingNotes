---
title: 第1章 jQuery入门 1.1 jQuery能做什么
categories: 
  - jQuery基础教程 第4版
  - 第1章 jQuery入门
date: 2019-06-29 21:19:28
updated: 2019-12-17 01:44:33
abbrlink: 938adc5f
---
<div id='my_toc'><a href="/ReadingNotes/938adc5f/#第1章-jQuery入门" class="header_1">第1章 jQuery入门</a><br><a href="/ReadingNotes/938adc5f/#1.1-jQuery能做什么" class="header_2">1.1 jQuery能做什么</a><br><a href="/ReadingNotes/938adc5f/#小结" class="header_2">小结</a><br></div>
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
# 第1章 jQuery入门 #
本章将介绍如下内容:

1. `jQuery`的主要特点;
2. 建立`jQuery`编码环境;
3. 简单`jQuery`脚本示例;
4. 选择`jQuery`而不是纯`JavaScript`的理由;
5. 常用`JavaScript`开发工具.

## 1.1 jQuery能做什么 ##

1. **取得文档中的元素**。如果不使用`JavaScript`库,遍历`DOM(Document Object Model`,文档对象模型)树, 以及查找`HTML`文档结构中某个特殊的部分,必须编写很多行代码。 `jQuery`为准确地获取需要检查或操纵的文档元素,提供了可靠而富有效率的选择符机制。
```javascript
$('div.content').find('p');
```
2. **修改页面的外观**。`CSS`虽然为影响文档呈现的方式提供了一种强大的手段,但当所有浏览器不完全支持相同的标准时,单纯使用`CSS`就会显得力不从心。 `jQuery`可以弥补这一不足,它提供了跨浏览器的标准解决方案。而且,即使在页面已经呈现之后,`jQuery`仍然能够改变文档中某个部分的类或者个别的样式属性。
```javascript
$('ul > li:first').addClass('active');
```
3. **改变文档的内容**。jQuery能够影响的范围并不局限于简单的外观变化,使用少量的代码,jQuery就能改变文档的内容。可以改变文本、插入或翻转图像、列表重新排序,甚至对HTML文档的整个结构都能重写和扩充——所有这些只需一个简单易用的API。
```javascript
$('#container').append('<a href="more.html">more</a>');
```
4. **响应用户的交互操作**。即使是最强大和最精心设计的行为,如果我们无法控制它何时发生,那它也毫无用处。`jQuery`提供了截获形形色色的页面事件(比如用户单击某个链接)的适当方式,而不需要使用事件处理程序拆散`HTML`代码。此外,它的事件处理`API`也消除了经常困扰`Web`开发人员浏览器的不一致性。
```javascript
$('button.show-details').click(function() {
  $('div.details').show();
});
```
5. **为页面添加动态效果**。为了实现某种交互式行为,设计者也必须向用户提供视觉上的反馈。`jQuery`中内置的一批淡入、擦除之类的效果,以及制作新效果的工具包,为此提供了便利.
```javascript
$('div.details').slideDown();
```
6. **无需刷新页面从服务器获取信息**。这种编程模式就是众所周知的`Ajax(Asynchronous JavaScript and XML`,异步`JavaScript`和`XML`),它是一系列在客户端和服务器之间传输数据的强大技术。`jQuery`通过消除这一过程中的浏览器特定的复杂性,使开发人员得以专注于服务器端的功能设计,从而得以创建出反应灵敏、功能丰富的网站。
```javascript
$('div.details').load('more.html #content');
```
7. **简化常见的`JavaScript`任务**。除了这些完全针对文档的特性之外,`jQuery`也改进了对基本的`JavaScript`数据结构的操作(例如迭代和数组操作等)。
```javascript

$.each(obj, function(key, value) { 
  total += value; 
});
```
## 小结 ##
使用`jQuery`可以做如下事情:
1. 取得文档中的元素
2. 修改页面的外观
3. 改变文档的内容
4. 响应用户的交互操作
5. 为页面添加动态效果
6. 无需刷新页面从服务器获取信息
7. 简化常见的`JavaScript`任务

