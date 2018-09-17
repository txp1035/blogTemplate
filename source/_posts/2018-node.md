---
title:  "Node.js"
category: 技术
tags: 前端
date: 2018-01-24
---
# 安装（Windows）
先到[官网](https://nodejs.org/en/)下载msi安装包,建议下载LTS（长期支持）版本。如图1：
![图1](../../img/2018/1-25-1.png)
双击安装包，如图2：
![图2](../../img/2018/1-25-2.png)
点击next，如图3：
![图3](../../img/2018/1-25-3.png)
勾选同意协议，点击next，如图4：
![图4](../../img/2018/1-25-4.png)
选择安装路径，点击next，如图5：
![图5](../../img/2018/1-25-5.png)
点击next，如图6：
![图6](../../img/2018/1-25-6.png)
点击install，如图7：
![图7](../../img/2018/1-25-7.png)
安装完成后，如图8：
![图8](../../img/2018/1-25-8.png)
为了验证是否安装成功，需要运行命令行来确认，使用Windows+R键打开运行界面，如图9：
![图9](../../img/2018/1-25-9.png)
输入cmd，点击确定，出现命令行窗口，输入`node -v`出现版本号表示node安装成功，`npm -v`出现版本号表示npm安装成功。
![图10](../../img/2018/1-25-10.png)
PS：由于npm的镜像源在国外，所以国内使用下载很慢，建议使用国内镜像安装快，操作步骤如下：
1、临时使用
打开命令行，输入`npm --registry https://registry.npm.taobao.org install package`，package为需要安装的包名。
2、持久使用
打开命令行，输入`npm config set registry https://registry.npm.taobao.org`，更换npm镜像地址。可以通过输入命令`npm config get registry`来验证是否配置成功。成功如图11：
![图11](../../img/2018/1-25-11.png)
3、通过cnpm使用
打开命令行，输入`npm install -g cnpm --registry=https://registry.npm.taobao.org`，安装完成后通过命令`cnpm install package`安装包，package为需要安装的包名。





