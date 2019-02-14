---
title: 'flutter折腾记'
category: 技术
tags: [笔记, 前端]
date: 2019-2-14
updated: 2019-2-14
---

期望 flutter 统一 JS 开发桌面客户端和 APP...

<!-- more -->

# 学习笔记

## 环境配置

### Windows

1. 安装 jdk
2. 安装 flutter
3. 安装 Android Studio
4. 安装 sdk
5. 创建一个 demo
6. 安装模拟器
7. 通过 vscode 开发 flutter

安装 jdk 很简单，通过[oracle 官网](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载。点击下一步即可安装完成（PS：最后 jre 可以取消安装，避免重复安装）。为了方便使用配置好环境变量。

安装 flutter 也简单，通过[flutter 官网](https://flutter.io/sdk-archive/#windows)下载。得到压缩包，在任意位置解压即可使用。在`flutter\bin`运行`flutter doctor`可以查看还需要安装哪儿些环境。为了方便使用将`flutter\bin`加入环境变量。从此命令可以得知我们还需要安装安卓 SDK 和安卓模拟器。

安装 Android Studio 也简单（在翻墙的情况下），在[安卓官网](https://developer.android.com/studio/)下载，得到软件一路下一步即可安装。安装完成后需要安装 sdk。如果你不会翻墙，那么在[安卓中文社区](http://www.android-studio.org/)也能下载 Android Studio，安装 sdk 前需要设置 host 文件，给 host 文件添加`203.208.41.37 dl.google.com`,ip 地址是通过[站长工具](http://ping.chinaz.com/dl.google.com)检测`dl.google.com`这个域名得到响应最快的国内 ip 地址，配置好 host 文件后再下载 sdk 速度就很快了。

安装完 sdk 后运行`flutter doctor`发现需要安装安卓证书，运行`flutter doctor --android-licenses`命令安装证书，提示选择 y。

接下来通过 Android Studio 来创建一个 demo，首先安装 Android Studio 的插件 flutter，安装 flutter 会自动安装 dart，安装完重启 Android Studio 会在启动界面看到多出了个选项`start a new flutter project`。
通过这个选项创建一个 flutter APP。

建好项目后，还需要项目运行环境，安卓模拟器，在 tools 里面选择 AVD manager，新加一个安卓模拟器，选择默认设备点击下一步，选择模拟器，模拟器旁边对应的安卓版本，还有 download 标识，标识没有下载，点击 download 下载模拟器（PS:如果不是 Intel 平台会比较麻烦），下载好后选择该模拟器，点击完成创建一个安卓模拟器。点击运行模拟器即可打开模拟器。

打开模拟器后就可以使用 debug 来浏览项目了。如果没有翻墙，需要修改项目文件`android->build.gradle`。将

```js
google();
jcenter();
```

替换为

```js
maven { url 'https://maven.aliyun.com/repository/google' }
maven { url 'https://maven.aliyun.com/repository/jcenter' }
maven { url 'http://maven.aliyun.com/nexus/content/groups/public'}
```

如此就能成功运行起程序。

作为 vscode 重度使用人来说换个编辑器还是有点不习惯的，那么怎么在 vscode 上开发 flutter 呢？首先我们需要解决脱离 Android Studio 能够运行起安卓模拟器。创建批处理文件

```js
C:\Users\ShawDanon\AppData\Local\Android\Sdk\emulator\emulator.exe -netdelay none -netspeed full -avd Nexus_5X_API_28
```

`C:\Users\ShawDanon\AppData\Local\Android\Sdk\emulator\emulator.exe`这个是安卓 sdk 路径下的可执行程序，需要改成你的路径。`Nexus_5X_API_28`是模拟器名字（名字本来是`Nexus 5X API 28`，空格使用下划线代替），在创建模拟器的时候可以设置。然后运行批处理文件即可打开安卓模拟器。

通过 vscode 打开刚才创建的项目，发现没有高亮代码。然后安装插件 flutter，安装完成重启 vscode 发现代码高亮了，就可以在 vscode 运行 flutter 了。在 vscode 中运行`flutter run`即可在刚才启动的模拟器中运行应用，但是在 vscode 中不能热更新了，需要每次修改代码之后在命令行输入 r 才能在模拟器中看到效果，如果需要热更新，要使用 debug 。
