---
title: '我的第一个umi插件'
category: 技术
tags: [笔记, 前端]
date: 2019-6-20
---

通过 swagger 快速生成 servers 和 mock 的 umi 插件

<!-- more -->

## 一个简单的插件例子

最简单的插件就是在本地建立一个文件，例如在 umi 项目根目录创建一个 plugin.js 的文件，文件内容如下：

```js
export default (api, opts) => {
  api.registerCommand('test', args => {
    console.log('this is test');
  }); //命令api，输入umi [命令]即可运行内部代码
}; //基本格式，api参数是官方提供的api，opts是配置文件的参数
```

然后在.umirc.js 中配置如下既可使用`umi test`运行写好的插件，会看到控制台输出`this is test`。

```js
export default {
  plugins: ['./plugin.js']
};
```

同理我们可以把插件封成一个包，方便使用和维护。

## 我的插件

首先通过建立文件夹`umi-plugin-swagger`，
