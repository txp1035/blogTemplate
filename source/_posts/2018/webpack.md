---
title:  "webpack总结"
category: 技术
tags: 前端
date: 2018-08-01
updated: 2018-08-01
---
# 版本：4.16.3
使用webpack所需要的包：webpack、webpack-cli（此工具用于在命令行中运行 webpack），webpack4之后将webpack-cli从webpack中分离的出来。  
配置文件：
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const CleanWebpackPlugin = require('clean-webpack-plugin');

const config = {
  entry: {
    app: './src/index.js',
    print: './src/print.js'
  },//设置入口
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  },//设置出口，name代表入口属性值
  devtool: 'inline-source-map',//使用source map，用于跟踪错误位置。（适用于开发，不适用于生产）
  devServer: {
    contentBase: './dist'
  },//设置热更新,需要安装webpack-dev-server（适用于开发，不适用于生产）
  plugins: [
    new CleanWebpackPlugin(['dist']),//用于每次运行webpack清理dist目录
    new HtmlWebpackPlugin({
      title: 'Output Management'
    })//用于自动生成HTML的插件
  ]//设置插件，添加插件需要先导入再new
};

module.exports = config;
```
