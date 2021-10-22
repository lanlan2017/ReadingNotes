---
categories:
  - Spring实战(第5版)
abbrlink: 2c9b2958
---
使用Initializr服务也很有用。
种消费该API的方式：
（又称为Spring Boot CLI）。
种方案，先从curl命令开始。
curl和Initializr API
方式是按照如下格式消费该API：
件中的所有项目信息都是默认值。
选项将下载的文件命名为demo.zip。
如果你想要使用自定义Initializr，那么需要对应地修改URL。
ST服务所有可用的参数（及其默认值）。
表A.1 Initializr API支持的请求参数
URL获取参数列表和可用依赖项的列表：
一个包含webstarter依赖的项目zip包：
在这种情况下，下面的命令可以解决该问题:
道的方式传递给tar命令进行解压。
ring Boot命令行接口
喜欢的）方式可能是使用SDKMAN：
实际上，使用Spring Boot CLI生成项目的最简单方式为：
载成名为demo.zip的zip文件。
表A.2列出了spring init命令所有可用的参数。
令支持的所有请求参数
出参数的列表以及可用依赖：
下使用--dependencies和--java命令即可：
我们可以使用如下的命令：
驼峰命名（例如package-name与packageName）。