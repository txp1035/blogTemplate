---
title: 'Tomcat安装'
category: 技术
tags: [服务器]
date: 2018-01-05
updated: 2018-01-05
---

# 下载 Tomcat

进入[Tomcat 官网](https://tomcat.apache.org)，下载对应你 jdk 版本的 Tomcat。

# 配置环境变量

在系统环境变量中配置名字为 JAVA_HOME 路径为你的 jdk 路径，名字为 CATALINA_HOME 路径为你的 Tomcat 路径。如下示例：

```
JAVA_HOME=C:\Program Files (x86)\Java\jdk1.7.0_71
CATALINA_HOME=C:\Program Files (x86)\Java\apache-tomcat-7.0.82
```

# 安装

解压 Tomcat 安装包即可

# 使用

将项目放置 webapps 目录里，在 bin 目录中运行 startup.bat 文件启动 Tomcat 服务器。运行 shutdown.bat 文件停止服务器。
