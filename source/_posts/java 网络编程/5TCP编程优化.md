---
title: 5TCP编程优化
categories: 
  - java 网络编程
date: 2018-08-17 22:47:59
updated: 2019-11-25 01:27:45
abbrlink: 5eef6183
---
<div id='my_toc'><a href="/ReadingNotes/5eef6183/#把客户端交换的逻辑写到循环中" class="header_2">把客户端交换的逻辑写到循环中</a><br><a href="/ReadingNotes/5eef6183/#把服务器端的数据交换逻辑写在循环" class="header_2">把服务器端的数据交换逻辑写在循环</a><br><a href="/ReadingNotes/5eef6183/#如何使服务器端支持多个客户端同时工作" class="header_1">如何使服务器端支持多个客户端同时工作</a><br><a href="/ReadingNotes/5eef6183/#运行效果" class="header_3">运行效果</a><br><a href="/ReadingNotes/5eef6183/#出现的问题" class="header_4">出现的问题</a><br><a href="/ReadingNotes/5eef6183/#使用线程池" class="header_2">使用线程池</a><br></div>
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

在前面的示例中，客户端中建立了一次连接，只发送一次数据就关闭了，这就相当于拨打电话时，电话打通了只对话一次就关闭了，其实更加常用的应该是拨通一次电话以后多次对话，这就是**复用客户端连接**。

## 把客户端交换的逻辑写到循环中 ##
那 么**如何实现建立一次连接，进行多次数据交换呢？其实很简单，建立连接以后，将数据交换的逻辑写到一个循环中就可以了**。这样只要循环不结束则连接就不会被关 闭。按照这种思路，可以改造一下上面的代码，让该程序可以在建立连接一次以后，发送三次数据，当然这里的次数也可以是多次，示例代码如下：
```java
package tcp;
import java.io.*;
import java.net.*;
/**
* 复用连接的Socket客户端
* 功能为：发送字符串“Hello”到服务器端，并打印出服务器端的反馈
*/
public class MulSocketClient 
{
    public static void main(String[] args) 
    {
        Socket socket = null;
        InputStream is = null;
        OutputStream os = null;
        //服务器端IP地址
        String serverIP = "127.0.0.1";
        //服务器端端口号
        int port = 10000;
        //发送内容
        String data[] ={"First","Second","Third"};
        try 
        {
            //建立连接
            socket = new Socket(serverIP,port);
            //初始化流
            os = socket.getOutputStream();
            is = socket.getInputStream();
            byte[] b = new byte[1024];
            //输出全部的数据
            for(int i = 0;i < data.length;i++)
            {
                //发送数据
                os.write(data[i].getBytes());
                //接收数据
                int n = is.read(b);
                //输出反馈数据
                System.out.println("服务器反馈：" + new String(b,0,n));
            }
        } catch (Exception e) {
            e.printStackTrace(); //打印异常信息
        }finally{
            try 
            {
                //关闭流和连接
                is.close();
                os.close();
                socket.close();
            } catch (Exception e2) {}
        }
    }
}

```
该示例程序和前面的代码相比，将数据交换部分的逻辑写在一个for循环的内容，这样就可以建立一次连接，依次将data数组中的数据按照顺序发送给服务器端了。

如果还是使用前面示例代码中的服务器端程序运行该程序，则该程序的结果是：
```
服务器反馈：First
java.net.SocketException: Software caused connection abort: recv failed
        at java.net.SocketInputStream.socketRead0(Native Method)
        at java.net.SocketInputStream.socketRead(SocketInputStream.java:116)
        at java.net.SocketInputStream.read(SocketInputStream.java:170)
        at java.net.SocketInputStream.read(SocketInputStream.java:141)
        at java.net.SocketInputStream.read(SocketInputStream.java:127)
        at tcp.MulSocketClient.main(MulSocketClient.java:35)
```
显然，客户端在实际运行时出现了异常，出现异常的原因是什么呢？如果仔细阅读前面的代码，应该还记得前面示例代码中的服务器端是对话一次数据以后就关闭了连接**，如果服务器端程序关闭了，客户端继续发送数据肯定会出现异常**，这就是出现该问题的原因。

按照客户端实现的逻辑，也可以复用服务器端的连接，实现的原理也是将服务器端的数据交换逻辑写在循环中即可，按照该种思路改造以后的服务器端代码为：


## 把服务器端的数据交换逻辑写在循环 ##

```java
package tcp;
import java.io.*;
import java.net.*;
/**
* 复用连接的echo服务器
* 功能：将客户端发送的内容反馈给客户端
*/
public class MulSocketServer 
{
    public static void main(String[] args) 
    {
        ServerSocket serverSocket = null;
        Socket socket = null;
        OutputStream os = null;
        InputStream is = null;
        //监听端口号
        int port = 10000;
        try 
        {
            //建立连接
            serverSocket = new ServerSocket(port);
            System.out.println("服务器已启动：");
            //获得连接
            socket = serverSocket.accept();
            //初始化流
            is = socket.getInputStream();
            os = socket.getOutputStream();
            byte[] b = new byte[1024];
            for(int i = 0;i < 3;i++)
            {
                int n = is.read(b);
                //输出
                System.out.println("客户端发送内容为：" + new String(b,0,n));
                //向客户端发送反馈内容
                os.write(b, 0, n);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            try
            {
                //关闭流和连接
                os.close();
                is.close();
                socket.close();
                serverSocket.close();
            }catch(Exception e){}
        }
    }
}

```
在该示例代码中，也将数据发送和接收的逻辑写在了一个for循环内部，只是在实现时硬性的将循环次数规定成了`3`次，这样代码虽然比较简单，但是通用性比较差。

服务器端程序的输出结果为：
```
服务器已启动：
客户端发送内容为：First
客户端发送内容为：Second
客户端发送内容为：Third
```
客户端的输出结果为：
```
服务器反馈：First
服务器反馈：Second
服务器反馈：Third
```
在该程序中，比较明显的体现出了“`请求-响应`”模型，也就是在客户端发起连接以后，

首先发送字符串“`First`”给服务器端，服务器端输出客户端发送的内容“`First`”，然后将客户端发送的内容再反馈给客户端，这样客户端也输出服务器反馈“`First`”，这样就完成了客户端和服务器端的一次对话，

紧接着客户端发送“`Second`”给服务器端，服务端输出“`Second`”，然后将“`Second`”再反馈给客户端，客户端再输出“`Second`”，从而完成第二次对话，第三次会话的过程和这个一样。

在这个过程中，**每次都是客户端程序首先发送数据给服务器端，服务器接收数据以后，将结果反馈给客户端，客户端接收到服务器端的反馈，从而完成一次通讯过程。**

在该示例中，虽然解决了多次发送的问题，但是客户端和服务器端的次数控制还不够灵活，如果客户端的次数不固定怎么办呢？是否可以使用某个特殊的字符串，例如quit，表示客户端退出呢,这就涉及到网络协议的内容了，会在后续的网络应用示例部分详细介绍。下面开始介绍另外一个网络编程的突出问题。

# 如何使服务器端支持多个客户端同时工作 #

前面介绍的服务器端程序，只是实现了概念上的服务器端，离实际的服务器端程序结构距离还很遥远，如果需要让服务器端能够实际使用，那么最需要解决的问题就是——如何支持多个客户端同时工作。

**一个服务器端一般都需要同时为多个客户端提供通讯，如果需要同时支持多个客户端，则必须使用前面介绍的线程的概念**。简单来说，也就是**当服务器端接收到一个连接时，启动一个专门的线程处理和该客户端的通讯。**

按照这个思路改写的服务端示例程序将由两个部分组成，`MulThreadSocketServer`类实现服务器端控制，实现**接收客户端连接，然后开启专门的逻辑线程处理该连接**，`LogicThread`类实现对于一个客户端连接的逻辑处理，**将处理的逻辑放置在该类的`run`方法中**。该示例的代码实现为：
```java
package tcp;
import java.net.ServerSocket;
import java.net.Socket;
/**
* 支持多客户端的服务器端实现
*/
public class MulThreadSocketServer 
{
    public static void main(String[] args) 
    {
        ServerSocket serverSocket = null;
        Socket socket = null;
        //监听端口号
        int port = 10000;
        try 
        {
            //建立连接
            serverSocket = new ServerSocket(port);
            System.out.println("服务器已启动：");
            while(true)
            {
                //获得连接
                socket = serverSocket.accept();
                //启动线程处理连接
                new LogicThread(socket);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }finally{
            try
            {
                //关闭连接
                serverSocket.close();
            }catch(Exception e){}
        }
    }
}

```
在该示例代码中，实现了一个`while`形式的死循环，由于`accept`方法是阻塞方法，所以当客户端连接未到达时，将阻塞该程序的执行，当客户端到达时接收该连接，并启动一个新的`ResponseThread`线程处理该连接，然后按照循环的执行流程，继续等待下一个客户端连接。这样当任何一个客户端连接到达时，都开启一个专门的线程处理，通过多个线程支持多个客户端同时处理。
下面再看一下`ResponseThread`线程类的源代码实现：
```
package tcp;

import java.io.*;
import java.net.*;
/**
* 服务器端逻辑线程
*/
public class ResponseThread extends Thread 
{
    Socket socket;
    InputStream in;
    OutputStream out;
    public ResponseThread(Socket socket)
    {
        this.socket = socket;
        start(); //启动线程
    }
    public void run()
    {
        byte[] receive = new byte[1024];
        try
        {
            response(receive);
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            close();
        }
    }
    /**   
     * @param receive 接收到的数据
     * @throws IOException  
     */  
    public void response(byte[] receive) throws IOException
    {
        //初始化流
        out = socket.getOutputStream();
        in = socket.getInputStream();
        for(int i = 0;i < 3;i++)
        {
            //读取数据
            int n = in.read(receive);
            //反馈数据
            out.write(receive,0,n);
        }
    }
    /**
    * 关闭流和连接
    */
    private void close()
    {
        try
        {
            //关闭流和连接
            out.close();
            in.close();
            socket.close();
        }catch(Exception e){}
    }
}

```
在该示例代码中，每次使用一个连接对象构造一个处理线程，该连接对象就是该线程需要处理的连接，在线程构造完成以后，该线程就被启动起来了，然后**在`run`方法内部对客户端连接进行处理**，数据交换的逻辑和前面的示例代码一致，只是这里将接收到客户端发送过来的数据并进行处理的逻辑封装成了`response`方法，实现的是`echo`服务的逻辑。

### 运行效果 ###
#### 出现的问题 ####
```
javac -d . MulThreadSocketServer.java
```
编译结果：
```
MulThreadSocketServer.java:26: 错误: 找不到符号
                new ResponseThread(socket);
                    ^
  符号:   类 ResponseThread
  位置: 类 MulThreadSocketServer
1 个错误
```
换到IDE中运行，运行起来是好好的，但是CMD中却报这样的错误。
这是怎么回事呢，这个其实是因为`ResponseThread.class`没有，所以应该先编译`ResponseThread`,然后再编译`MulThreadSocketServer`
编译响应逻辑线程：
```
javac -d . ResponseThread.java
```
编译服务器：
```
javac -d . MulThreadSocketServer.java
```
运行服务器：
```
java tcp.MulThreadSocketServer
```
运行客户端1：
```
java tcp.MulSocketClient
```
运行客户端2：
```
java tcp.MulSocketClient
```
两个客户端的响应效果如下所示：

![两个服务器的响应效果](https://i.imgur.com/DjjkjBK.png)

这里的示例还只是基础的服务器端实现，在实际的服务器端实现中，由于硬件和端口数的限制，所以不能无限制的创建线程对象，而且频繁的创建线程对象效率也比较低，所以程序中都实现了线程池来提高程序的执行效率。
## 使用线程池 ##
这里简单介绍一下线程池的概念，**线程池(`Thread pool)`是池技术的一种，就是在程序启动时首先把需要的线程对象创建好**，例如创建`5000`个线程对象，**然后当客户端连接到达时从线程池中取出一个已经创建完成的线程对象使用即可**。**当客户端连接关闭以后，将该线程对象重新放入到线程池中供其它的客户端重复使用**，这样可以提高程序的执行速度，优化程序对于内存的占用等。

关于基础的`TCP`方式的网络编程就介绍这么多，下面介绍`UDP`方式的网络编程在`Java`语言中的实现。

>原文链接: [5TCP编程优化](https://www.lansheng.net.cn/blog/5eef6183/)
