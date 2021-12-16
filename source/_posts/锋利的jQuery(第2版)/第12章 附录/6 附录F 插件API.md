---
categories:
  - 锋利的jQuery(第2版)
  - 第12章 附录
abbrlink: 43daea3b
---
# 附录F 插件API
## F.1 Validation插件API
Validation插件有两个经常被用到的选项，分别是方法（method）和规则（rule）。
（1）方法。验证方法就是通过执行验证逻辑判断一个元素是否合法。例如 email()方法就是检查当前文本格式是否是正确的E-mail格式。读者能很方便地利用Validation插件提供的方法来完成验证。另外，读者也可以自定义方法。
（2）规则。验证规则将元素和元素的验证方法关联起来，例如验证一个需要E-mail格式和必填的属性name为email的元素，可以定义该元素的规则如下：

[插图]

- 插件方法如表F-1所示。

<center>表F-1 插件方法</center>

[插图]

- 内置验证规则如表F-2所示。

<center>表F-2 内置验证规则</center>

[插图]

- Validator

Validation验证会返回一个Validator对象，validator对象可以帮助用户触发validation程序或者改变form的内容。validator对象更多的方法如表F-3所示。

<center>表F-3 validator对象的方法</center>

[插图]

validator对象中的静态方法如表F-4所示。

<center>表F-4 validator对象中的静态方法</center>

[插图]

- 实用项

<center>表F-5 实用项</center>

[插图]

- 普通选择器

<center>表F-6 普通选择器</center>

[插图]

## F.2 Form插件API
（1）Form插件API

Form插件拥有很多方法，这些方法可以使用户很容易地管理表单数据和提交表单。

- ajaxForm()

增加所需要的事件监听器，为Ajax 提交表单做好准备。AjaxForm()方法并没有提交表单，而是在$(document).ready()方法中，使用ajaxForm()方法来为Ajax提交表单做好准备。ajaxForm方法可以接受0个或1个参数。单个的参数既可以是一个回调函数，也可以是一个Options对象。此方法可以进行链式操作。

例子：

[插图]

- ajaxSubmit()

立即通过Ajax方式提交表单。在大多数情况下，都是调用ajaxSubmit()方法来响应用户的提交表单操作。AjaxSubmit()方法可以接受0个或1个参数。单个的参数既可以是一个回调函数，也可以是一个Options对象。此方法可以进行链式操作。

例子：

[插图]

- formSerialize()

该方法将表单中所有的元素串行化（序列化）为一个字符串。formSerialize()方法会返回一个格式化好的字符串，格式如下：

[插图]

因为返回的是字符串，而不是jQuery对象，所以该方法不能进行链式操作。

例子：

[插图]

- fieldSerialize()

fieldSerialize()方法将表单的字段元素串行化（序列化）成一个字符串。当用户只需要串行化表单的一部分时就可以用到该方法了。fieldSerialize()方法会返回一个格式化后的字符串，格式如下：

[插图]

因为返回的是字符串，所以该方法不可以进行链式操作。

例子：

[插图]

- fieldValue()

fieldValue()方法把匹配元素的值插入到数组中，然后返回这个数组。从0.91版本起，该方法总是以数组的形式返回数据，如果元素值被判定无效，则数组为空，否则数组将包含一个或多个元素值。fieldValue()方法返回一个数组，因此不可以进行链式操作。

例子：

[插图]

- resetForm()

该方法通过调用表单元素原有的DOM 方法重置表单到初始状态。resetForm()方法可以进行链式操作。

例子：

[插图]

- clearForm()

clearForm()方法用来清空表单中的元素。该方法将所有的文本框（text）、密码框（password）和文本域（textarea）元素置空，清除下拉框（select）元素的选定以及将所有的单选按钮（radio）和多选按钮（checkbox）重置为非选定状态。clearForm()方法可以进行链式操作。

例子：

[插图]

- clearFields()

clearFields()方法用来清空字段元素。当用户需要清空一部分表单元素时就会用到该方法。clearFields()方法可以进行链式操作。

例子：

[插图]

（2）ajaxForm and ajaxSubmit的Options对象

ajaxForm()方法和ajaxSubmit()方法支持许多选项，这些选项都可以通过Options对象来设置。Options对象是一个简单的JavaScript对象，包含了如下属性与值的集合。

- target

指明页面中根据服务器响应进行更新的元素。这个值可能是一个特殊的jQuery选择器字符串、一个jQuery对象或者一个DOM元素。

默认值：null。

- url

将表单元素提交到指定的url中。

默认值：表单action属性的值。

- type

指定提交表单数据的方法（method）：GET或POST。

默认值：表单method属性的值（如果没有找到，则为GET）。

- beforeSubmit

表单提交前的回调函数。beforeSubmit回调函数被用来运行预提交逻辑或者校验表单数据。假如beforeSubmit回调函数返回false，则表单将不会被提交。beforeSubmit回调函数有3个参数：数组形式的表单数据、jQuery表单对象和传递给ajaxForm()方法或ajaxSubmit()方法的Options对象。表单数据数组遵循以下数据格式（json类型）。

[插图]

默认值：null。

- success

表单成功提交后调用的回调函数。假如success回调函数被指定，将在服务器返回响应后被调用。success函数可以传回responseText或者responseXML的值（决定值的数据类型是dataType选项）

默认值：null。

- dataType

期望的服务器响应的数据类型，可以是null、xml、script或者json。dataType提供了指定的方法以便控制服务器的响应。这个指定的方法将被直接地反映到jQuery.httpData()方法中。dataType支持以下格式。

- xml。如果dataType被指定为xml，服务器返回内容将被作为XML来对待。同时，如果“success”回调函数被指定，responseXML的值将会传递给回调函数。
- json。如果dataType被指定为json，服务器返回内容将被执行，如果“success”回调函数被指定，返回的内容将会传递给回调函数。
- script。如果dataType被指定为script，服务器返回内容将被放在全局环境中执行。

默认值：null。

- semantic

是否需要定义为严格的语义格式。注意，普通的表单序列化要遵循的语义不能包括type 属性为image的input元素。假如服务器有严格的语义要求，而表单也至少包含一个type="image"元素的时候，那么必须设置semantic选项为true。

默认值：false。

- resetForm

表单是否在提交成功后被重置。

默认值：null。

- clearForm

表单是否在提交成功后被清空。

默认值：null。

- iframe

表单是否总是将服务器响应指向到一个iframe。iframe在文件上传时会很有用。

默认值：false。

- data

包含额外数据的对象通过form形式提交。

[插图]

- error

错误时的回调函数。

- beforeSerialize

回调函数被调用前被序列化。它可以在调用之前检索其值的形式。它带有两个参数：form对象和ajaxForm/ ajaxSubmit传递过来的options对象。

[插图]

默认值：null。

- replaceTarget

可选，与target选项一起使用。如果想将目标元素一起替换掉，请设为true，如果只想替换目标元素的内容，则设为false。

默认值：false。在v2.43后增加。

- iframeSrc

字符串值，当/如果使用iframe时作为iframe的src属性。

默认值：about:blank

网页使用https协议时默认值为：javascript:false

- forceSync

布尔值，当上传文件（或使用iframe选项）时，提交表单前为了消除短延迟，设置为true。延迟的使用是为了让浏览器渲染DOM更新前执行原有的表单submit。这时显示一条信息告知用户，如：“请稍等...”，会改善可用性。

默认值：false。在v2.38后增加。

- uploadProgress

上传进度信息（如果浏览器支持）回调函数。回调传递以下参数：
1）event：浏览器事件
2）position：位置（整数）
3）total：总长度（整数）
4）percentComplete：完成度（整数）

默认值：null

- iframeTarget

使用iframe元素作为响应文件上传目标。默认情况下，该插件将创建一个临时的iframe元素来捕捉上传文件时的反应。此选项允许您使用现有的iframe，如果你想。使用此选项时，插件对来自服务器的响应不作任何处理。

默认值：null。在v2.76后增加。

（3）Form插件实例

[插图]

注意，利用此Options对象，可以将值传给jQuery的$.ajax()方法。假如用户熟悉$.ajax()方法提供的options对象，那么可以利用它们来将Options对象传递给ajaxForm()方法和ajaxSubmit()方法。

## F.3 SimpleModal插件API
API的官方网站地址为：http://www.ericmmartin.com/projects/simplemodal/

<center>表F-7 SimpleModal插件的API</center>

[插图]

## F.4 Cookie插件API
API的官方网站地址为：https://github.com/carhartl/jquery-cookie

- 写入Cookie。

[插图]

<div style="border:1px solid;"><strong>注意</strong>：“the_cookie”为待写入的Cookie名，“the_value”为待写入的值。</div>

- 删除Cookie。

[插图]

<div style="border:1px solid;"><strong>注意</strong>：“the_cookie”为Cookie名，设置为null即删除此Cookie。必须使用与之前设置时相同的路径（path）和域名（domain），才可以正确删除Cookie。
</div>

- 其他可选参数。

[插图]

<div style="border:1px solid;">
<strong>注意</strong>：
- expires：（Number|Date）有效期。可以设置一个整数作为有效期（单位：天），也可以直接设置一个日期对象作为Cookie的过期日期。如果指定日期为负数，例如已经过去的日子，那么此Cookie将被删除；如果不设置或者设置为null，那么此Cookie将被当作Session Cookie处理，并且在浏览器关闭后删除。
- path：（String）cookie的路径属性。默认是创建该Cookie的页面路径。
- domain：（String）cookie的域名属性。默认是创建该Cookie的页面域名。
- secure：（Boolean）如果设为true，那么此Cookie的传输会要求一个安全协议，例如HTTPS。

</div>