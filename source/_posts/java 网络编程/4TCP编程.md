---
title: 4TCP编程
categories: 
- Java
- java 网络编程
date: 2018-08-17 14:51:52
updated: 2018-11-05 17:17:07
abbrlink: dfafaccc
---
- [客户端网络编程](/blog/dfafaccc/#客户端网络编程)
    - [第一步：建立连接](/blog/dfafaccc/#第一步：建立连接)
    - [第二步: 交换数据](/blog/dfafaccc/#第二步:-交换数据)
    - [第三步：关闭网络连接](/blog/dfafaccc/#第三步：关闭网络连接)
    - [实例](/blog/dfafaccc/#实例)
- [TCP客户端编程](/blog/dfafaccc/#TCP客户端编程)
    - [第一步：监听窗口](/blog/dfafaccc/#第一步：监听窗口)
    - [第二步：建立连接](/blog/dfafaccc/#第二步：建立连接)
    - [第三步：交换数据](/blog/dfafaccc/#第三步：交换数据)
    - [关闭连接](/blog/dfafaccc/#关闭连接)

<!--more-->
<input type="button" onclick="open_closeTOC()" id="showcloseButton">&nbsp;<input type="button" value="本文链接" onclick="copyPageURL();">
<script>
    function open_closeTOC() {var id = document.querySelector(".post-body > ul"); if (id.style.display == "block") {id.style.display = "none";document.getElementById("showcloseButton").value= "展开目录";}else if (id.style.display == "none") {id.style.display = "block";document.getElementById("showcloseButton").value="折叠目录";}}(function () {document.querySelector(".post-body > ul").style.display = "none";document.getElementById("showcloseButton").value="展开目录";})();  
    function copyPageURL() {const input = document.createElement('input');input.setAttribute('readonly', 'readonly');input.setAttribute('value', window.location.href);document.body.appendChild(input); input.select();if (document.execCommand("copy")) {alert("已复制: " + input.value)} document.body.removeChild(input);}
</script>

<!--end-->

按照前面的介绍，**网络通讯的方式有`TCP`和`UDP`两种**，其中`TCP`方式的网络通讯是指在通讯的过程中保持连接，有点类似于打电话，只需要拨打一次号码(建立一次网络连接)，就可以多次通话(多次传输数据)。这样方式在实际的网络编程中，由于传输可靠，类似于打电话，如果甲给乙打电话，乙说没有听清楚让甲重复一遍，直到乙听清楚为止，实际的网络传输也是这样，如果发送的一方发送的数据接收方觉得有问题，则网络底层会自动要求发送方重发，直到接收方收到为止。

在`Java`语言中，对于`TCP`方式的网络编程提供了良好的支持，在实际实现时，**以`java.net.Socket`类代表客户端连接，以`java.net.ServerSocket`类代表服务器端连接**。在进行网络编程时，底层网络通讯的细节已经实现了比较高的封装，所以在程序员实际编程时，只需要指定`IP`地址和`端口号码`就可以建立连接了。正是由于这种高度的封装，一方面简化了`Java`语言网络编程的难度，另外也使得使用`Java`语言进行网络编程时无法深入到网络的底层，所以使用`Java`语言进行网络底层系统编程很困难，具体点说，`Java`语言无法实现底层的网络嗅探以及获得`IP`包结构等信息。但是由于`Java`语言的网络编程比较简单，所以还是获得了广泛的使用。

在使用`TCP`方式进行网络编程时，需要按照前面介绍的网络编程的步骤进行，下面分别介绍一下**在`Java`语言中客户端和服务器端的实现步骤。**
## 客户端网络编程 ##
### 第一步：建立连接 ###
在客户端网络编程中，首先需要建立连接，在`Java API`中以`java.net.Socket`类的对象代表网络连接，**所以建立客户端网络连接，也就是创建`Socket`类型的对象**，该对象代表网络连接，示例如下：
```java
Socket socket1 = new Socket(“192.168.1.103”,10000);
Socket socket2 = new Socket(“github.com”,80);
```
上面的代码中，`socket1`实现的是连接到`IP`地址是`192.168.1.103`的计算机的`10000`号端口，而`socket2`实现的是连接到域名是`www.sohu.com`的计算机的`80`号端口，至于底层网络如何实现建立连接，对于程序员来说是完全透明的。如果建立连接时，本机网络不通，或服务器端程序未开启，则会抛出异常。
### 第二步: 交换数据 ###
连接一旦建立，则完成了客户端编程的第一步，紧接着的步骤就是按照“请求-响应”模型进行网络数据交换，在`Java`语言中，**数据传输功能由`Java IO`实现，也就是说只需要从连接中获得`输入流`和`输出流`即可**，然后`将需要发送的数据写入连接对象的输出流`中，在发送完成以后`从输入流中读取数据`即可。示例代码如下：
```
OutputStream os = socket1.getOutputStream(); //获得输出流，用来想服务发送请求
InputStream is = socket1.getInputStream();     //获得输入流,用来读取服务器的响应
```
上面的代码中，分别从`socket1`这个连接对象获得了输出流和输入流对象，在整个网络编程中，后续的数据交换就变成了`IO`操作，也就是遵循“`请求-响应`”模型的规定，**先向输出流中写入数据**，这些数据会被系统发送出去，**然后再从输入流中读取服务器端的反馈信息，这样就完成了一次数据交换过程**，当然这个数据交换过程可以多次进行。

这里获得的只是最基本的输出流和输入流对象，还可以根据前面学习到的`IO`知识，**使用流的嵌套将这些获得到的基本流对象转换成需要的装饰流对象，从而方便数据的操作。**

### 第三步：关闭网络连接 ###
最后当数据交换完成以后，关闭网络连接，释放网络连接占用的系统端口和内存等资源，完成网络操作，示例代码如下：
```
socket1.close();
```
### 实例 ###
这就是最基本的网络编程功能介绍。下面是一个简单的网络客户端程序示例，该程序的作用是向服务器端发送一个字符串“Hello”，并将服务器端的响应显示到控制台，数据交换只进行一次，当数据交换进行完成以后关闭网络连接，程序结束。实现的代码如下：
实例：
```
package tcp;

import java.io.*;
import java.net.*;

/**
 * 简单的Socket客户端
 * 功能为：发送字符串“Hello”到服务器端，并打印出服务器端的响应
 */
public class SimpleSocketClient
{
	public static void main(String[] args)
	{
		Socket socket = null;
		InputStream is = null;
		OutputStream os = null;
		// 服务器端IP地址
		String serverIP = "127.0.0.1";
		// 服务器端端口号
		int serverPort = 10000;
		// 发送内容
		String request = "Hello";
		try
		{
			// 第一步:建立连接
			socket = new Socket(serverIP, serverPort);
			
			// 第二步:交换数据
			// 获取输出流
			os = socket.getOutputStream();
			// 发送数据给服务器
			os.write(request.getBytes());
			// 接收服务器的数据
			is = socket.getInputStream();
			byte[] response = new byte[1024];
			int size = is.read(response);
			// 输出反馈数据
			System.out.println("服务器响应：" + new String(response, 0, size));
		} catch (Exception e)
		{
			e.printStackTrace(); // 打印异常信息
		} finally
		{
			if(os!=null)
			{
				try
				{
					os.close();
				} catch (IOException e)
				{
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			if(is!=null)
			{
				try
				{
					is.close();
				} catch (IOException e)
				{
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
			if(socket!=null)
			{
				try
				{
					socket.close();
				} catch (IOException e)
				{
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
	}
}
```
在该示例代码中`建立了一个连接到`IP`地址为`127.0.0.1`，端口号码为`10000`的`TCP`类型的网络连接`，然后获得连接的输出流对象，将需要发送的字符串“`Hello`”转换为`byte`数组写入到输出流中，由系统自动完成将输出流中的数据发送出去，如果需要强制发送，可以调用输出流对象中的`flush`方法实现。在数据发送出去以后，从连接对象的输入流中读取服务器端的反馈信息，读取时可以使用`IO`中的各种读取方法进行读取，这里使用最简单的方法进行读取，**从输入流中读取到的内容就是服务器端的响应**，并将读取到的内容在客户端的控制台进行输出，最后依次关闭打开的流对象和网络连接对象。

这是一个简单的功能示例，在该示例中演示了`TCP`类型的`网络客户端`基本方法的使用，该代码只起演示目的，还无法达到实用的级别。

## TCP客户端编程 ##

介绍完一个简单的客户端编程的示例，下面接着介绍一下`TCP`类型的服务器端的编写。首先需要说明的是，**客户端的步骤和服务器端的编写步骤不同**，所以在学习服务器端编程时注意不要和客户端混淆起来。
### 第一步：监听窗口 ###
在服务器端程序编程中，由于服务器端实现的是被动等待连接，所以服**务器端编程的第一个步骤是监听端口**，也就是监听是否有客户端连接到达。实现服务器端监听的代码为：
```
ServerSocket ss = new ServerSocket(10000);
```
该代码实现的功能是监听当前计算机的`10000`号端口，如果在执行该代码时，`10000`号端口已经被别的程序占用，那么将抛出异常。否则将实现监听。

### 第二步：建立连接 ###

服务器端编程的第二个步骤是获得连接**。该步骤的作用是当有客户端连接到达时，建立一个和客户端连接对应的`Socket`连 接对象，从而释放客户端连接对于服务器端端口的占用**。实现功能就像公司的前台一样，当一个客户到达公司时，会告诉前台我找某某某，然后前台就通知某某某， 然后就可以继续接待其它客户了。通过获得连接，使得客户端的连接在服务器端获得了保持，另外使得服务器端的端口释放出来，可以继续等待其它的客户端连接。 实现获得连接的代码是：
```
Socket socket = ss.accept();
```
该代码实现的功能是**获得当前连接到服务器端的客户端连接**。需要说明的是**`accept`和`IO`部分介绍的`read`方法一样，都是一个阻塞方法，也就是当无连接时，该方法将阻塞程序的执行，直到连接到达时才执行该行代码。**另外获得的连接会在服务器端的该端口注册，这样以后就可以通过在服务器端的注册信息直接通信，而注册以后服务器端的端口就被释放出来，又可以继续接受其它的连接了。
### 第三步：交换数据 ###
连接获得以后，后续的编程就和客户端的网络编程类似了，这里获得的Socket类型的连接就和客户端的网络连接一样了，只是**服务器端需要首先读取发送过来的数据，然后进行逻辑处理以后再发送给客户端，也就是交换数据的顺序和客户端交换数据的步骤刚好相反。**这部分的内容和客户端很类似，所以就不重复了，如果还不熟悉，可以参看下面的示例代码。

### 关闭连接 ###
最后，在服务器端通信完成以后，关闭服务器端连接。实现的代码为：
```
ss.close();
```
这就是基本的`TCP`类型的服务器端编程步骤。下面以一个简单的`echo`服务实现为例子，介绍综合使用示例。`echo`的意思就是“回声”，**`echo`服务器端实现的功能就是将客户端发送的内容再原封不动的反馈给客户端。**实现的代码如下：

```java
package tcp;
import java.io.*;
import java.net.*;
/**
 * echo服务器 功能：将客户端发送的内容反馈给客户端
 */
public class SimpleSocketServer
{
	public static void main(String[] args)
	{
		ServerSocket serverSocket = null;
		Socket socket = null;
		OutputStream out = null;
		InputStream in = null;
		// 监听端口号
		int port = 10000;
		try
		{
			// 建立连接
			serverSocket = new ServerSocket(port);
			// 获得连接
			socket = serverSocket.accept();
			// 接收客户端发送内容
			in = socket.getInputStream();
			byte[] recive = new byte[1024];
			int size = in.read(recive);
			// 输出
			System.out.println("客户端发送内容为：" + new String(recive, 0, size));
			// 向客户端发送反馈内容
			out = socket.getOutputStream();
			out.write(recive, 0, size);
		} catch (Exception e)
		{
			e.printStackTrace();
		} finally
		{
			try
			{
				// 关闭流和连接
				out.close();
				in.close();
				socket.close();
				serverSocket.close();
			} catch (Exception e)
			{
			}
		}
	}
}
```
在该示例代码中建立了一个监听当前计算机`10000`号端口的服务器端`Socket`连接，然后获得客户端发送过来的连接，如果有连接到达时，读取连接中发送过来的内容，并将发送的内容在控制台进行输出，输出完成以后将客户端发送的内容再反馈给客户端。最后关闭流和连接对象，结束程序。


### 运行客户端和服务端 ###：
因为在IDE中只有一个控制台窗口，所以运行效果不明显，所以这里再cmd命令行中编译运行简单点。

- 编译运行服务器
在cmd中编译服务器
```
javac -d . SimpleSocketServer.java
```
在cmd中运行服务器
```
java tcp.SimpleSocketServer
```
此时，服务器端将阻塞，等待客户端的连接。
![服务器等待客户端的连接](https://i.imgur.com/VcFSVEN.png)
- 编译运行客户端
在cmd中编译客户端
```
javac -d . SimpleSocketClient.java
```
在cmd中运行客户端
```
java tcp.SimpleSocketClient
```
![编译运行客户端](https://i.imgur.com/SV1h4R1.png)
运行结果：
![](https://i.imgur.com/mEFqwtO.png)

这样，就以一个很简单的示例演示了`TCP`类型的网络编程在`Java`语言中的基本实现，这个示例只是演示了网络编程的基本步骤以及各个功能方法的基本使用，只是为网络编程打下了一个基础，下面将就几个问题来深入介绍网络编程深层次的一些知识。
为了一步一步的掌握网络编程，下面再研究网络编程中的两个基本问题，通过解决这两个问题将对网络编程的认识深入一层。

>原文链接: [4TCP编程](https://www.lansheng.net.cn/blog/dfafaccc/)