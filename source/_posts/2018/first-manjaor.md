---
title: '初探manjaor'
category: 技术
tags: [数据库]
date: 2018-01-02
---

第一次使用 manjaor...

<!-- more -->

## 写在前面

在[distrowatch](http://www.distrowatch.org/)中发行版排行第一的 Linux,兼顾性能和易用的版本,抱着这样的心情我开始使用它.首先下载的官方推荐的 XFCE 版,不习惯这个桌面,之后下载了社区版的 Deepin 桌面.
桌面选好就开始装软件,刚开始搜索到的都是通过命令`pacman`安装,配置许久就是不成功,说好的易用呢?就这样折腾了几次.趁着国庆假期长,再来折腾一下,让我找到了 manjaor 的正确使用姿势.

## 安装中文输入法

1 打开软件包管理器
2 搜索 fcitx-im 会出现六个包(fcitx 配置|fcitx|fcitx-gtk2|fcitx-gtk3|fcitx-qt4|fcitx-qt5),勾起全部,点击应用即可安装.
3 搜索 fcitx-configtool 会出现三个包(fcitx 配置|fcitx|fcitx-configtool),由于前两个装过了,只需要装第三包即可.
4 搜索 fcitx 可以看到很多包,我们装一个谷歌拼音 fcitx-googlepinyin.
5 配置.xprofile 文件,在~目录中找到.xprofile 文件,没有的话就创建一个,文件中写入以下内容并保存,然后重启就可以使用中文输入法了.

```js
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx
```
