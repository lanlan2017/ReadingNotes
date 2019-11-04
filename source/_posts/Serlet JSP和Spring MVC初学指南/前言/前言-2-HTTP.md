---
title: 前言-2-HTTP
categories: 
  - Serlet JSP和Spring MVC初学指南
  - 前言
date: 2019-04-25 14:56:06
updated: 2019-11-02 10:13:00
abbrlink: 8b8be5cf
---
- [前言-2-HTTP](/ReadingNotes/8b8be5cf/#前言-2-HTTP)
    - [HTTP](/ReadingNotes/8b8be5cf/#HTTP)
        - [HTTP请求](/ReadingNotes/8b8be5cf/#HTTP请求)
        - [**HTTP**响应](/ReadingNotes/8b8be5cf/#HTTP响应)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
# 前言-2-HTTP #
## HTTP ##
**`HTTP`协议使得`Web`服务器与浏览器之间可以通过互联网或内网进行数据交互**。万维网联盟（W3C）， 作为一个制定标准的国际社区，负责和维护`HTTP`协议。`HTTP`第一个版本是`HTTP0.9`，之后是`HTTP 1.0`，当前最新版本是`HTTP 1.1`。`HTTP 1.1`版本的`RFC`编号是2616，下载地址为[http://www.w3.org/Protocols/HTTP/1.1/rfc2616.pdf](http://www.w3.org/Protocols/HTTP/1.1/rfc2616.pdf)。按计划，`HTTP`的下一个版本是`HTTP/2`。

`Web`服务器7×24小时不间断运行，并等待`HTTP`客户端（通常是`Web`浏览器）来连接并请求资源。通常， 由客户端发起一个连接，服务端不会主动连接客户端。
> **注意**
> 2011年，标准化组织`IETF`发布了`WebSocket`协议，即`RFC 6455`规范。该协议允许一个`HTTP`连接升级为`WebSocket`连接，支持双向通信，这就使得服务端可以通过`WebSocket`协议主动发起同客户端的会话通信。

**互联网用户需要通过点击一个链接或者在地址栏之中输入一个`URL`地址来访问一个资源**，如下为两个示例：

```URL
http://google.com/index.html
http://facebook.com/index.html
```
**`URL`的第一个部分是**`http`，代表所采用的**协议**。除 `HTTP`协议外，`URL`还可以采用其他类型,下面为两个示例：
```
protocol://[host.]domain[:port][/context][/resource][?query string]
```
或者
```
protocol://IP address[:port][/context][/resource][?query string]
```
中括号中的内容是可选的，因此一个最简的`URL`是` http://yahoo.ca` 或者`http://192.168.1.9` 。
需要说明的是，除了输入[http://google.com](http://google.com)，你还可以用[http://209.85.143.99](http://209.85.143.99)来访问谷歌。可以用`ping`命令来获取域名所对应的`IP`地址： 
```cmd
ping google.com
```
由于`IP`地址不容易记忆，实践中更倾向于使用域名。一台计算机可以托管不止一个域名，因此不同的域名可能指向同一个`IP`。另外，`example.com`或者 `example.org`无法被注册，因为它们被保留作为各类文档手册举例使用。
`URL`中的`Host`部分用来表示在互联网或内网中一个唯一的地址，例如：`http://yahoo.com`（没有host）所访问的地址完全不同于`http://mail.yahoo.com` （有host）。 多年以来，作为最受欢迎的主机名，`www`是默认的主机名，通常，`http://www.domainName` 会被映射到`http://domainName` 。

**`HTTP`的默认端口是80端口**。因此，对于采用80端口的`Web`服务器，可以无须输入端口号。但有时候， `Web`服务器并未运行在80端口上，此时必须输入相应的端口号。例如：**`Tomcat`服务器的默认端口号是8080**， 为了能正确访问，必须提供输入端口号：
```URL
http://localhost:8080
```
**`localhost`作为一个保留关键字，用于指向本机**。
`URL`中的`context`部分用来代表应用名称，该部分也是可选的。一台`Web`服务器可以运行多个上下文（应用），其中一个可以配置为默认上下文，对于访问默认上下文中的资源，可以跳过`context`部分。

最后，一个`context`可以有一个或多个默认资源（通常为`index.html`，`index.htm`或者`default.htm`）。一个没有带资源名称的`URL`通常指向默认资源。当存在多个默认资源时，其中最高优先级的资源将被返回给客户端。

在资源名之后可以有一个或多个查询语句或者路径参数。查询语句是一个`Key/Value`组，多个查询语句间用“`&`”分隔。路径参数类似于查询语句，但只有 `value`部分，多个`value`部分用“`/`”符号分隔。

### HTTP请求 ###
一个`HTTP`请求包含三部分内容： 
- 方法-`URI-`协议/版本 
- 请求头信息 
- 请求正文如下为一个具体示例：

```HTTP
POST /examples/default.jsp HTTP/1.1 
Accept: text/plain; text/html 
Accept-Language: en-gb 
Connection: Keep-Alive Host:localhost 
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKi t/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36 
Content-Length: 30 
Content-Type: application/x-www-form-urlencoded 
Accept-Encoding: gzip, deflate 

lastName=Blanks&firstName=Mike
```
请求的第一行即是：方法-URI-协议/版本 
```HTTP
POST /examples/default.jsp HTTP/1.1
```
请求方法为`POST`，`URI`为`/examples/default.jsp`，而协议/版本为`HTTP/1.1`。

**`HTTP 1.1`规范`定义了7种类型的方法`，包括`GET`、 `POST`、`HEAD`、`OPTIONS`、`PUT`、`DELETE`以及 `TRACE`，其中`GET`和`POST`广泛应用于互联网应用。**

`URI`定义了一个互联网资源，**通常解析为服务器根目录的相对路径。因此，通常用`/`符号打头**。另外**`URL`是`URI`的一个具体类型**。（详见 [http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)。）

`HTTP`请求所包含的请求头信息包含关于客户端环境以及实体内容等非常有用的信息。例如，浏览器所设置的语言实体内容长度等。**每个`header`用回车/换行（即 `CRLF`）分隔**。
**`HTTP`请求头`信息和`请求正文``用一行空行分隔`**， `HTTP`服务器据此判断请求正文的起始位置。因此在一些关于互联网的书籍中，`CRLF`作为`HTTP`请求的第四种组件。 在此前所举的例子中，请求正文如下行：
```HTTP
lastName=Blanks&firstName=Mike
```
在正常的`HTTP`请求中，请求正文的内容不止如此。
### `HTTP`响应  ###
同`HTTP`请求一样，`HTTP`响应包含三部分： 
- 协议—状态码—描述 
- 响应头信息 
- 响应正文

如下是一个`HTTP`响应实例：

```HTTP
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1 
Date: Thu, 8 Jan 2015 13:13:33 GMT
Content-Type: text/html
Last-Modified: Wed, 7 Jan 2015 13:13:12 GMT 
Content-Length: 112 

<html>
<head>
    <title>HTTP Response Example</title>
</head>
<body>
    Welcome to Brainy Software
</body>
</html>
```

类似于`HTTP`请求报文，`HTTP`响应报文第一行:
```HTTP
HTTP/1.1 200 OK
```
说明 了`HTTP`协议的版本是1.1，并且请求结果是成功的（状态代码200为响应成功）。

同`HTTP`请求报文头信息一样，`HTTP`响应报文的`响应头信息`也包含了大量有用的信息。
`HTTP`响应报文的`响应正文`是`HTML`文档。**`HTTP`响应报文的响应头信息和响应正文之间也是用`\r\n`(CRLF)分隔的**。

**状态代码200表示Web服务器能正确响应所请求的资源**。若一个请求的资源不能被找到或者理解，则`Web `服务器将返回不同的状态代码。例如：`访问未授权的资 源将返回401`，`而使用被禁用的请求方法将返回405`。完 整的HTTP响应状态代码列表详见如下网址：
[http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

