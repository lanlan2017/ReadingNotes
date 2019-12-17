---
title: DatagramSocket类
categories: 
  - java 网络编程
  - API
date: 2018-08-18 21:47:34
updated: 2019-12-17 01:44:33
abbrlink: c1fee13e
---
<div id='my_toc'><a href="/ReadingNotes/c1fee13e/#成员方法" class="header_2">成员方法</a><br></div>
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
|方法|描述|
|:-|:-|
|`DatagramSocket()`|构造数据报套接字并将其绑定到本地主机上任何可用的端口。 |
|`DatagramSocket(int port)` |创建数据报套接字并将其绑定到本地主机上的指定端口。 |
|`DatagramSocket(int port, InetAddress laddr)` |创建数据报套接字，将其绑定到指定的IP地址|
|`DatagramSocket(SocketAddress bindaddr)` |创建数据报套接字，将其绑定到指定的本地套接字地址。 |
|`protected  DatagramSocket(DatagramSocketImpl impl)`|创建带有指定 DatagramSocketImpl 的未绑定数据报套接字。 |
## 成员方法 ##

|方法|描述|
|:-|:-|
|`void bind(SocketAddress addr)`|将此 DatagramSocket 绑定到特定的地址和端口。 |
|`void close()`|关闭此数据报套接字。 |
|`void connect(InetAddress address, int port)`|将套接字连接到此套接字的远程地址。 |
|`void connect(SocketAddress addr)`|将此套接字连接到远程套接字地址（IP 地址 + 端口号）。 |
|`void disconnect()`|断开套接字的连接。 |
|`boolean getBroadcast()`|检测是否启用了 SO_BROADCAST。 |
|`DatagramChannel getChannel()`|返回与此数据报套接字关联的唯一 DatagramChannel 对象（如果有）。 |
|`InetAddress getInetAddress()`|返回此套接字连接的地址。 |
|`InetAddress getLocalAddress()`|获取套接字绑定的本地地址。 |
|`int getLocalPort()`|返回此套接字绑定的本地主机上的端口号。 |
|`SocketAddress getLocalSocketAddress()`|返回此套接字绑定的端点的地址，如果尚未绑定则返回 null。 |
|`int getPort()`|返回此套接字的端口。 |
|`int getReceiveBufferSize()`|获取此 DatagramSocket 的 SO_RCVBUF 选项的值，该值是平台在 DatagramSocket 上输入时使用的缓冲区大小。 |
|`SocketAddress getRemoteSocketAddress()`|返回此套接字连接的端点的地址，如果未连接则返回 null。 |
|`boolean getReuseAddress()`|检测是否启用了 SO_REUSEADDR。 |
|`int getSendBufferSize()`|获取此 DatagramSocket 的 SO_SNDBUF 选项的值，该值是平台在 DatagramSocket 上输出时使用的缓冲区大小。 |
|`int getSoTimeout()`|获取 SO_TIMEOUT 的设置。 |
|`int getTrafficClass()`|为从此 DatagramSocket 上发送的包获取 IP 数据报头中的流量类别或服务类型。 |
|`boolean isBound()`|返回套接字的绑定状态。 |
|`boolean isClosed()`|返回是否关闭了套接字。 |
|`boolean isConnected()`|返回套接字的连接状态。 |
|`void receive(DatagramPacket p)`|从此套接字接收数据报包。 |
|`void send(DatagramPacket p)`|从此套接字发送数据报包。 |
|`void setBroadcast(boolean on)`|启用/禁用 SO_BROADCAST。 |
|`static void setDatagramSocketImplFactory(DatagramSocketImplFactory fac)`|为应用程序设置数据报套接字实现工厂。 |
|`void setReceiveBufferSize(int size)`|将此 DatagramSocket 的 SO_RCVBUF 选项设置为指定的值。 |
|`void setReuseAddress(boolean on)`|启用/禁用 SO_REUSEADDR 套接字选项。 |
|`void setSendBufferSize(int size)`|将此 DatagramSocket 的 SO_SNDBUF 选项设置为指定的值。 |
|`void setSoTimeout(int timeout)`|启用/禁用带有指定超时值的 SO_TIMEOUT，以毫秒为单位。 |
|`void setTrafficClass(int tc)`|为从此 DatagramSocket 上发送的数据报在 IP 数据报头中设置流量类别 (traffic class) 或服务类型八位组 (type-of-service octet)。 |

>原文链接: [DatagramSocket类](https://www.lansheng.net.cn/blog/c1fee13e/)
