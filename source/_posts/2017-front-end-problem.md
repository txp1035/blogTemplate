---
title: "前端问题"
category: 技术
tags: 前端
date: 2017-09-22
---

前端遇到的一些问题汇总。

<!-- more -->

### 跨页面传值问题

#### 一、地址栏传值方式

原理是把参数放入跳转页面的 url 里，跳转页面后读取当前页面的 url 就可以获得上一个页面传过来的参数。  
下面代码是通过 JS 跳转到 www.tangxiaoping.top/search 页面，传入`?a=1&b=1`字符串。通常我们使用`?`来隔断 url 和需要传入的字符串，用`&`隔断不同的参数，用`=`隔断参数和参数对应的值。

```
window.location.href = "https://www.tangxiaoping.top/search?a=1&b=1";
```

那么跳转完页面我们就需要获取我们需要的参数了。通过下面的方法获得带有参数的对象，通过对象获取我们需要的值。

```
var obj = parseURL(location.href);//调用解析url方法，传入参数为url，将返回值赋值给obj
function parseURL(url) {
    var str = url.split("?")[1];//获取?后面的字符串
    var strArr = str.split("&");//通过&符号把str分割成字符串数组
    var obj = {};//定义一个对象
    var arr = [];//定义一个数组
    for (var i = 0; i < strArr.length; i++) {
        arr = strArr[i].split("=");//通过=符号把strArr分割成字符串数组
        obj[arr[0]] = arr[1];//把=左边的字符串设为obj属性，把=右边的字符串设为值
    }//将strArr遍历一遍
    return obj;//返回一个对象（包括我们需要的参数和值）
}//解析url的方法
```

#### 二、session

#### 三、Cookies

#### 四、Application

### 在 js 中引入其他 js

使用场景：多个页面需要引入多个相同的 js 时、多个页面引入 js 的 src 需要频繁更改时  
一、如下代码所示，在公共 js 中使用 document.write 来同步引入其他 js。  
index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="common.js"></script>
</head>
<body>
</body>
</html>
```

common.js

```
document.write("<script src=''></script>"); //src自行填写
```

二、如下代码所示，通过 appendChild 异步引入其他 js

```
var js = document.createElement("script"); //创建标签元素
js.src = ""; //给标签src赋值，src自行填写
document.head.appendChild(js); //将标签动态加入head里
```

### ready()用法

当 DOM（文档对象模型） 已经加载，并且页面（包括图像）已经完全呈现时，会发生 ready 事件。  
由于该事件在文档就绪后发生，因此把所有其他的 jQuery 事件和函数置于该事件中是非常好的做法。正如上面的例子中那样。  
ready() 函数规定当 ready 事件发生时执行的代码。  
ready() 函数仅能用于当前文档，因此无需选择器。  
允许使用以下三种语法：  
语法 1

```
$(document).ready(function)
```

语法 2

```
$().ready(function)
```

语法 3

```
$(function)
```

### JavaScript 刷新页面

`location.reload()`
