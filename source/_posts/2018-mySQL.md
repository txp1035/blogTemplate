---
title: "MySQL安装"
category: 技术
tags: 数据库
date: 2018-01-02
updated: 2018-01-02
---

mysql 安装总结...

<!-- more -->

# 下载 MySQL

打开[MySQL 社区版官方下载](https://dev.mysql.com/downloads/mysql/)下载 Windows (x86, 32-bit/64-bit), ZIP Archive 安装包。32 位 64 位根据电脑选。我目前的版本是 5.7.20。

# 配置 MySQL

下载并复制到 mysql 里的 bin 目录下。
解压安装包，在安装包目录创建一个 data 空文件夹和创建一个 my.ini 文件，文件内容如下。

```
[mysql]

; 设置mysql客户端默认字符集

default-character-set=utf8

[mysqld]

;设置3306端口

port = 3306

; 设置mysql的安装目录(需要改动成你的目录)

basedir=C:\Users\Administrator\Desktop\java\mysql-5.7.20-winx64

; 设置mysql数据库的数据的存放目录(需要改动成你的目录)

datadir=C:\Users\Administrator\Desktop\java\mysql-5.7.20-winx64\data

; 允许最大连接数

max_connections=200

; 服务端使用的字符集默认为8比特编码的latin1字符集

character-set-server=utf8

; 创建新表时将使用的默认存储引擎

default-storage-engine=INNODB
```

1、安装 MySQL 服务  
打开命令行，进入 MySQL 的 bin 目录。  
2、安装 Windows 服务  
输入`mysqld install`，出现`The service already exists`则安装成功。  
3、初始化 data 目录  
输入`mysqld --initialize-insecure --user=mysql`，不报错则初始化成功。  
PS:使用-initialize 生成随机密码，使用-initialize-insecure 生成空密码。默认帐号 root,后面的-user=mysql 不更改  
4、启动 MySQL 服务  
输入`net start mysql`，出现`MySQL 服务启动成功`则启动服务成功。

# 配置环境变量

1、打开环境变量设置：  
在我的电脑上右键->点击属性->点击高级系统设置->点击环境变量  
复制你 mysql 文件路径，在系统变量里找到 Path 变量，点击编辑，光标移动到最前面，粘贴，加上;即可。

# 登录 MySQL

打开命令行。  
输入`mysql -uroot -p`，输入密码，出现`mysql>`则成功登录。

# 修改密码（忘记密码）

my.ini 配置文件[mysqld]条目下加一条命令 skip-grant-tables,然后重启 mysql 服务。  
1、进入 MySQL 数据库：  
打开命令行。  
输入`mysql -uroot -p`，出现`mysql>`则成功进入。  
2、准备修改密码：  
输入`mysql> use mysql;`，出现`Database changed`则准备成功。  
3、给 root 用户重置密码：  
输入`mysql> update user set authentication_string=password("新密码") where user="root";`，出现`Query OK,1 rows affected(0.01sec)Rows matched:1 Changed:1Warnings: 0`则修改成功。  
4、刷新数据库：  
输入`mysql> flush privileges;`，出现`QueryOK, 0 rows affected (0.00 sec)`则刷新成功。  
5、退出数据库：  
输入`mysql> quit`退出数据库。  
注释掉 my.ini 里的 skip-grant-tables。  
完成上面 5 步则成功修改密码。
