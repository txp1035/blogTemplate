---
title: 'macOS软件折腾记'
category: 技术
tags: [笔记, 前端]
date: 2019-3-14
---

快买 mac mini 一个月了，记录下使用体验和常用软件安装...

<!-- more -->

## 需要解决的功能

1. 通过编辑器快速打开项目

## 软件安装

### zip 类型软件（双击解压，将程序拖到应用程序即可）

[vscode](https://code.visualstudio.com/)：编辑器
[item2](https://www.iterm2.com/)：终端
[Gas Mask](https://github.com/2ndalpha/gasmask)：修改 host
[Android Studio 中文网](http://www.android-studio.org/)：安卓开发
[KeepingYouAwake](https://github.com/newmarcel/KeepingYouAwake)：可保证系统不自动休眠
[f.lux](https://justgetflux.com/)：调节显示器色温，护眼，尤其是早上起来屏幕实在是刺眼
[AppCleaner](http://freemacsoft.net/appcleaner/)：卸载软件

### dmg 类型软件（双击安装）

[Android Studio 官网|科学上网](https://developer.android.google.cn/studio/)：安卓开发
[Lantern](https://github.com/getlantern/download/wiki)：科学上网
[Karabiner Element](https://pqrs.org/osx/karabiner/index.html)：键盘设置
[qBittorrent](https://www.qbittorrent.org/)：下载工具，下 magnet
[Folx 5|科学上网](https://mac.eltima.com/download-manager.html)：下载工具，下 http
[IINA](https://iina.io/)：视频播放器
[keka](https://www.keka.io/en/)：解压、压缩软件
[欧路词典](https://www.eudic.net/v4/en/app/eudic)：单词查询
[itsycal](https://www.mowglii.com/itsycal/)：日历软件
Parallels Desktop：Windows 虚拟机
CleanMyMac X：系统管理
[QQ](https://im.qq.com/download/)、[微信](https://mac.weixin.qq.com/?t=mac&lang=zh_CN)、[钉钉](https://tms.dingtalk.com/markets/dingtalk/download?spm=a3140.8196062.###31602.8.65f85c3d5uaOTy&source=1001&lwfrom=2017120202091367000000111)、[网易云音乐](https://music.163.com/##/download)、[谷歌浏览器|科学上网](https://www.google.cn/intl/zh-CN/chrome/)、[番茄土豆](https://mac.pomotodo.com/)、[百度网盘](https://pan.baidu.com/download##pan)、[迅雷](https://www.xunlei.com/)、[WPS](http://mac.wps.cn/)

Ps：科学上网下载速度慢可以复制下载链接到迅雷下载

### 应用商店

Xcode：mac 开发
Thor：一键直达
Alfred：应用启动
RunCat：菜单栏显示奔跑的小猫，CPU 占用率越高跑地越快

### 命令行软件

homebrew：包管理工具
git：版本管理
nvm：node 版本管理工具
node：前端开发

## Homebrew

### 常用命令

查看帮助信息：`brew help`。
查看版本：`brew -v`。
更新 Homebrew：`brew update`。
安装软件包：`brew install [包名]`。
查询可更新的包：`brew outdated`。
更新包：`rew upgarde //更新所有包`、`brew upgarde [包名] //更新指定包`。
清理旧版本：`brew cleanup //清理所有包的旧版本`、`brew cleanup [包名] //清理指定包的旧版本`、`brew cleanup -n //查看可清理的旧版本包，不执行实际操作`。
锁定不想更新的包：`brew pin $FORMULA //锁定某个包`、`brew unpin $FORMULA //取消锁定`。
卸载安装包：`brew uninstall [包名]`。
查看包信息：`brew info [包名]`。
查看安装列表：`brew list`。
查询可用包：`brew search [包名]`。
