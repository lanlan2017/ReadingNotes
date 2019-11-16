---
title: UDP网络编程
categories: 
- Java
- java 网络编程
date: 2018-08-18 15:50:10
updated: 2018-11-05 17:17:07
abbrlink: b6cecc51
---
- [Java UDP网络编程相关类](/blog/b6cecc51/#Java-UDP网络编程相关类)
    - [DatagramSocket类](/blog/b6cecc51/#DatagramSocket类)
    - [`DatagramPacket`类](/blog/b6cecc51/#`DatagramPacket`类)
- [UDP客户端编程步骤](/blog/b6cecc51/#UDP客户端编程步骤)
    - [建立连接](/blog/b6cecc51/#建立连接)
    - [发送数据](/blog/b6cecc51/#发送数据)
    - [客户端接收数据](/blog/b6cecc51/#客户端接收数据)
    - [关闭](/blog/b6cecc51/#关闭)
- [UDP服务端网络编程](/blog/b6cecc51/#UDP服务端网络编程)
    - [第一步监听窗口，建立连接](/blog/b6cecc51/#第一步监听窗口，建立连接)
    - [第二步：接收客户端的数据](/blog/b6cecc51/#第二步：接收客户端的数据)
    - [第三步：处理接收的数据，给出响应](/blog/b6cecc51/#第三步：处理接收的数据，给出响应)
- [实例](/blog/b6cecc51/#实例)
- [多次发送多次接收](/blog/b6cecc51/#多次发送多次接收)
    - [情况：得不到服务器的响应，一直阻塞](/blog/b6cecc51/#情况：得不到服务器的响应，一直阻塞)

<!--more-->
<input type="button" onclick="open_closeTOC()" id="showcloseButton">&nbsp;<input type="button" value="本文链接" onclick="copyPageURL();">
<script>
    function open_closeTOC() {var id = document.querySelector(".post-body > ul"); if (id.style.display == "block") {id.style.display = "none";document.getElementById("showcloseButton").value= "展开目录";}else if (id.style.display == "none") {id.style.display = "block";document.getElementById("showcloseButton").value="折叠目录";}}(function () {document.querySelector(".post-body > ul").style.display = "none";document.getElementById("showcloseButton").value="展开目录";})();  
    function copyPageURL() {const input = document.createElement('input');input.setAttribute('readonly', 'readonly');input.setAttribute('value', window.location.href);document.body.appendChild(input); input.select();if (document.execCommand("copy")) {alert("已复制: " + input.value)} document.body.removeChild(input);}
</script>

<!--end-->
参考：[https://blog.csdn.net/sihai12345/article/details/79334299](https://blog.csdn.net/sihai12345/article/details/79334299)

网络通讯的方式除了`TCP`方式以外，还有一种实现的方式就是`UDP`方式。`UDP(User Datagram Protocol)`，中文意思是**用户数据报协议**，方式类似于发短信息，是一种物美价廉的通讯方式，使用**该种方式无需建立专用的虚拟连接**，由于无需建立专用的连接，所以**对于服务器的压力要比`TCP`小很多**，所以也是一种常见的网络编程方式。但是使用**该种方式最大的不足是传输不可靠**，当然也不是说经常丢失，就像大家发短信息一样，理论上存在收不到的可能，这种可能性可能是`1%`，反正比较小，但是由于这种可能的存在，所以平时我们都觉得重要的事情还是打个电话吧(类似`TCP`方式)，一般的事情才发短信息(类似`UDP`方式)。网络编程中也是这样，**必须要求可靠传输的信息一般使用`TCP`方式实现，一般的数据才使用`UDP`方式实现。**

`UDP`方式的网络编程也在`Java`语言中获得了良好的支持，由于其在传输数据的过程中不需要建立专用的连接等特点，所以在`Java API`中设计的实现结构和`TCP`方式不太一样。当然，需要使用的类还是包含在`java.net`包中。
## Java UDP网络编程相关类 ##
在`Java API`中，实现`UDP`方式的编程，包含`客户端网络编程`和`服务器端网络编程`，主要由两个类实现，分别是：

### DatagramSocket类 ###

`DatagramSocket`类实现“**网络连接**”，包括客户端网络连接和服务器端网络连接。虽然UDP方式的网络通讯不需要建立专用的网络连接，但是毕竟还是需要发送和接收数据，**`DatagramSocket`实现的就是发送数据时的发射器，以及接收数据时的监听器的角色。**类比于TCP中的网络连接，该类既可以用于实现客户端连接，也可以用于实现服务器端连接。

### `DatagramPacket`类 ###
**`DatagramPacket`类实现对于网络中传输的数据封装**，也就是说，**该类的对象代表网络中交换的`数据`**。
**在`UDP`方式的网络编程中，无论是需要发送的数据还是需要接收的数据，都必须被处理成`DatagramPacket`类型的对象**，该对象中包含`发送到的地址`、`发送到的端口号`以及`发送的内容`等。其实`DatagramPacket`类的作用类似于现实中的信件，在信件中包含信件发送到的地址以及接收人，还有发送的内容等，邮局只需要按照地址传递即可。在接收数据时，接收到的数据也必须被处理成`DatagramPacket`类型的对象，在该对象中包含发送方的地址、端口号等信息，也包含数据的内容。和`TCP`方式的网络传输相比，**`IO`编程在`UDP`方式的网络编程中变得不是必须的内容**，结构也要比`TCP`方式的网络编程简单一些。

下面介绍一下UDP方式的网络编程中，客户端和服务器端的实现步骤，以及通过基础的示例演示UDP方式的网络编程在Java语言中的实现方式。

UDP方式的网络编程，编程的步骤和TCP方式类似，只是使用的类和方法存在比较大的区别，下面首先介绍一下UDP方式的网络编程客户端实现过程。
## UDP客户端编程步骤 ##
UDP客户端编程涉及的步骤也是4个部分：**建立连接**、**发送数据**、**接收数据**和**关闭连接**。
### 建立连接 ###
首先介绍UDP方式的网络编程中建立连接的实现。其中**UDP方式的建立连接和TCP方式不同，只需要建立一个连接对象即可，不需要指定服务器的IP和端口号码**。实现的代码为：
```
DatagramSocket ds = new DatagramSocket();
```
这样就建立了一个客户端连接，**该客户端连接使用系统随机分配的一个本地计算机的未用端口号**。在该连接中，不指定服务器端的IP和端口，所以UDP方式的网络连接更像一个发射器，而不是一个具体的连接。
当然，可以通过制定连接使用的端口号来创建客户端连接。
```
DatagramSocket ds = new DatagramSocket(5000);
```
这样就是使用本地计算机的`5000`号端口建立了一个连接。**一般在建立客户端连接时没有必要指定端口号码。**
### 发送数据 ###
接着，介绍一下UDP客户端编程中发送数据的实现。**在UDP方式的网络编程中，IO技术不是必须的**，**发送数据步骤：**

- 需要将需要发送的数据内容首先转换为`byte`数组，
- 然后将`数据内容`、`服务器IP`和`服务器端口号`一起构造成一个`DatagramPacket`类型的对象，这样数据的准备就完成了，
- 发送时调用网络连接对象中的send方法发送该对象即可。

例如将字符串“`Hello`”发送到IP是`127.0.0.1`，端口号是`10001`的服务器，则实现发送数据的代码如下：
```java
String s = “Hello”;
String host = “127.0.0.1”;
int port = 10001;
//将发送的内容转换为byte数组
byte[] byteToSend = s.getBytes();
//将服务器IP转换为InetAddress对象
InetAddress serverIP = InetAddress.getByName(host);
//构造发送的数据包对象,数据包中放入数据，目的地址，目的端口号
DatagramPacket sendDp = new DatagramPacket(byteToSend,byteToSend.length,serverIP,port);
//发送数据
ds.send(sendDp);
```
在该示例代码中，不管发送的数据内容是什么，都需要转换为byte数组，然后将服务器端的IP地址构造成InetAddress类型的对象，在准备完成以后，将这些信息构造成一个DatagramPacket类型的对象，发送的数据内容、服务器端的IP和端口号，都包含在DatagramPacket对象中。在准备完成以后，调用连接对象ds的send方法把DatagramPacket对象发送出去即可。

按照UDP协议的约定，在进行数据传输时，系统只是尽全力传输数据，但是并不保证数据一定被正确传输，**如果数据在传输过程中丢失，那就丢失了。**

UDP方式在进行网络通讯时，也遵循“**请求-响应**”模型，**在发送数据完成以后，就可以接收服务器端的反馈数据了。**
### 客户端接收数据 ###
下面介绍一下UDP客户端编程中接收数据的实现。当数据发送出去以后，就可以接收服务器端的反馈信息了。**接收数据在Java语言中的实现是这样的：**
- 首先构造一个数据缓冲数组，该数组用于存储接收的服务器端反馈数据，该数组的长度必须大于或等于服务器端反馈的实际有效数据的长度。
- 然后以该缓冲数组为基础构造一个DatagramPacket数据包对象，
- 最后调用连接对象的receive方法接收数据即可。

接收到的服务器端反馈数据存储在DatagramPacket类型的对象内部。实现接收数据以及显示服务器端反馈内容的示例代码如下：
```java
//第一步,构造缓冲数组用于接收数据
byte[] data = new byte[1024];
//第二步,构造数据包对象
DatagramPacket received = new DatagramPacket(data,data.length);
//接收数据
ds.receive(receiveDp);
//输出数据内容
byte[] b = receiveDp.getData(); //获得缓冲数组
int len = receiveDp.getLength(); //获得有效数据长度
String s = new String(b,0,len);
System.out.println(s);
```
在该代码中，首先构造缓冲数组`data`，这里设置的长度`1024`是预估的接收到的数据长度，要求该长度必须大于或等于接收到的数据长度，然后以该缓冲数组为基础，构造数据包对象，使用连接对象`ds`的`receive`方法接收反馈数据，由于在`Java`语言中，除`String`以外的其它对象都是按照地址传递，所以在`receive`方法内部可以改变数据包对象`receiveDp`的内容，这里的`receiveDp`的功能和返回值类似。数据接收到以后，只需要从数据包对象中读取出来就可以了，使用`DatagramPacket`对象中的`getData`方法可以获得数据包对象的缓冲区数组，但是缓冲区数组的长度一般大于有效数据的长度，换句话说，也就是缓冲区数组中只有一部分数据是反馈数据，所以需要使用`DatagramPacket`对象中的`getLength`方法获得有效数据的长度，则有效数据就是缓冲数组中的前有效数据长度个内容，这些才是真正的服务器端反馈的数据的内容。
### 关闭 ###
UDP方式客户端网络编程的最后一个步骤就是关闭连接。虽然UDP方式不建立专用的虚拟连接，但是连接对象还是需要占用系统资源，所以在使用完成以后必须关闭连接。关闭连接使用连接对象中的close方法即可，实现的代码如下：
```
ds.close();
```
需要说明的是，和TCP建立连接的方式不同，UDP方式的同一个网络连接对象，可以发送到达不同服务器端IP或端口的数据包，这点是TCP方式无法做到的。
## UDP服务端网络编程 ##
介绍完了`UDP`方式客户端网络编程的基础知识以后，下面再来介绍一下`UDP`方式服务器端网络编程的基础知识。

`UDP`方式网络编程的服务器端实现和`TCP`方式的服务器端实现类似，也是服务器端监听某个端口，然后获得数据包，进行逻辑处理以后将处理以后的结果反馈给客户端，最后关闭网络连接，下面依次进行介绍。
### 第一步监听窗口，建立连接 ###
首先`UDP`方式服务器端网络编程需要建立一个连接，该连接监听某个端口，实现的代码为：
```
DatagramSocket ds = new DatagramSocket(10010);
```
由于**服务器端的端口需要固定，所以一般在建立服务器端连接时，都指定端口号。**例如该示例代码中指定10010端口为服务器端使用的端口号，客户端端在连接服务器端时连接该端口号即可。
### 第二步：接收客户端的数据 ###
接着服务器端就开始接收客户端发送过来的数据，其接收的方法和客户端接收的方法一直，其中`receive`方法的作用类似于`TCP`方式中`accept`方法的作用，该方法也是一个阻塞方法，其作用是接收数据。
### 第三步：处理接收的数据，给出响应 ###
接收到客户端发送过来的数据以后，服务器端对该数据进行逻辑处理，然后将处理以后的结果再发送给客户端，**在这里发送时就比客户端要麻烦一些，因为服务器端需要获得客户端的IP和客户端使用的端口号**，这个都可以`从接收到的数据包中获得`。示例代码如下：
```java
//获得客户端的IP
InetAddress clientIP = receiveDp.getAddress();
//获得客户端的端口号
Int clientPort = receiveDp.getPort();
```
使用以上代码，就可以从接收到的数据包对象`receiveDp`中获得客户端的`IP`地址和客户端的端口号，这样就可以在服务器端中将处理以后的数据构造成数据包对象，然后将处理以后的数据内容反馈给客户端了。

最后，当服务器端实现完成以后，关闭服务器端连接，实现的方式为调用连接对象的`close`方法，示例代码如下：
```
ds.close();
```
介绍完了`UDP`方式下的客户端编程和服务器端编程的基础知识以后，下面通过一个简单的示例演示`UDP`网络编程的基本使用。
## 实例 ##
该实例的功能是实现**将客户端程序的系统时间发送给服务器端，服务器端接收到时间以后，向客户端反馈字符串“`OK`”。**实现该功能的客户端代码如下所示：
```java
package udp;

import java.net.*;
import java.util.*;
/**
 * 简单的UDP客户端，实现向服务器端发生系统时间功能
 */
public class SimpleUDPClient
{
	public static void main(String[] args)
	{
		DatagramSocket ds = null; // 连接对象
		DatagramPacket sendDp; // 发送数据包对象
		DatagramPacket receiveDp; // 接收数据包对象
		String serverHost = "127.0.0.1"; // 服务器IP
		int serverPort = 10010; // 服务器端口号
		try
		{
			// 建立连接,自动分配一个空闲端口
			ds = new DatagramSocket();
			// 初始化发送数据
			Date d = new Date(); // 当前时间
			String content = d.toString(); // 转换为字符串
			byte[] data = content.getBytes();
			// 初始化IP地址
			InetAddress address = InetAddress.getByName(serverHost);
			// 初始化发送包对象 数据,数据的长度,IP地址,端口号
			sendDp = new DatagramPacket(data, data.length, address, serverPort);
			// 发送这个数据包
			ds.send(sendDp);
			// 初始化接收数据
			byte[] receive = new byte[1024];
			receiveDp = new DatagramPacket(receive, receive.length);
			// 从服务器接收数据包,
			ds.receive(receiveDp);
			// 读取反馈内容，并输出
			byte[] response = receiveDp.getData();
			int len = receiveDp.getLength();
			String s = new String(response, 0, len);
			System.out.println("服务器端反馈为：" + s);
		} catch (Exception e)
		{
			e.printStackTrace();
		} finally
		{
			try
			{
				// 关闭连接
				ds.close();
			} catch (Exception e)
			{
			}
		}
	}
}

```
在该示例代码中，首先建立`UDP`方式的网络连接，然后获得当前系统时间，这里获得的系统时间是客户端程序运行的本地计算机的时间，然后将时间字符串以及服务器端的`IP`和端口，构造成发送数据包对象，调用连接对象`ds`的`send`方法发送出去。在数据发送出去以后，构造接收数据的数据包对象，调用连接对象`ds`的`receive`方法接收服务器端的反馈，并输出在控制台。最后在`finally`语句块中关闭客户端网络连接。

和下面将要介绍的服务器端一起运行时，客户端程序的输出结果为：
```
服务器端反馈为：OK
```
下面是该示例程序的服务器端代码实现：
```java
package udp;
import java.net.*;
/**
* 简单UDP服务器端，实现功能是输出客户端发送数据，
并反馈字符串“OK"给客户端
*/
public class SimpleUDPServer 
{
    public static void main(String[] args) 
    {
        DatagramSocket ds = null; //连接对象
        DatagramPacket sendDp; //发送数据包对象
        DatagramPacket receiveDp; //接收数据包对象
        final int PORT = 10010; //端口
        try
        {
            //建立连接，监听端口
            ds = new DatagramSocket(PORT);
            System.out.println("服务器端已启动：");
            //初始化接收数据
            byte[] b = new byte[1024];
            receiveDp = new DatagramPacket(b,b.length);
            //接收
            ds.receive(receiveDp);
            //读取反馈内容，并输出
            InetAddress clientIP = receiveDp.getAddress();
            int clientPort = receiveDp.getPort();
            byte[] data = receiveDp.getData();
            int len = receiveDp.getLength();
            System.out.println("客户端IP：" + clientIP.getHostAddress());
            System.out.println("客户端端口：" + clientPort);
            System.out.println("客户端发送内容：" + new String(data,0,len));
            //发送反馈
            String response = "OK";
            byte[] bData = response.getBytes();
            sendDp = new DatagramPacket(bData,bData.length,clientIP,clientPort);
            //发送
            ds.send(sendDp);
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            try
            {
                //关闭连接,释放占用的端口
                ds.close();
            }catch(Exception e){}
        }
    }
}

```
在该服务器端实现中，首先监听`10010`号端口，和`TCP`方式的网络编程类似，服务器端的`receive`方法是阻塞方法，如果客户端不发送数据，则程序会在该方法处阻塞。

当客户端发送数据到达服务器端时，则接收客户端发送过来的数据，然后将客户端发送的数据内容读取出来，并在服务器端程序中打印客户端的相关信息，**从客户端发送过来的数据包中可以读取出客户端的`IP`以及客户端端口号**，将反馈数据字符串“`OK`”发送给客户端，最后关闭服务器端连接，释放占用的系统资源，完成程序功能示例。

运行结果：
![](https://i.imgur.com/fzgDZkV.png)

和前面`TCP`方式中的网络编程类似，这个示例也仅仅是网络编程的功能示例，也存在前面介绍的客户端无法进行多次数据交换，以及服务器端不支持多个客户端的问题，这两个问题也需要对于代码进行处理才可以很方便的进行解决。

在解决该问题以前，需要特别指出的是`UDP`方式的网络编程由于不建立虚拟的连接，所以在实际使用时和`TCP`方式存在很多的不同，最大的一个不同就是“`无状态`”。该特点指每次服务器端都收到信息，但是这些信息和连接无关，换句话说，也就是服务器端只是从信息是无法识别出是谁发送的，这样就要求发送信息时的内容需要多一些，这个在后续的示例中可以看到。

## 多次发送多次接收 ##
下面是实现客户端多次发送以及服务器端支持多个数据包同时处理的程序结构，实现的原理和`TCP`方式类似，在**客户端将数据的发送和接收放入循环中，而服务器端则将接收到的每个数据包启动一个专门的线程进行处理。**实现的代码如下：
```java
package udp;
import java.net.*;
import java.util.*;
/**
* 简单的UDP客户端，实现向服务器端发生系统时间功能
* 该程序发送3次数据到服务器端
*/
public class MulUDPClient 
{
    public static void main(String[] args) 
    {
        DatagramSocket ds = null; //连接对象
        DatagramPacket sendDp; //发送数据包对象
        DatagramPacket receiveDp; //接收数据包对象
        String serverHost = "127.0.0.1"; //服务器IP
        int serverPort = 10012; //服务器端口号
        try
        {
            //建立连接
            ds = new DatagramSocket();
            //初始化
            InetAddress address = InetAddress.getByName(serverHost);
            byte[] b = new byte[1024];
            receiveDp = new DatagramPacket(b,b.length);
            System.out.println("客户端准备完成");
            //循环10次，每次间隔0.01秒
            for(int i = 0;i < 10;i++)
            {
                //初始化发送数据
                Date d = new Date(); //当前时间
                String content = d.toString(); //转换为字符串
                byte[] data = content.getBytes();
                //初始化发送包对象
                sendDp = new DatagramPacket(data,data.length,address, serverPort);
                //发送
                ds.send(sendDp);
                //延迟
                Thread.sleep(10);
                //接收
                ds.receive(receiveDp);
                //读取反馈内容，并输出
                byte[] response = receiveDp.getData();
                int len = receiveDp.getLength();
                String s = new String(response,0,len);
                System.out.println("服务器端反馈为：" + s);
            }
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            try
            {
                //关闭连接
                ds.close();
            }catch(Exception e){}
        }
    }
}

```
在该示例中，将和服务器端进行数**据交换的逻辑写在一个for循环的内部，这样就可以实现和服务器端的多次交换了**，考虑到服务器端的响应速度，在每次发送之间加入0.01秒的时间间隔。最后当数据交换完成以后关闭连接，结束程序。

实现该逻辑的服务器端程序代码如下：
```java
package udp;
import java.net.*;
/**
* 可以并发处理数据包的服务器端
* 功能为：显示客户端发送的内容，并向客户端反馈字符串“OK”
*/
public class MulUDPServer 
{
    public static void main(String[] args) 
    {
        DatagramSocket ds = null; //连接对象
        DatagramPacket receiveDp; //接收数据包对象
        final int PORT = 10012; //端口
        byte[] b = new byte[1024];
        receiveDp = new DatagramPacket(b,b.length);
        try
        {
            //建立连接，监听端口
            ds = new DatagramSocket(PORT);
            System.out.println("服务器端已启动：");
            while(true)
            {
                //接收
                ds.receive(receiveDp);
                //启动线程处理数据包
                new LogicThread(ds,receiveDp);
            }
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            try
            {
                //关闭连接
                ds.close();
            }catch(Exception e){}
        }
    }
}

```
该代码实现了服务器端的接收逻辑，使用一个循环来接收客户端发送过来的数据包，当接收到数据包以后启动一个LogicThread线程处理该数据包。这样服务器端就可以实现同时处理多个数据包了。

实现逻辑处理的线程代码如下：
```java
package udp;
import java.net.*;
/**
* 逻辑处理线程
*/
public class LogicThread extends Thread 
{
    /**连接对象*/
    DatagramSocket ds;
    /**接收到的数据包*/
    DatagramPacket dp;
    public LogicThread(DatagramSocket ds,DatagramPacket dp)
    {
        this.ds = ds;
        this.dp = dp;
        start(); //启动线程
    }
    public void run()
    {
        try
        {
            //获得缓冲数组
            byte[] data = dp.getData();
            //获得有效数据长度
            int len = dp.getLength();
            //客户端IP
            InetAddress clientAddress = dp.getAddress();
            //客户端端口
            int clientPort = dp.getPort();
            //输出
            System.out.println("客户端IP：" + clientAddress.getHostAddress());
            System.out.println("客户端端口号：" + clientPort);
            System.out.println("客户端发送内容：" + new String(data,0,len));
            //反馈到客户端
            byte[] b = "OK".getBytes();
            DatagramPacket sendDp = new DatagramPacket(b,b.length,clientAddress,clientPort);
            //发送
            ds.send(sendDp);
        }catch(Exception e){
            e.printStackTrace();
        }
    }
}

```
在该线程中，只处理一次UDP通讯，当通讯结束以后线程死亡，在线程内部，每次获得客户端发送过来的信息，将获得的信息输出到服务器端程序的控制台，然后向客户端反馈字符串“OK”。

**由于UDP数据传输过程中可能存在丢失，所以在运行该程序时可能会出现程序阻塞的情况。**如果需要避免该问题，可以**将客户端的网络发送部分也修改成线程实现**。
### 情况：得不到服务器的响应，一直阻塞 ###
![](https://i.imgur.com/ONgEpnm.png)
正常运行的情况：
![](https://i.imgur.com/gPAL9qU.png)
客户端接收响应的时候，设置超时时间，超时的时候停止等待接收。
```
for(int i = 0;i < 10;i++)
{
    //初始化发送数据
    Date d = new Date(); //当前时间
    String content = d.toString(); //转换为字符串
    byte[] data = content.getBytes();
    //初始化发送包对象
    sendDp = new DatagramPacket(data,data.length,address, serverPort);
    //发送
    ds.send(sendDp);
    //设置接收的延时如果超过这个时间就不在等待接收
    ds.setSoTimeout(3000);
    //接收
    ds.receive(receiveDp);
    //读取反馈内容，并输出
    byte[] response = receiveDp.getData();
    int len = receiveDp.getLength();
    String s = new String(response,0,len);
    System.out.println("服务器端反馈为：" + s);
}
```
这样当客户端长时间接收不到服务器的响应的时候，就会抛出`java.net.SocketTimeoutException`异常，客户端被终止运行。
超时的运行效果：
```
客户端准备完成
服务器端反馈为：OK
java.net.SocketTimeoutException: Receive timed out
        at java.net.DualStackPlainDatagramSocketImpl.socketReceiveOrPeekData(Native Method)
        at java.net.DualStackPlainDatagramSocketImpl.receive0(DualStackPlainDatagramSocketImpl.java:124)
        at java.net.AbstractPlainDatagramSocketImpl.receive(AbstractPlainDatagramSocketImpl.java:143)
        at java.net.DatagramSocket.receive(DatagramSocket.java:812)
        at udp.MulUDPClient.main(MulUDPClient.java:40)
```
关于基础的UDP网络编程就介绍这么多了，下面将介绍一下网络协议的概念。

>原文链接: [UDP网络编程](https://www.lansheng.net.cn/blog/b6cecc51/)