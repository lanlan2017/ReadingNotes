---
title: 实例033 利用数组随机抽取幸运观众
categories:
  - 7 Java经典编程300例
  - 第5章 数组及其常用操作
abbrlink: 846a1c17
date: 2020-09-12 03:06:06
updated: 2020-09-12 03:06:06
---
# 实例033 利用数组随机抽取幸运观众
## 实例说明
数组在程序开发中被广泛应用,使用数组可以使程序代码更加规范,更易于维护。例如,字符串数组可用于定义表格控件的列名称,而整型数组可以用来定义列对应的宽度,本实例就通过这两个数组实现了对表格控件中表头列的设置。实例的运行效果如图54所示。


### 脚下留神
如果直接将表格控件添加到滚动面板以外的容器中,首先应该通过`JTable`类的`getTableHeader()`方法获取表格的`JTableheader`表头类的对象,然后再将该对象添加到容器相应的位置,否则表格将没有表头,无法显示任何列名称.
### 技术要点
本实例的关键技术在于设置表格的数据模型和访问列模型。其中表格的数据模型可以采用`DefaultTableModel`类创建数据模型对象,而创建过程中可以把字符串数组作为参数来创建表格列的名称.
#### 1. 创建表格数据模型
`DefaultAbleModel`类的构造方法有很多,其中一个可以把字符串数组作为参数来生成列名称,同时接收`int`类型的参数来设置表格添加多少行空白数据。这个构造方法的声明如下:
```java
public DefaultTableModel(Object[] columnNames, int rowCount) {

}
```
参数说明
- `columnNames`:存放列名的数组。
- `rowCount`:指定创建多少行空白数据。

#### 2. 设置表格数据模型
`JTable`类是表格控件,它提供了`setModel()`方法来设置表格的数据模型。设置数据模型以后表格控件可以从数据模型中提取表头所有列名称和所有行数据,这个数据模型将负责表格所有数据的维护。该设置表格模型的方法的声明如下:
```java
public void setModel(final TableModel dataModel)
```
参数说明
`dataModel`:此表的新数据模型。
#### 3. 获取表格列模型
表格中所有列对象都存放在列模型中,它们用于定义表格的每个列的名称及宽度等信息。表格的列模型可以通过`getColumnModel()`方法来获取。其方法的声明如下
```java
public TableColumnModel getColumnModel()
```
#### 4. 设置列宽度
列对象存放在列模型中,并且列的宽度需要通过列对象的`setPreferredWidth()`方法来设置。该方法的声明如下:
```java
public void setPreferredWidth(int preferredWidth)
```
参数说明
`preferredWidth`:列对象的首选宽度参数。