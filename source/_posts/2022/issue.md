---
title: '问题合集'
category: 技术
tags: [笔记, 前端]
date: 2020-7-14
---

一些日常问题记录，方便日后回顾。

<!-- more -->

### js 怎么写一个链式调用的方法

### antd 日期组件不兼容 dayjs

### npm 包里面命令和全局命令冲突

npx 调用项目内的命令,直接命令是调用全局

### Omit 有什么用

### formatMessage 为什么不能直接用

### 科学上网后，git push 443

我的情况是使用 ssh 进行提交，各种方法试了一遍都是时好时坏，remote 缓存 https 后再也没出过问题

~~设置代理
git config --global http.proxy socks5://127.0.0.1:7890
git config --global https.proxy socks5://127.0.0.1:7890~~

### @babel/generator 生成字符串特殊字符被转义

增加选项{ jsescOption: { minimal: true }

```js
generate(ast, { jsescOption: { minimal: true } });
```

### Node.js 中读取文件后用 Json.parse 方法报错

**问题详细描述：**
文件 a

```js
const json = `{
    "a":123
}';
export default JSON.parse(json);
```

文件 b 通过 fs 读取文件 a，截取`{ "a":123 }'后 Json.parse 报错
**解法：**
文件读取后本身是字符串，加上截取的首位引号产生报错，去除首位引号即可

### git 查看提交数量

`git log | grep "^Author: " | awk '{print $2}' | sort | uniq -c | sort -k1,1nr`

### node 中如果导入 ts 文件

pirates+esbuild 实现动态编译，对导入的 ts 编译后再导入
