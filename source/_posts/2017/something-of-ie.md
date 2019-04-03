---
title: '判断IE版本的HTML语句'
category: 技术
tags: [前端]
date: 2017-08-14

---

IE那些事...

<!-- more -->
经常用一些框架会看到类似注释一样的语句，例如bootstrap里的：

```html
<!--[if lt IE 9]>
    <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
    <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
```

写了这个代码就能兼容IE8了。那么这些代码是什么意思呢？我们来看下面例子：

```html
<!--[if !IE]>除IE外都可识别 <![endif]-->
<!--[if IE]> 所有的IE可识别 <![endif]-->
<!--[if IE 6]> 仅IE6可识别 <![endif]-->
<!--[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-->
<!--[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-->
<!--[if IE 7]> 仅IE7可识别 <![endif]-->
<!--[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-->
<!--[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-->
<!--[if IE 8]> 仅IE8可识别 <![endif]-->
<!--[if IE 9]> 仅IE9可识别 <![endif]-->
```

| 语句   | 例子                     | 说明                                                                        |
| ------ | ------------------------ | --------------------------------------------------------------------------- |
| !      | [if !IE]                 | NOT运算符。这是摆立即在前面的功能，操作员，或子表达式扭转布尔表达式的意义。 |
| lt     | [if lt IE 5.5]           | 小于运算符。如果第一个参数小于第二个参数，则返回true。                      |
| lte    | [if lte IE 6]            | 小于或等于运算。如果第一个参数是小于或等于第二个参数，则返回true。          |
| gt     | [if gt IE 5]             | 大于运算符。如果第一个参数大于第二个参数，则返回true。                      |
| gte    | [if gte IE 7]            | 大于或等于运算。如果第一个参数是大于或等于第二个参数，则返回true。          |
| ()     | [if !(IE 7)]             | 子表达式运营商。在与布尔运算符用于创建更复杂的表达式。                      |
| &      | [if (gt IE 5)&(lt IE 7)] | AND运算符。如果所有的子表达式计算结果为true，返回true                       |
| &#124; | [if (IE 6)&#124;(IE 7)]  | OR运算符。返回true，如果子表达式计算结果为true。                            |