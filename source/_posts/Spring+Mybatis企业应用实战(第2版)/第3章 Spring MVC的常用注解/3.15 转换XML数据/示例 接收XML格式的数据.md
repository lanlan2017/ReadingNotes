---
title: 示例 接收XML格式的数据
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.15 转换XML数据
date: 2019-08-21 00:20:01
updated: 2019-11-02 01:39:00
abbrlink: bcd788ad
---
- [示例 接收XML格式的数据](/ReadingNotes/bcd788ad/#示例-接收XML格式的数据)
    - [sendxml.jsp](/ReadingNotes/bcd788ad/#sendxml-jsp)
    - [Book.java](/ReadingNotes/bcd788ad/#Book-java)
- [示例 返回XML格式的数据](/ReadingNotes/bcd788ad/#示例-返回XML格式的数据)
    - [readxml.jsp](/ReadingNotes/bcd788ad/#readxml-jsp)

<!--more-->
<script src="https://cdn.bootcss.com/jquery/3.4.0/jquery.slim.min.js"></script>
<script>$(document).ready(function () {$(".post-body > ul:nth-child(1)").hide();});</script>

<!--end-->
<!--SSTStart-->
# 示例 接收XML格式的数据 #
创建一个`XmlTest`项目,在`WebContent`目录下创建一个`js`目录,加入`jQuery`和`json2`的`js`文件。
<!--replace:sendxml=send XML&xml=X M L-->

## sendxml.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试接收XML格式的数据</title>
<script type="text/javascript" src="js/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="js/json2.js"></script>
<script type="text/javascript">
	$(document).ready(function() {
		sendxml();
	});
	function sendxml() {
		var xmlData = "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><book><id>1</id><name>书的名称</name><author>作者</author></book>";
		$.ajax("${pageContext.request.contextPath}/sendxml",// 发送请求的URL字符串。
		{
			type : "POST", //  请求方式 POST或GET
			contentType : "application/xml", //  发送信息至服务器时的内容编码类型
			// 发送到服务器的数据。
			data : xmlData,
			async : true, // 默认设置下，所有请求均为异步请求。如果设置为false，则发送同步请求
		});
	}
</script>
</head>
<body>
</body>
</html>
```
<!--replace:sendxml=send xml-->
`sendxml.jsp`页面代码分析如下:
(1)页面使用`jQuery`发送`JSON`数据,在页面的`<head>`部分,引入了`jQuery`和`json2`的js文件
(2)载入页面时调用`sendxml`函数。
(3)`sendxml`函数发送异步请求到`"sendxml"`,
- `ajax`方法的contentType选项:`contentType:"application/xml"`表示发送的内容编码格式为`XML`;
- `ajax`方法的`data`选项表示要发送的数据是`XML`数据。

## Book.java ##
```java
package org.fkit.domain;

import java.io.Serializable;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.bind.annotation.XmlRootElement;

// @XmlRootElement表示XML文档的根元素
@XmlRootElement
public class Book implements Serializable
{
	private static final long serialVersionUID = 1L;
	private Integer id;
	private String name;
	private String author;
	public Book()
	{
		super();
	}
	public Book(Integer id, String name, String author)
	{
		super();
		this.id = id;
		this.name = name;
		this.author = author;
	}
	public Integer getId()
	{
		return id;
	}
	// 该属性作为xml的element
	@XmlElement
	public void setId(Integer id)
	{
		this.id = id;
	}

	public String getName()
	{
		return name;
	}
	@XmlElement
	public void setName(String name)
	{
		this.name = name;
	}
	public String getAuthor()
	{
		return author;
	}
	@XmlElement
	public void setAuthor(String author)
	{
		this.author = author;
	}
	@Override
	public String toString()
	{
		return "Book [id=" + id + ", name=" + name + ", author=" + author + "]";
	}
}
```
在`Book`类中定义了3个属性:`id`、`nane`和`author`,分别对应`XML`的元素。 `toString`方法用来输出获取的数据对象信息。
```java
package org.fkit.controller;

import java.io.InputStream;
import javax.xml.bind.JAXBContext;
import javax.xml.bind.Unmarshaller;
import org.fkit.domain.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class BookController
{
	// @RequestBody Book book会将传递的xml数据自动绑定到Book对象
	@PostMapping(value = "/sendxml")
	public void sendxml(@RequestBody Book book)
	{
		System.out.println("接收XML数据成功");
		System.out.println(book);
	}
	// @ResponseBody 会将Book自动转成XML数据返回
	@PostMapping(value = "/readxml")
	// @ResponseBody注解把方法返回的Book对象转换成XML并发给客户端.
	@ResponseBody
	public Book readXml() throws Exception
	{
		// 通过JAXBContext的newInstance方法，传递一个class就可以获得一个上下文
		JAXBContext context = JAXBContext.newInstance(Book.class);
		// 创建一个Unmarshall对象
		Unmarshaller unmar = context.createUnmarshaller();
		// 读取资源目录下的文件
		InputStream is = this.getClass().getResourceAsStream("/book.xml");
		// Unmarshall对象的unmarshal方法可以进行xml到Java对象的转换
		Book book = (Book) unmar.unmarshal(is);
		System.out.println(book);
		return book;
	}
}
```
`sendxml`方法中的第一个参数`@RequestBody Book book`表示,使用`@RequestBody`注解获取到`XML`数据后,将`XML`数据设置到`Book`对象的对应属性中。为了测试接收数据,将接收到XML数据的`Book`对象打印在控制台上。
`springmvc-config.xml`文件和`JsonRequestTest`项目的一致,重点在于`<mvc:annotation-driven />`,该配置默认装配了`Jaxb2RootElementHttpMessageConverter`来处理`XML`数据的转换。
部署`XmlTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/XmlTest/sendxml.jsp
```
载λ `sendxml.jsp`页面时会发送`Ajax`请求,传递`XML`数据。`BookController`接收到请求后,`@RequestBody`注解会将`XML`数据设置到`Book`参数对应的属性中。控制台输出如下:
```
接收XML数据成功
Book [id=1, name=书的名称, author=作者]
```
可以看到,`XML`数据传递的`id`、`name`、 `author`元素被赋值到了`Book`对象对应的属性当中。
# 示例 返回XML格式的数据 #
<!--replace:readxml=read X M L-->
## readxml.jsp ##
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试返回XML格式的数据</title>
<script type="text/javascript" src="js/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="js/json2.js"></script>
<script type="text/javascript">
	$(document).ready(function() {
		readxml();
	});
	function readxml() {
		$.ajax("${pageContext.request.contextPath}/readxml",// 发送请求的URL字符串。
		{
			dataType : "text", // 预期服务器返回的数据类型。
			type : "POST", //  请求方式 POST或GET
			async : true, // 默认设置下，所有请求均为异步请求。如果设置为false，则发送同步请求
			// 请求成功后的回调函数。
			success : function(xml) {
				// 获得xml数据的id，name，author
				var id = $("id", xml).text();
				var name = $("name", xml).text();
				var author = $("author", xml).text();
				var tr = $("<tr align='center'/>");
				$("<td/>").html(id).appendTo(tr);
				$("<td/>").html(name).appendTo(tr);
				$("<td/>").html(author).appendTo(tr);
				$("#booktable").append(tr);
			},
			// 请求出错时调用的函数
			error : function() {
				alert("数据接收失败");
			}
		});
	}
</script>
</head>
<body>
    <table id="booktable" border="1" style="border-collapse: collapse;">
        <tr align="center">
            <th>编号</th>
            <th>书名</th>
            <th>作者</th>
        </tr>
    </table>
</body>
</html>
```
`readxml.jsp`页面代码分析如下:
(1)页面使用`jQuery`发送M数据,在页面的`<head>`部分,引入了`jQuery`和`json2`的js文件。
(2)载入页面时调用`readxml`函数。
(3) `readxml`函数发送异步请求到`readxml`,请求成功将返回一个`XML`数据,接到返回的数据后将`XML`数据中的元素读取出来并将其设置到页面的`<span>`中。
`BookController`的`readxml`方法使用`JAXB`读取一个`XML`文件的数据并生成一个`Book`对象返回。`@ResponseBody`会将`Book`对象转换成`XML`数据返回到前台`JSP`页面。
在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/XmlTest/readxml.jsp
```
浏览器显示内容如下:
```
编号 	书名 	作者
1	书的名称	书的作者
```
这表示`Spring MVC`成功将`XML`数据返回到客户端。
<!--SSTStop-->

