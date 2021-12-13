---
title: 第3章 Java语言基础
categories: 
  - 7 Java经典编程300例
  - 第3章 Java语言基础
date: 2020-09-06 09:13:35
updated: 2020-09-06 09:13:35
abbrlink: cb809aa4
---
<div id='my_toc'></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第3章 Java语言基础
本章读者可以学到如下实例:
- 实例011 输出错误信息与调试信息
- 实例012 从控制台接收输入字符
- 实例013 重定向输出流实现程序日志
- 实例014 自动类型转换与强制类型转换
- 实例015 加密可以这样简单(位运算)
- 实例016 用三元运算符判断奇数和偶数
- 实例017 不用乘法运算符实现2×16
- 实例018 实现两个变量的互换(不借助第3个变量)


## 实例013 重定向输出流实现程序日志
`System`类中的`out`成员变量是`Java`的标准输出流,程序常用它来输出调试信息。`out`成员变量被定义为`fina`类型的,无法直接重新复制,但是可以通过`setOut`方法来设置新的输出流。本实例利用该方法实现了输出流的重定向,把它指向一个文件输出流,从而实现了日志功能。程序运行后控制台提示运行结束信息,如图3.3所示,但是在运行过程中的步骤都保存到了日志文件中,如图3.4所示。

```java
package com.mingrisoft;
import java.io.FileNotFoundException;
import java.io.PrintStream;
public class RedirectOutputStream {
    public static void main(String[] args) {
        try {
            PrintStream out = System.out;// 保存原输出流
            PrintStream ps=new PrintStream("./log.txt");// 创建文件输出流
            System.setOut(ps);// 设置使用新的输出流
            int age=18;// 定义整形变量
            System.out.println("年龄变量成功定义，初始值为18");
            String sex="女";// 定义字符串变量
            System.out.println("性别变量成功定义，初始值为女");
            // 整合两个变量
            String info="这是个"+sex+"孩子，应该有"+age+"岁了。";
            System.out.println("整合两个变量为info字符串变量，其结果是："+info);
            System.setOut(out);// 恢复原有输出流
            System.out.println("程序运行完毕，请查看日志文件。");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## 实例015 加密可以这样简单(位运算)
### 实例说明
本实例通过位运算的异或运算符“^”把字符串与一个指定的值进行异或运算,从而改变字符串中每个字符的值,这样就可以得到一个加密后的字符串,如图3.6所示。当把加密后的字符串作为程序输入内容,异或运算会把加密后的字符串还原为原有字符串的值,如图3.7所
```java
package com.mingrisoft;
import java.util.Scanner;
public class Example {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.println("请输入一个英文字符串或解密字符串");
        String password = scan.nextLine();// 获取用户输入
        char[] array = password.toCharArray();// 获取字符数组
        for (int i = 0; i < array.length; i++) {// 遍历字符数组
            array[i] = (char) (array[i] ^ 20000);// 对每个数组元素进行异或运算
        }
        System.out.println("加密或解密结果如下：");
        System.err.println(new String(array));// 输出密钥
    }
}
```
### 技术要点
本实例的关键技术是异或运算。**如果某个字符(或数值)x与一个数值m进行异或运算得到y,则再用y与m进行异或运算就可以还原为x**,因此应用这个原理可以实现加密和解密功能。
## 实例016 用三元运算符判断奇数和偶数
三元运算符是`if...else`条件语句的简写格式,它可以完成简单的条件判断。本实例利用这个三元运算符实现了奇偶数的判断,程序要求用户输入一个整数,然后程序判断是奇数还是偶数,并输出到控制台中。实例的运行效果如图3.8所示。
```java
package com.mingrisoft;
import java.util.Scanner;
public class ParityCheck {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);// 创建输入流扫描器
        System.out.println("请输入一个整数：");
        long number = scan.nextLong();// 获取用户输入的整数
        String check = (number % 2 == 0) ? "这个数字是:偶数" : "这个数字是：奇数";
        System.out.println(check);
    }
}
```
技术要点本实例的关键技术就是以三元运算符实现简单的条件判断。其语法格式如下
```
条件运算?运算结果1:运算结果2;
```
如果条件运算结果为`true`,返回值就是运算结果1,否则返回运算结果2

## 实例017 不用乘法运算符实现2×16
程序开发中常用的乘法运算是通过“*”运算符或者`BigDecimal`类的`multiply()`方法实现的。但是本实例将介绍在这两种方法之外如何实现乘法,而且实现的运算效率非常高。实例的运行效果如图3.9所示。

```java
package com.mingrisoft;
import java.util.Scanner;
public class Example {
    public static void main(String[] args) {
        Scanner scan=new Scanner(System.in);// 创建扫描器
        System.out.println("请输入一个整数");
        long number = scan.nextLong();// 获取输入的整数
        System.out.println("你输入的数字是："+number);
        System.out.println("该数字乘以2的运算结果为："+(number<<1));
        System.out.println("该数字乘以4的运算结果为："+(number<<2));
        System.out.println("该数字乘以8的运算结果为："+(number<<3));
        System.out.println("该数字乘以16的运算结果为："+(number<<4));
    }
}
```
### 技术要点
本实例的关键技术就是左移运算。**如果一个整数左移运算n位,就相当于这个整数乘以2的n次方**。例如,`2<<4`(即2左移4位)相当于2^4,也就是16

## 实例018 实现两个变量的互换(不借助第3个变量)
### 实例说明
变量的互换常见于数组排序算法中,当判断两个数组元素需要交互时,将创建一个临时变量来共同完成互换,临时变量的创建增加了系统资源的消耗。**如果需要交换的是两个`整数类型`的变量**,那么可以使用更高效的方法。本实例演示了如何不借助临时变量(第3个变量)实现两个整数类型变量的高效互换。实例的运行效果如图3.10所示。

### 实现过程
```java
package com.mingrisoft;
import java.util.Scanner;
public class VariableExchange {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);// 创建扫描器
        System.out.println("请输入变量A的值");
        long A = scan.nextLong();// 接收第一个变量值
        System.out.println("请输入变量B的值");
        long B = scan.nextLong();// 接收第二个变量值
        System.out.println("A=" + A + "\tB=" + B);
        System.out.println("执行变量互换...");
        A = A ^ B;// 执行变量互换
        B = B ^ A;
        A = A ^ B;
        System.out.println("A=" + A + "\tB=" + B);
    }
}
```