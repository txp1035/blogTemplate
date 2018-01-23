---
title:  "jekyll搭建"
category: 技术
tags: 前端 博客搭建
date: 2017-09-12
---
第二次搭建jekyll了，结果还是出错了些，不过也比第一次快了很多，还是记录一下吧。 
1. 下载ruby(本次用的[rubyinstaller-2.4.1-2-x64](https://rubyinstaller.org/downloads/ "ruby下载链接"));
2. 安装ruby会有三个选项：
* Add Ruby executables to your PATH
* Associate .rb and .rbw files with this Ruby installation
* Use UTF-8 as default external encoding
<br>都选上钩，接着下一步完成安装，打开命令行窗口输入<code>ruby -v</code>若看到<code>ruby 2.4.1p111 (2017-03-22 revision 58053) [x64-mingw32]</code>则表示安装成功。
3. 打开命令行窗口，输入<code>gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/</code>把国外镜像换成国内镜像，这样做可以使安装软件速度加快。
4. 打开命令行窗口，输入<code>gem install bundler</code>安装依赖包bundler，然后输入<code>gem install jekyll</code>安装jekyll。
5. 打开命令行窗口，输入<code>jekyll new 123</code>创建一个jekyll默认博客名字叫123，如果有博客也需要创建一次，防止报错。
6. 进入123文件目录（你的jekyll博客），打开命令行窗口（shift+鼠标右键，点击‘在此处打开命令窗口’），输入<code>jekyll serve</code>，看到` Server address: http://127.0.0.1:4000/ Server running... press ctrl-c to stop.`然后就可以在服务器上浏览了,浏览地址：http://127.0.0.1:4000/。