---
title: Java网络编程 URLEncoder只编码URL中的中文,空格编码为百分之20
categories: 
  - java 网络编程
  - API
date: 2018-10-30 20:22:09
updated: 2019-12-17 02:00:55
abbrlink: 7865fbca
---
<div id='my_toc'><a href="/ReadingNotes/7865fbca/#需求" class="header_2">需求</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#只编码URL里的中文" class="header_2">只编码URL里的中文</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#同时编码中文和空格" class="header_2">同时编码中文和空格</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#方案1：先把空格编码成加号，然后用%20替换" class="header_3">方案1：先把空格编码成加号，然后用%20替换</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#方案2：只编码中文-直接用%20替换空格" class="header_3">方案2：只编码中文,直接用%20替换空格</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#完整代码" class="header_2">完整代码</a>&nbsp;<br><a href="/ReadingNotes/7865fbca/#参考链接" class="header_2">参考链接</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->

## 需求 ##
把下面的带中文的URL：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java IO流/Java IO流 使用RandomAccessFile快速读写文本文件最后一行/
```
编码成：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java%20IO%E6%B5%81/Java%20IO%E6%B5%81%20%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
```
## 只编码URL里的中文 ##
java中，默认的URLEcoder.encode()方法对URL进行编码的时候，会把特殊字符`:`,`.`,`空格`等都进行编码,这与我从浏览器中复制粘贴出来的显然不一样。
```java
String str = "https://www.lansheng.net.cn/2018/10/30/Java/Java IO流/Java IO流 使用RandomAccessFile快速读写文本文件最后一行/";
System.out.println(URLEncoder.encode(str,"utf-8"));
```
运行结果：
```
https%3A%2F%2Fwww.lansheng.net.cn%2F2018%2F10%2F30%2FJava%2FJava+IO%E6%B5%81%2FJava+IO%E6%B5%81+%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C%2F

```
可以看到默认的URLEncoder.encode(str,"utf-8")方法，把`:`编码成`%3A`,`/`编码成`%2F`并不需要编码那么多，只需要编码中文即可,这里来使用正则表达式对中文进行编码：
```java
public static String encode(String str, String charset)
        throws UnsupportedEncodingException
{
    //匹配中文和空格的正则表达式
    String zhPattern = "[\u4e00-\u9fa5]+";
    Pattern p = Pattern.compile(zhPattern);
    Matcher m = p.matcher(str);
    StringBuffer b = new StringBuffer();
    while (m.find())
    {
        m.appendReplacement(b, URLEncoder.encode(m.group(0), charset));
    }
    m.appendTail(b);
    return b.toString();
}
```
运行结果：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java IO%E6%B5%81/Java IO%E6%B5%81 %E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
```
这里可以看到，空格没有被编码。
## 同时编码中文和空格 ##
这里有两个方案，方案1：在正则表达式中匹配空格，也就是把正则表达式改成`[\u4e00-\u9fa5 ]`这样空格就会被编码了。
### 方案1：先把空格编码成加号，然后用%20替换 ###
运行结果：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java+IO%E6%B5%81/Java+IO%E6%B5%81+%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
```
可以看到这里空格被编码为加号`+`,但是，不幸的是，我复制到浏览器中，还是打不开我的这篇文章。：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/javaw%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/api/Ecoder/404.png)
解决方案，使用正则表达式把加号+，替换为`%20`即可：
只对中文和空格进行编码
```java
/**
 * 只对中文和空格进行编码。
 * 
 * @param str
 *            被替换的字符串
 * @param charset
 *            字符集
 * @return 替换好的
 * @throws UnsupportedEncodingException
 *             不支持的字符集
 */
    public static String encodeSpaceChinese(String str, String charset)
            throws UnsupportedEncodingException
{
    //匹配中文和空格的正则表达式
    String zhPattern = "[\u4e00-\u9fa5 ]+";
    Pattern p = Pattern.compile(zhPattern);
    Matcher m = p.matcher(str);
    StringBuffer b = new StringBuffer();
    while (m.find())
    {
        m.appendReplacement(b, URLEncoder.encode(m.group(0), charset));
    }
    m.appendTail(b);
    return b.toString();
}
```
main方法：
```java
String str = "https://www.lansheng.net.cn/2018/10/30/Java/Java IO流/Java IO流 使用RandomAccessFile快速读写文本文件最后一行/";
String url=encodeSpaceChinese(str, "UTF-8");
System.out.println(url);
url=url.replaceAll("\\+", "%20");
System.out.println(url);
```
运行结果：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java+IO%E6%B5%81/Java+IO%E6%B5%81+%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
https://www.lansheng.net.cn/2018/10/30/Java/Java%20IO%E6%B5%81/Java%20IO%E6%B5%81%20%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
```
这样就可以成功打来我的这篇文章了：
![](https://image-1257720033.cos.ap-shanghai.myqcloud.com/blog/Java/javaw%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/api/Ecoder/yes.png)
因为这与我从浏览器中复制粘贴的地址格式已经完全一样了：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java%20IO%E6%B5%81/Java%20IO%E6%B5%81%20%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
```
### 方案2：只编码中文,直接用%20替换空格 ###
这里钻了个空子：我可以直接编码中文，然后把没有编码的空格` `直接替换为`%20`。这样少了一步操作。
只对中文进行编码：
```java
public static String encodeChinese(String str, String charset)
        throws UnsupportedEncodingException
{
    //匹配中文和空格的正则表达式
    String zhPattern = "[\u4e00-\u9fa5]+";
    Pattern p = Pattern.compile(zhPattern);
    Matcher m = p.matcher(str);
    StringBuffer b = new StringBuffer();
    while (m.find())
    {
        m.appendReplacement(b, URLEncoder.encode(m.group(0), charset));
    }
    m.appendTail(b);
    return b.toString();
}
```
main方法：
```java
String str = "https://www.lansheng.net.cn/2018/10/30/Java/Java IO流/Java IO流 使用RandomAccessFile快速读写文本文件最后一行/";
String url=encodeChinese(str, "UTF-8");
System.out.println(url);
url=url.replaceAll(" ", "%20");
System.out.println(url);
```


运行结果：
```
https://www.lansheng.net.cn/2018/10/30/Java/Java IO%E6%B5%81/Java IO%E6%B5%81 %E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/
https://www.lansheng.net.cn/2018/10/30/Java/Java%20IO%E6%B5%81/Java%20IO%E6%B5%81%20%E4%BD%BF%E7%94%A8RandomAccessFile%E5%BF%AB%E9%80%9F%E8%AF%BB%E5%86%99%E6%96%87%E6%9C%AC%E6%96%87%E4%BB%B6%E6%9C%80%E5%90%8E%E4%B8%80%E8%A1%8C/

```
当然这两个方法基本差不多，我这里就简单记录一下两种可能，个人习惯用第二中方法。
## 完整代码 ##
```java
package url.encoder.hz;


import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 正则替换字符串里面的汉字部分。
 */
public class URLEncoderCH
{
    public static void main(String[] args) throws Exception
    {
        String str = "https://www.lansheng.net.cn/2018/10/30/Java/Java IO流/Java IO流 使用RandomAccessFile快速读写文本文件最后一行/";
//        把URL中表示空格的+替换成%20,因为有些应用不认+表示的空格，只认%20
        String url = URLEncode(str);
        System.out.println(url);
    }
    /**编码为浏览器可以直接访问的URL。
     * @param str
     * @return
     * @throws UnsupportedEncodingException  
     */  
    public static String URLEncode(String str)
            throws UnsupportedEncodingException
    {
        String url=encodeChinese(str, "UTF-8");
        System.out.println(url);
        url=url.replaceAll(" ", "%20");
        return url;
    }

    /**
     * 只对中文进行编码。
     * 
     * @param str
     *            被替换的字符串
     * @param charset
     *            字符集
     * @return 替换好的
     * @throws UnsupportedEncodingException
     *             不支持的字符集
     */
    public static String encodeChinese(String str, String charset)
            throws UnsupportedEncodingException
    {
        //匹配中文和空格的正则表达式
        String zhPattern = "[\u4e00-\u9fa5]+";
        Pattern p = Pattern.compile(zhPattern);
        Matcher m = p.matcher(str);
        StringBuffer b = new StringBuffer();
        while (m.find())
        {
            m.appendReplacement(b, URLEncoder.encode(m.group(0), charset));
        }
        m.appendTail(b);
        return b.toString();
    }
    
    /**
     * 只对中文和空格进行编码。
     * 
     * @param str
     *            被替换的字符串
     * @param charset
     *            字符集
     * @return 替换好的
     * @throws UnsupportedEncodingException
     *             不支持的字符集
     */
    public static String encodeSpaceChinese(String str, String charset)
            throws UnsupportedEncodingException
    {
        //匹配中文和空格的正则表达式
        String zhPattern = "[\u4e00-\u9fa5 ]+";
        Pattern p = Pattern.compile(zhPattern);
        Matcher m = p.matcher(str);
        StringBuffer b = new StringBuffer();
        while (m.find())
        {
            m.appendReplacement(b, URLEncoder.encode(m.group(0), charset));
        }
        m.appendTail(b);
        return b.toString();
    }
}
```
## 参考链接 ##
URLEncoder的只编码中文字符的类：[https://blog.csdn.net/a332324956/article/details/18991243](https://blog.csdn.net/a332324956/article/details/18991243)
URL中关于空格的编码转换成＋或转换成％20的问题：[https://www.jianshu.com/p/4a7eb969235d](https://www.jianshu.com/p/4a7eb969235d)
>原文链接: [Java网络编程 URLEncoder只编码URL中的中文,空格编码为百分之20](https://www.lansheng.net.cn/blog/7865fbca/)
