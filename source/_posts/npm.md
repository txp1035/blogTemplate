---
title:  "npm"
category: 工具
tags: 前端
date: 2017-12-12
---
## 常用命令
### npm install 安装模块
安装模块分全局安装和本地安装。全局安装是安装在npm默认目录，在这个电脑上的项目都可以使用全局安装的模块；本地安装是将模块安装在当前目录中，这些模块只能供当前目录的项目使用。  
本地安装模块（moduleName是模块名字）：
```
npm install moduleName
```
全局安装模块（moduleName是模块名字）：
```
npm install -g moduleName
``` 
### npm uninstall 卸载模块
卸载模块（moduleName是模块名字）：
```
npm uninstall moduleName
``` 
### npm update 更新模块
更新模块（moduleName是模块名字）：
```
npm update moduleName
``` 
### npm ls 查看安装的模块
```
npm ls
``` 
```
npm ls --depth=0 //查看模块的第一个文件夹名
```