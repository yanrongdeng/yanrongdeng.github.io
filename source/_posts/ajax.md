---
title: ajax的学习笔记
date: 2021-07-06 17:39:29
tags: AJAX
categories: 学习笔记
---

# AJAX是什么
AJAX - Asynchronous JavaScript And XML - 异步的 JavaScript 和 XML

该方法能够让Web浏览器在不刷新页面的情况下与服务器交换数据。

> 当使用结合了这些技术的 AJAX 模型以后， 网页应用能够快速地将增量更新呈现在用户界面上，而不需要重载（刷新）整个页面。这使得程序能够更快地回应用户的操作。

# XMLHttpRequest
`XMLHttpRequest()`用于和服务器交换数据。

发送一个HTTP请求时，需要创建一个 XMLHttpRequest 对象，打开一个URL，发送请求，服务器会返回 HTTP 状态码及响应主体。
```js
var xmlHttp = new XMLHTTPRequest();
```
值得一提的是，IE6 及以前版本的IE用的都是`ActiveXObject`。2021年了，还有人用 IE6 吗？

# 发送请求
使用 `XMLHttpRequest` 对象的 `open()` 和 `send()` 方法。
```js
xmlHttp.open("GET","https://kawashiro_ryofu.gitee.io/blogimagerc/index.html",true)
xmlHttp.send();
```
## open()方法
语法：`xmlHttp.open(method, url, async, user, passwd);`

~ `xmlHttp`: 创建的 XMLHttpRequest 对象
~ `method`: 要使用的HTTP方法。常用的是 GET 和 POST
~ `url`: 要向其发送请求的URL
~ `async`: 可选参数。布尔类型。表示是否异步操作，默认为 true。如果为 false，`send()` 方法直到收到答复前不会返回
~ `user`: 可选参数。用于认证用途，用户名
~ `passwd`: 可选参数。用于认证用途，密码

## send()方法
语法：`xmlHttp.send(body);`

~ `body`: 可选参数。在 `XMLHttpRequest` 请求中要发送的数据体，默认为 null 。仅用于 POST 请求

## GET还是POST
一言蔽之，`GET` 适用于大多数请求（与 POST 相比，GET 更简单也更快）。

在以下情况中，请使用 POST 请求：

> - 无法使用缓存文件（更新服务器上的文件或数据库）
> - 向服务器发送大量数据（POST没有数量限制）
> - 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

### GET
```js
xmlHttp.open("GET","https://kawashiro_ryofu.gitee.io/blogimagerc/index.html",true);
xmlHttp.send();
```

执行上面的例子，浏览器可能返回缓存的数据。

简单粗暴的解决方案：
```js
xmlHttp.open("GET","https://kawashiro_ryofu.gitee.io/blogimagerc/index.html?t=" + Math.random(),true);
xmlHttp.send();
```
只需要向URL中添加一个无用的随机参数就可以了。

### POST
```js
xmlHttp.open("POST","https://www.runoob.com/try/ajax/demo_post2.php" + Math.random(),true);
xmlHttp.setRequestHeader("Content-type","application/x-www-form-urlencoded"); //向请求添加HTTP头
xmlHttp.send("fname=河城&lname=荷取") //参数
```
# 头部信息

## 设置header

语法：`xmlHttp.setRequestHeader(key,value);`

~ `key`: 规定HTTP头的名称
~ `value`: 规定头的值

## 获取header

语法：`xmlhttp.getAllResponseHeaders();` 检索资源（文件）的头信息。

语法：`xmlHttp.getResponseHeader(key)` 检索资源（文件）的指定头信息。

```js
xmlhttp.getResponseHeader('Last-Modified');
```

# 异步还是同步
多数情况下，`async`应设置为`true`，表示异步。但有时 async=false 更合适。

对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。

通过 AJAX，JavaScript 无需等待服务器的响应，而是：
 + 在等待服务器响应时执行其他脚本
 + 当响应就绪后对响应进行处理

## Async = true

当使用 `async=true` 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：

```js
xmlHttp.onreadystatechange=function()
{
    if (xmlHttp.readyState==4 && xmlHttp.status==200)
    {
        document.getElementById("myDiv").innerHTML = xmlHttp.getAllResponseHeaders();
    }
}
xmlHttp.open("GET","/try/ajax/ajax_info.txt",true);
xmlHttp.send();
```

## Async = false

如需使用 `async=false`，请将 open() 方法中的第三个参数改为 false：

```js
xmlHttp.open("GET","test1.txt",false);
```

非必要情况，不推荐使用 async=false（同步），JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。

**注意：** 使用 async=false 时，不要编写 onreadystatechange 函数， 把代码放到 send() 语句后面即可：

``` js
    xmlHttp.open("GET","/try/ajax/ajax_info.txt",false);
    xmlHttp.send();
    document.getElementById("myDiv").innerHTML=xmlHttp.responseText;
```

# 服务器响应
接收服务器响应数据，应使用 `responseText` 或 `responseXML` 属性。二者的区别在于，前者默认获得文本（字符串）数据，后者会解析 XML。

## responseText

```js
console.log(xmlHttp.responseText)
```

## responseXML

~~什么时候推出一个“responseJson”啊~~

```js
xmlDoc=xmlHttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
{
    txt=txt + x[i].childNodes[0].nodeValue + "<br>";
}
document.getElementById("myDiv").innerHTML=txt;
```

# onreadystatechange事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

下面是 XMLHttpRequest 对象的三个重要的属性：

`onreadystatechange`	存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
`readyState`	存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
>   0 : 请求未初始化
    1 : 服务器连接已建立
    2 : 请求已接收
    3 : 请求处理中
    4 : 请求已完成，且响应已就绪

`status`	200 : "OK"  &nbsp;&nbsp;  404 : 未找到页面

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

当 readyState 等于 4 且状态为 200 时，表示响应已就绪：

``` js
xmlHttp.onreadystatechange=function()
{
    if (xmlHttp.readyState==4 && xmlHttp.status==200)
    {
        document.getElementById("myDiv").innerHTML= xmlHttp.responseText;
    }
}
```
**注意：** onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化。

# 参考
+ [AJAX 教程 | 菜鸟教程 - RUNOOB.COM](https://www.runoob.com/ajax/ajax-intro.html)

+ [Ajax - Web 开发者指南 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX)

+ [笔记·AJAX](https://www.kawashiros.club/p/2020/46134e8e)