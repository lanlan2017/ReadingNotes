# 附录C Ajax的XMLHttpRequest对象的属性和方法
XMLHttpRequest对象是Ajax的核心，它有许多的属性、方法和事件以便于脚本处理和控制HTTP的请求与响应。下面是关于XMLHttpRequest对象的一些属性和方法的介绍。

## 1．readyState属性
当一个XMLHttpRequest对象被创建后，readyState属性标识了当前对象正处于什么状态，可以通过对该属性的访问，来判断此次请求的状态然后做出相应的操作。readyState属性具体的值代表的意义如表C-1所示。

<center>表C-1 readyState属性</center>

[插图]

## 2．responseText属性
responseText属性包含客户端接收到的HTTP响应的文本内容。当readyState属性值为0、1或2时，responseText属性包含一个空字符串；当readyState属性值为3（正在接收）时，响应中包含客户端还未完成的响应信息；当readyState属性值为4（已加载）时，该responseText属性才包含完整的响应信息。

## 3．responseXML属性
只有当readyState属性值为4，并且响应头部的Content-Type的MIME类型被指定为XML（text/xml或者application/xml）时，该属性才会有值并且被解析为一个XML文档，否则该属性值为null。如果是回传的XML文档结构不良或者未完成响应回传，该属性值也会为null。由此可见，responseXML属性用来描述被XMLHttpRequest解析后的XML文档的属性。

## 4．status属性
status属性描述了HTTP状态代码。注意，仅当readyState属性值为3（正在接收中）或4（已加载）时，才能对此属性进行访问。如果在readyState属性值小于3时，试图存取status属性值，将引发一个异常。

## 5．statusText属性
statusText属性描述了HTTP状态代码文本，并且仅当readyState属性值为3或4时才可用。当readyState属性为其他值时试图存取statusText属性值将引发一个异常。

## 6．onreadystatechange事件
每当 readyState 属性值发生改变时，就会触发 onreadystatechange 事件。一般都通过该事件来触发回传处理函数。

## 7．open()方法
XMLHttpRequest对象是通过调用open（method，uri，async，username，password）方法来进行初始化工作的。调用该方法将得到一个可以用来进行发送（send()方法）的对象。open()方法有5个参数。
（1）method参数是必须提供的，用于指定用来发送请求的HTTP方法（GET，POST，PUT， DELETE或HEAD）。按照HTTP规范，该参数要大写。
（2）uri参数用于指定XMLHttpRequest对象把请求发送到的服务器相应的URI，该地址会被自动解析为绝对地址。
（3）async参数用于指定是否请求是异步的，其默认值为true。如果需要发送一个同步请求，需要把该参数设置为false。
（4）如果需要服务器验证访问用户的情况，那么可以设置username以及password这两个参数。

## 8．send()方法
调用open()方法后，就可以通过调用send()方法按照open()方法设定的参数将请求进行发送。当open()方法中async参数为true时，在send()方法调用后立即返回，否则将会中断直到请求返回。需要注意的是，send()方法必须在readyState属性值为1时，即调用open()方法以后才能调用。在调用send()方法以后到接收到响应信息之前，readyState 属性的值将被设为2；一旦接收到响应消息， readyState属性值将会被设为3；直到响应接收完成，readyState属性的值才会被设为4。

send()方法使用一个可选的参数，该参数可以包含可变类型的数据。用户可以使用它并通过POST方法把数据发送到服务器。另外，可以显式地使用null参数调用send()方法，这与不用参数调用该方法一样。对于大多数其他的数据类型，在调用send()方法之前，应该使用setRequestHeader()方法先设置Content-Type头部。如果send（data）方法中的data参数的类型为DOMString，那么，数据将被编码为UTF-8。如果数据是Document类型，那么将使用由data.xmlEncoding指定的编码串行化该数据。

## 9．abort()方法
该方法可以暂停一个HttpRequest的请求发送或者HttpResponse的接收，并且将XMLHttp Request对象设置为初始化状态。

## 10．setRequestHeader()方法
该方法用来设置请求的头部信息。当readyState属性值为1时，可以在调用open()方法后调用这个方法；否则将得到一个异常。setRequestHeader（header,value）方法包含两个参数：前一个是header键名称，后一个是键值。

## 11．getResponseHeader()方法
此方法用于检索响应的头部值，仅当readyState属性值是3或4（即在响应头部可用以后）时，才可以调用这个方法；否则，该方法返回一个空字符串。此外还可以通过getAllResponse Headers()方法获取所有的HttpResponse的头部信息。
