---
title: '2019面试经历'
category: 技术
tags: [总结, 前端]
date: 2019-2-19
---

希望有个好的 offer...

<!-- more -->

# 面试

## 博彦科技

### 博彦科技电面一

问题：react 子组件向父组件传值都有哪儿些技术方法？

1. 父组件通过 props 传递带参数的函数给子组件，子组件调用这个函数，把需要传递给父组件的参数传给这个函数的参数。
2. react-redux

问题：es6 箭头函数和普通函数的区别？
箭头函数没有自己的 this，它会捕获上下文的 this 作为自己的 this 值。普通函数 this 指向有四种：一、作为方法调用时，在对象中的方法指向该对象；二、作为函数调用时，指向 window；三、作为构造函数调用时，指向实例对象；四、使用 apply、call、bind 调用时，指向绑定的 this。

问题：浅拷贝都有哪儿些方法？
赋值、object.assign()

问题：你们主要用哪儿些方法跨域？
cors

## 阿里巴巴(ICBU 技术部)

### 阿里巴巴电面一

问题：自我介绍

问题：CMS 项目讲解
smis 系统和隔壁仓库管理系统。

smis 系统问题：怎么保证数据实时性，怎么校验数据，数据安全？

smis 系统问题：用户量有多大？

smis 系统问题：生命体征检测系统有哪儿些数据和维度？

smis 系统问题：生命检测系统数据怎么处理的？

隔壁仓库管理系统问题：

隔壁仓库管理系统问题：负责模块？

隔壁仓库管理系统问题：前端技术体系是什么？

隔壁仓库管理系统问题：有没有遇到过 ant design 组件不能解决的问题？

隔壁仓库管理系统问题：react 组件间通信？

隔壁仓库管理系统问题：有没有遇到过长列表或者复杂的表单，遇到性能问题，做过优化？

隔壁仓库管理系统问题：react-router 实现？

隔壁仓库管理系统问题：react 生命周期？

阿里(ICBU 技术部)：

对外场景 PC：jQuery 技术体系（脚手架、框架、组件）
卖家端：react（脚手架、组件库）
无限：weex
可视端：egg（node 应用）
内部系统：ant design

## 蚂蚁金服（成都中软国际外包）

### 面试问题

使用的技术栈介绍
询问 js 和 css 偏向
询问 umi 配置按需加载
问 react 版本，考验新版本功能
新版本生命周期区别
webpack 询问，拒绝了
react route 问题
react router link 和 a 标签区别
redux 问题
redux reducer 为什么要用纯函数
react 优化相关 我回答的 milady
key 作用
react 的异步渲染说一下
setstate 方法
react 的受控组建和非受控组件区别
react 和高阶组件和普通组件区别，举例 redux 是高阶组件
connect
组件通讯方法
context 了解过嘛
hooks 常用的用法（比较常用）

js 相关
类的继承 es5 方法
混合法这些（）
变量作用域链
call aplay bind 区别
防抖节流怎么实现的用来干嘛的
loash 知道吗
深拷贝实现
异步方法
事件循环
type of 和 instant 区别
跨域方法，cross 原理
闭包场景询问，避开了
let const
var 变量申明提升
let const 有没有提升
antd 组件样式修改
js 事件委托事件冒泡事件捕获描述
说下如何阻止事件冒泡
用过 echart 什么库
ts form 表单需要哪儿些处理
h5 新的跨域方法是哪儿个
post massage
react 组件定义方式
component PureComponent memo
和 pcm 差不多
通过什么方式访问后端接口的

hooks 了解下，react 原理，新的 API 用法。

### 面试总结

不熟悉的知识吞吞吐吐，熟悉的只是语速过快，甚至没听完面试官问题就开始抢答，
