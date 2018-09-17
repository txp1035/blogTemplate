---
title:  "尝试hexo"
category: 技术
tags: [前端,博客搭建]
date: 2017-12-13
---
由于用node比较多，所以想试试基于node的hexo。  
### 准备
搭建hexo前需要先装node。打开[Node.js官网](https://nodejs.org/en/)下载LTS版本即可。Windows安装直接双击msi文件，一直下一步即可完成安装。  
### 安装hexo
打开命令行，输入`npm install hexo-cli -g`。
### 建立你的博客
打开命令行，输入`hexo init blog`。然后就会在当前目录创建一个名为blog的文件夹，这个就是你的博客文件了。
### 运行你的博客
进入你的博客目录，打开命令行，输入`hexo server`。你就可以在`http://127.0.0.1:4000/`访问你的博客了。
### GitHub部署博客
新建仓库 
打开_config.yml,进行基础配置
```
deploy:
  type: git
  repo: https://github.com/...... 仓库地址
```
安装hexo-deployer-git自动部署发布工具
```
npm install hexo-deployer-git  --save
```
发布到Github
```
hexo clean && hexo g && hexo d
```