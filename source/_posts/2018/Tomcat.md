---
title:  "Tomcat安装"
category: 技术
tags: 服务器
date: 2018-01-05
---
### 下载Tomcat
进入[Tomcat官网](https://tomcat.apache.org)，下载对应你jdk版本的Tomcat。
### 配置环境变量
在系统环境变量中配置名字为JAVA_HOME路径为你的jdk路径，名字为CATALINA_HOME路径为你的Tomcat路径。如下示例：
```
JAVA_HOME=C:\Program Files (x86)\Java\jdk1.7.0_71
CATALINA_HOME=C:\Program Files (x86)\Java\apache-tomcat-7.0.82
```
### 安装
解压Tomcat安装包即可
### 使用
将项目放置webapps目录里，在bin目录中运行startup.bat文件启动Tomcat服务器。运行shutdown.bat文件停止服务器。
