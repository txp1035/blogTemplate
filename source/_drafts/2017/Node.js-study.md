---
title: 'Node.js学习笔记'
category: 技术
tags: 学习笔记
date: 2017-12-09
---

学习 node.js 的笔记

<!-- more -->

# 1

为什么使用 Node.js？  
Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境，它将 JavaScript 编程语言扩展到服务端开发。  
Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。  
Node.js 的包管理器 npm，是全球最大的开源库生态系统。  
Node.js 安装  
打开[Node.js 官网](https://nodejs.org/en/)下载 LTS 版本即可。Windows 安装直接双击 msi 文件，一直下一步即可完成安装。  
REPL（交互式解释器）  
打开命令行，运行`node`进入 REPL  
编写首个服务器程序

```
var http = require('http');
http.createServer(function (req, res) {
res.writeHead(200, {'Content-Type': 'text/plain'});
res.end('Hello World\n');
}).listen(8124, "127.0.0.1");
console.log('Server running at http://127.0.0.1:8124/');
```
