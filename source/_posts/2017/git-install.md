---
title: 'git安装'
category: 工具
tags: [版本控制]
date: 2017-12-18
---

git 安装...

<!-- more -->

## windwos 版

打开[git 官网](https://git-scm.com/)下载最新版的 git，如下图
![git下载示例](/assets/img/2017/12-18-1.png)
下载完成后一直点下一步即可完成安装。

## github

1、如何 fork 项目后与原作者保持同步

fork 别人的项目后，把自己名下 fork 别人的项目 clone 到本地后，如何与作者的项目保持同步,
如我 fork 了：`https://github.com/alitajs/milady`,该仓库到我的名下变为：`https://github.com/ShawDanon/milady`并把`https://github.com/ShawDanon/milady`clone 到本地，想要与作者同步

1、git remote add milady https://github.com/alitajs/milady
milady 是关联的原仓库在我本地的名字，可以自定义。git remote -v 可以查看添加的新的数据源
