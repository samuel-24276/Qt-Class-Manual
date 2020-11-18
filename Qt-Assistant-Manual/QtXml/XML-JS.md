XML JavaScript

# 1.XMLHTTP Request

## 1.1.XMLHttpRequest 对象

`XMLHttpRequest` 对象用于在后台与服务器交换数据。

`XMLHttpRequest `对象是**开发者的梦想**，因为您能够：

- 在不重新加载页面的情况下更新网页
- 在页面已加载后从服务器请求数据
- 在页面已加载后从服务器接收数据
- 在后台向服务器发送数据



## 1.2.创建一个 XMLHttpRequest 对象

所有现代浏览器（IE7+、Firefox、Chrome、Safari 和 Opera）都有内建的` XMLHttpRequest` 对象。

创建 XMLHttpRequest 对象的语法：

`xmlhttp=new XMLHttpRequest();`

旧版本的Internet Explorer（IE5和IE6）中使用 ActiveX 对象：

`xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");`

在下一章中，我们将使用 XMLHttpRequest 对象从服务器取回 XML 信息。

# 2.XML Parser

所有现代浏览器都有内建的 XML 解析器。

**XML 解析器把 XML 文档转换为 XML DOM 对象 - 可通过 JavaScript 操作的对象。**

## 2.1.解析 XML 文档

下面的代码片段把 XML 文档解析到 XML DOM 对象中：

```js
if (window.XMLHttpRequest)
{// code for IE7+, Firefox, Chrome, Opera, Safari
	xmlhttp=new XMLHttpRequest();
}
else
{// code for IE6, IE5
	xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
xmlhttp.open("GET","books.xml",false);
xmlhttp.send();
xmlDoc=xmlhttp.responseXML;
```

## 2.2.解析 XML 字符串

下面的代码片段把 XML 字符串解析到 XML DOM 对象中：

```js
txt="<bookstore><book>";
txt=txt+"<title>Everyday Italian</title>";
txt=txt+"<author>Giada De Laurentiis</author>";
txt=txt+"<year>2005</year>";
txt=txt+"</book></bookstore>";

if (window.DOMParser)
{
	parser=new DOMParser();
	xmlDoc=parser.parseFromString(txt,"text/xml");
}
else // Internet Explorer
{
	xmlDoc=new ActiveXObject("Microsoft.XMLDOM");
	xmlDoc.async=false;
	xmlDoc.loadXML(txt);
}
```



> **注释：**Internet Explorer 使用 loadXML() 方法来解析 XML 字符串，而其他浏览器使用 DOMParser 对象。

## 2.3.跨域访问

出于安全方面的原因，现代的浏览器不允许跨域的访问。

这意味着，网页以及它试图加载的 XML 文件，都必须位于相同的服务器上。

# 3.XML DOM

XML DOM（XML Document Object Model 文档对象模型）定义了访问和操作 XML 文档的标准方法。

**XML DOM 把 XML 文档作为树结构来查看。**

所有元素可以通过 DOM 树来访问。可以修改或删除它们的内容，并创建新的元素。元素，它们的文本，以及它们的属性，都被认为是节点。

## 3.1.加载一个 XML 文件 - 跨浏览器实例

下面的实例把 XML 文档（"[note.xml](https://www.runoob.com/try/xml/note.xml)"）解析到 XML DOM 对象中，然后通过 JavaScript 提取一些信息：

```xml
<html>
<body>
<h1>W3Schools Internal Note</h1>
<div>
	<b>To:</b> <span id="to"></span><br />
	<b>From:</b> <span id="from"></span><br />
	<b>Message:</b> <span id="message"></span>
</div>

<script>
if (window.XMLHttpRequest)
{// code for IE7+, Firefox, Chrome, Opera, Safari
	xmlhttp=new XMLHttpRequest();
}
else
{// code for IE6, IE5
	xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
xmlhttp.open("GET","note.xml",false);
xmlhttp.send();
xmlDoc=xmlhttp.responseXML;

document.getElementById("to").innerHTML=
xmlDoc.getElementsByTagName("to")[0].childNodes[0].nodeValue;
document.getElementById("from").innerHTML=
xmlDoc.getElementsByTagName("from")[0].childNodes[0].nodeValue;
document.getElementById("message").innerHTML=
xmlDoc.getElementsByTagName("body")[0].childNodes[0].nodeValue;
</script>

</body>
</html>
```

> 重要注释!!!!!
>
> 如需从上面的 XML 文件（"note.xml"）的 <to> 元素中提取文本 "Tove"，语法是：getElementsByTagName("to")[0].childNodes[0].nodeValue请。注意，**即使 XML 文件只包含一个 <to> 元素，您仍然必须指定数组索引 [0]**。这是因为 getElementsByTagName() 方法返回一个数组。

------

## 3.2.加载一个 XML 字符串 - 跨浏览器实例

下面的实例把 XML 字符串解析到 XML DOM 对象中，然后通过 JavaScript 提取一些信息：

```xml
<html>
<body>
<h1>W3Schools Internal Note</h1>
<div>
	<b>To:</b> <span id="to"></span><br />
	<b>From:</b> <span id="from"></span><br />
	<b>Message:</b> <span id="message"></span>
</div>

<script>
if (window.XMLHttpRequest)
{// code for IE7+, Firefox, Chrome, Opera, Safari
	xmlhttp=new XMLHttpRequest();
}
else
{// code for IE6, IE5
	xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
xmlhttp.open("GET","note.xml",false);
xmlhttp.send();
xmlDoc=xmlhttp.responseXML;

document.getElementById("to").innerHTML=
xmlDoc.getElementsByTagName("to")[0].childNodes[0].nodeValue;
document.getElementById("from").innerHTML=
xmlDoc.getElementsByTagName("from")[0].childNodes[0].nodeValue;
document.getElementById("message").innerHTML=
xmlDoc.getElementsByTagName("body")[0].childNodes[0].nodeValue;
</script>

</body>
</html>
```

