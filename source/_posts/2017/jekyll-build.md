---
title: 'jekyll'
category: 技术
tags: [博客, 框架]
date: 2017-09-12

---

jekyll 使用总结...

<!-- more -->

第二次搭建 jekyll 了，结果还是出错了些，不过也比第一次快了很多，还是记录一下吧。

# 安装

1、下载 ruby(本次用的[rubyinstaller-2.4.1-2-x64](https://rubyinstaller.org/downloads/ 'ruby下载链接'));
2、安装 ruby 会有三个选项：

- Add Ruby executables to your PATH
- Associate .rb and .rbw files with this Ruby installation
- Use UTF-8 as default external encoding

都选上钩，接着下一步完成安装，打开命令行窗口输入`ruby -v`若看到`ruby 2.4.1p111 (2017-03-22 revision 58053) [x64-mingw32]`则表示安装成功。

# 搭建

1、打开命令行窗口，输入`gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/`把国外镜像换成国内镜像，这样做可以使安装软件速度加快。
2、打开命令行窗口，输入`gem install bundler`安装依赖包 bundler，然后输入`gem install jekyll`安装 jekyll。
3、打开命令行窗口，输入`jekyll new 123`创建一个 jekyll 默认博客名字叫 123，如果有博客也需要创建一次，防止报错。
4、进入 123 文件目录（你的 jekyll 博客），打开命令行窗口（shift+鼠标右键，点击‘在此处打开命令窗口’），输入`jekyll serve`，看到`Server address: http://127.0.0.1:4000/ Server running... press ctrl-c to stop.`然后就可以在服务器上浏览了,浏览地址：http://127.0.0.1:4000/。
