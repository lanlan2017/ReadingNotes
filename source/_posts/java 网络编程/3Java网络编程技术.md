---
title: 3Java网络编程技术
categories: 
  - java 网络编程
date: 2018-08-17 11:40:15
updated: 2019-11-25 01:27:45
abbrlink: eadab85c
---
<div id='my_toc'><a href="/ReadingNotes/eadab85c/#-InetAddress-类--代表一个-IP-地址" class="header_2">`InetAddress`类--代表一个`IP`地址</a><br><a href="/ReadingNotes/eadab85c/#创建InetAddress类实例的方法" class="header_3">创建InetAddress类实例的方法</a><br><a href="/ReadingNotes/eadab85c/#实例" class="header_4">实例</a><br><a href="/ReadingNotes/eadab85c/#重写Object类的方法：" class="header_3">重写Object类的方法：</a><br><a href="/ReadingNotes/eadab85c/#获取IP地址相关信息的方法" class="header_3">获取IP地址相关信息的方法</a><br><a href="/ReadingNotes/eadab85c/#判断方法：" class="header_3">判断方法：</a><br></div>
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

`Java`语言是在网络环境下诞生的，所以`Java`语言虽然不能说是对于网络编程的支持最好的语言，但是必须说是一种对于网络编程提供良好支持的语言，使用`Java`语言进行网络编程将是一件比较轻松的工作。

**和网络编程有关的基本`API`位于`java.net`包中**，该包中包含了基本的网络编程实现，该包是网络编程的基础。该包中既包含基础的网络编程类，也包含封装后的专门处理`WEB`相关的处理类。在本章中，将只介绍基础的网络编程类。

首先来介绍一个基础的网络类——`InetAddress`类。该类的功能是代表一个`IP`地址，是`ip`地址的`java`表示方式。并且将`IP`地址和域名相关的操作方法包含在该类的内部。

## `InetAddress`类--代表一个`IP`地址 ##
### 创建InetAddress类实例的方法 ###

**`InetAddress`没有`public`构造器，必须通过一系列的静态方法获取实例。**如下表所示。

|方法|描述|
|:-|:-|
|`static InetAddress[] getAllByName(String host)`|在给定主机名的情况下，根据系统上配置的名称服务返回其 IP 地址所组成的数组。 |
|`static InetAddress getByAddress(byte[] addr)`|在给定原始 IP 地址的情况下，返回 InetAddress 对象。 |
|`static InetAddress getByAddress(String host, byte[] addr)`|根据提供的主机名和 IP 地址创建 InetAddress。 |
|`static InetAddress getByName(String host)`|在给定主机名的情况下确定主机的 IP 地址。 |
|`static InetAddress getLocalHost()`|返回本地主机。 |

在这些静态方法中，最为常用的应该是`getByName(String host)`方法，只需要传入目标主机的名字，

#### 实例 ####
通过域名获取`InetAddress`对象：
```java
// 使用域名创建InetAddress对象
InetAddress inetAddr = InetAddress.getByName("github.com");
```
通过IP地址获取InetAddress对象:
```java
// 使用点分十进制IP地址创建InetAddress对象
InetAddress inetAddr = InetAddress.getByName("52.74.223.119");
```
获取本机的InetAddress对象:
```java
InetAddress address = InetAddress.getLocalHost();
```
### 重写Object类的方法： ###

|方法|描述|
|:-|:-|
|`boolean equals(Object obj)`|将此对象与指定对象比较。 |
|`int hashCode()`|返回此 IP 地址的哈希码。 |
|`String toString()`|将此 IP 地址转换为 String。 |
实例：
```java
//根据域名生成实例
InetAddress inetAddr=InetAddress.getByName("github.com");
System.out.println(inetAddr.toString());
//根据IP地址生产实例
inetAddr=InetAddress.getByName("13.250.177.223");
System.out.println(inetAddr.toString());
//获取本机
inetAddr=InetAddress.getLocalHost();
System.out.println(inetAddr.toString());
```
运行结果：
```
github.com/13.250.177.223
/13.250.177.223
DESKTOP-9H231R6/192.168.233.233
```
### 获取IP地址相关信息的方法 ###

|方法|描述|
|:-|:-|
|`String getCanonicalHostName()`|获取此 IP 地址的完全限定域名。 |
|`String getHostAddress()`|获取点分十进制表示的ip地址 |
|`byte[] getAddress()`|获取字节数组表示的ip地址 |
|`String getHostName()`|获取此 IP 地址的主机名。 |

实例：
```
public static void main(String[] args)
{
    try
    {
        // 使用域名创建对象
        InetAddress inetAddr = InetAddress.getByName("github.com");
        System.out.println("IP地址的完全限定域名：" + inetAddr.getCanonicalHostName());
        System.out.println("主机IP地址为：" + inetAddr.getHostAddress());
        System.out.println("主机名称为：" + inetAddr.getHostName());

        // byte[] getAddress() 返回此 InetAddress 对象的原始 IP 地址。
        byte[] ipbyte = inetAddr.getAddress();// 获取原始IP地址
        System.out.println("字节数组表示的ip地址：" + Arrays.toString(ipbyte));
        System.out.print("字节地址转为点分十进制表示:");
        for (int i = 0; i < ipbyte.length; i++)
        {
            if (i != 0)
                System.out.print(".");
            System.out.print(Byte.toUnsignedInt(ipbyte[i]));
        }
        System.out.println();
    } catch (Exception e)
    {
    }
}
```
运行结果：
```
IP地址的完全限定域名：ec2-52-74-223-119.ap-southeast-1.compute.amazonaws.com
主机IP地址为：52.74.223.119
主机名称为：github.com
字节数组表示的ip地址：[52, 74, -33, 119]
字节地址转为点分十进制表示:52.74.223.119
```
从运行结果中可以看到`getHostAddress()`方法获取的是字符串表示的IP地址(点分十进制)，而`getAddress()`获取的是字节数组表示的IP地址，这两者只是表示方式不同而已，两者之间可以相互转化。

### 判断方法： ###

|方法|描述|
|:-|:-|
|`boolean isAnyLocalAddress()`|检查 InetAddress 是否是通配符地址的实用例行程序。 |
|`boolean isLinkLocalAddress()`|检查 InetAddress 是否是链接本地地址的实用例行程序。 |
|`boolean isLoopbackAddress()`|检查 InetAddress 是否是回送地址的实用例行程序。 |
|`boolean isMCGlobal()`|检查多播地址是否具有全局域的实用例行程序。 |
|`boolean isMCLinkLocal()`|检查多播地址是否具有链接范围的实用例行程序。 |
|`boolean isMCNodeLocal()`|检查多播地址是否具有节点范围的实用例行程序。 |
|`boolean isMCOrgLocal()`|检查多播地址是否具有组织范围的实用例行程序。 |
|`boolean isMCSiteLocal()`|检查多播地址是否具有站点范围的实用例行程序。 |
|`boolean isMulticastAddress()`|检查 InetAddress 是否是 IP 多播地址的实用例行程序。 |
|`boolean isReachable(int timeout)`|测试是否可以达到该地址。 |
|`boolean isReachable(NetworkInterface netif,int ttl, int timeout)`|测试是否可以达到该地址。 |
|`boolean isSiteLocalAddress()`|检查 InetAddress 是否是站点本地地址的实用例行程序。 |

>原文链接: [3Java网络编程技术](https://www.lansheng.net.cn/blog/eadab85c/)
