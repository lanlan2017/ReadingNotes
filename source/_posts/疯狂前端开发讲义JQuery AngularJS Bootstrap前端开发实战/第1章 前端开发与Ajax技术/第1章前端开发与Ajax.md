---
title: 第1章前端开发与Ajax
categories: 
  - 疯狂前端开发讲义JQuery AngularJS Bootstrap前端开发实战
  - 第1章 前端开发与Ajax技术
date: 2019-05-29 17:31:30
updated: 2019-11-02 01:39:01
abbrlink: a5bcd8d
---
- [同步](/ReadingNotes/a5bcd8d/#同步)
- [异步](/ReadingNotes/a5bcd8d/#异步)
- [Ajax应用的工作过程](/ReadingNotes/a5bcd8d/#Ajax应用的工作过程)
- [JavaScript 使用Ajax过程](/ReadingNotes/a5bcd8d/#JavaScript-使用Ajax过程)
- [使用XMLHttpRequest对象发送请求步骤](/ReadingNotes/a5bcd8d/#使用XMLHttpRequest对象发送请求步骤)
- [传统Web应用发送请求形式](/ReadingNotes/a5bcd8d/#传统Web应用发送请求形式)
- [获取服务器响应生成的文本](/ReadingNotes/a5bcd8d/#获取服务器响应生成的文本)
- [获取服务器响应的状态码](/ReadingNotes/a5bcd8d/#获取服务器响应的状态码)
- [传统Web编程和Ajax编程的区别](/ReadingNotes/a5bcd8d/#传统Web编程和Ajax编程的区别)
    - [1.客户端发送请求的方式不同](/ReadingNotes/a5bcd8d/#1-客户端发送请求的方式不同)
    - [2.服务器生成的响应不同](/ReadingNotes/a5bcd8d/#2-服务器生成的响应不同)
    - [3.客户端加载响应的方式不同](/ReadingNotes/a5bcd8d/#3-客户端加载响应的方式不同)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
# 同步 #
每次用户发送请求,向服务器请求获得新数据时,**浏览器都会完全丢弃当前页面,而等待重新加载新的页面。而在服务器完全响应之前,用户浏览器将一片空白,用户的动作必须中断**。
# 异步 #
**异步是指用户发送请求后,无须等待,请求在后台发送,不会阻塞用户当前活动。用户无须等待第一次请求得到完全响应,即可发送第二次请求**。
# Ajax应用的工作过程 #
- `JavaScript`脚本使用`XMLHttpRequest`对象**向服务器发送请求**。发送请求时,既可以发送`GET`请求,也可以发送`POST`请求。
- `JavaScript`脚本使用`XMLHttpRequest`对象**解析服务器响应数据**。
- `JavaScript`脚本**通过`DOM`动态更新`HTML`页面**。也可以为服务器响应数据增加`CSS`样式表,在当前网页的某个部分加以显示。

# JavaScript 使用Ajax过程 #
`JavaScript`主要完成`Ajax`如下事情:
- 1.创建`XMLHttpRequest`对象。
- 2.通过`XMLHttpRequest`对象向服务器发送请求。
- 3.创建回调函数,监视服务器响应状态,在服务器响应完成后,回调函数将会被调用。
- 4.回调函数通过`DOM`动态更新`HTML`页面。


# 使用XMLHttpRequest对象发送请求步骤 #
一般而言，使用`XMLHttpRequest`对象发送请求应按如下步骤进行：
- 1.使用`open()`方法连接服务器`URL`。
- 2.调用`setRequestHeader()`方法为请求设置合适的请求头。根据不同的请求,可能需要设置不同的请求头。
- 3.为`load`事件注册事件处理函数。**当服务器响应返回时,`load`事件处理函数将会被触发**。
- 4.调用`send`()方法发送请求。

# 传统Web应用发送请求形式 #
- 在浏览器的地址栏中输入请求地址后按回车键发送`GET`请求。
- 提交表单发送`POST`或`GET`请求,具体发送何种请求取决于表单元素的`method`属性。

# 获取服务器响应生成的文本 #
`XMLHttpRequest`对象包含一个属性`responseText`,**该属性可获取服务器响应被生成的文本**
# 获取服务器响应的状态码 #
`XMLHttpRequest`对象提供了`status`属性,**该属性是服务器响应对应的状态码**,其中**`200`表明响应正常**,而404表明资源丢失,500表明内部错误等
# 传统Web编程和Ajax编程的区别 #
## 1.客户端发送请求的方式不同 ##
传统`Web`应用发送请求通常有两种方式:采用提交表单的方式发送`GET`请求或`POST`请求;让浏览器直接请求网络资源发送`GET`请求。在采用`Ajax`的现代`Web`应用中,应用需要使用`XMLHttpRequest`对象来发送请求。
## 2.服务器生成的响应不同 ##
在传统`Web`应用中,服务器的响应总是完整的`HTML`页面。在采用`Ajax`技术之后,服务器响应不再是完整的`HTML`页面,而只是必须更新的数据,因此服务器生成的响应可能只是简单的文本(当然也可以是`JSON`格式或`XML`格式的文本)。
## 3.客户端加载响应的方式不同 ##
**传统`Web`应用**具有每个请求对应一个页面的特点,而且服务器响应就是一个完整的`HTML`页面,所以**浏览器可以自动加载并显示服务器响应**。在**采用`Ajax`**技术后,服务器响应只是必须更新的数据,故**客户端必须通过程序来动态加载服务器响应**。

