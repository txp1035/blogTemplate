---
title: 'webpack总结'
category: 技术
tags: [前端]
date: 2018-08-01
updated: 2018-08-01
---

# 版本：4.16.3

使用 webpack 所需要的包：webpack、webpack-cli（此工具用于在命令行中运行 webpack），webpack4 之后将 webpack-cli 从 webpack 中分离的出来。

## webpack 基本配置

webpack.config.js

```js
const path = require('path'); //导入node.js的path模块
const HtmlWebpackPlugin = require('html-webpack-plugin'); //导入自动生成HTML插件
const CleanWebpackPlugin = require('clean-webpack-plugin'); //导入清理文件夹插件

const config = {
  /**
   *设置入口，用于设置打包的索引文件。
   *单入口用字符串，多入口用对象。
   */
  entry: {
    app: './src/index.js',
    print: './src/print.js'
  },
  /**
   *设置出口，用于设置打包的位置和文件名。
   *filename表示打包后的文件名。
   *[name]表示入口属性名。
   *path表示打包后存放的路径。
   *path.resolve表示获取绝对位置。
   *__dirname表示当前执行脚本所在的目录。
   */
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, './dist')
  },
  /**
   *设置loader，用于对模块的源代码进行转换。
   *用于在 import 或"加载"模块时预处理文件。
   *loader对象放在module对象下的rules数组中。
   *loader对象的test表示匹配什么文件。
   *loader对象的use表示引用什么loader
   */
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
  /**
   *设置插件，用于处理
   *添加插件需要先导入再实例化。
   */
  plugins: [
    new CleanWebpackPlugin(['dist']), //用于清理dist文件夹
    new HtmlWebpackPlugin({
      title: 'Output Management'
    }) //用于自动生成HTML
  ]
}; //定义配置文件

module.exports = config; //导出配置文件
```

运行配置：
npx webpack --config webpack.config.js
在 package.js 中 script 设置，"build":“webpack --config webpack.config.js”
PS：--config webpack.config.js 用于设置运行文件名，不设置默认运行 webpack.config.js

## source map

webpack.config.js

```js
const path = require('path');

module.exports = {
  entry: {
    app: './src/index.js',
    print: './src/print.js'
  },
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  /**
   *用于追踪错误和警告在源代码中的原始位置。
   *不设置：显示打包后的代码。（用于生产环境）
   *inline-source-map：显示原始源代码。
   */
  devtool: 'inline-source-map'
};
```

## 模块热替换

### webpack 设置方法

webpack.config.js

```js
const path = require('path');
const webpack = require('webpack');

module.exports = {
  entry: {
    app: './src/index.js'
  },
  /**
   *设置webpack-dev-server，用于提供服务器。
   *contentBase用于设置服务器目录。
   *hot表示是否启用webpack的模块热替换特性。
   */
  devServer: {
    contentBase: './dist',
    hot: true
  },
  plugins: [
    new webpack.NamedModulesPlugin(), //当开启HMR的时候使用该插件会显示模块的相对路径。
    new webpack.HotModuleReplacementPlugin() //模块热替换插件。
  ],
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

运行配置：
npx webpack-dev-server --open --config webpack.config.js
在 package.js 中 script 设置，"start":“webpack-dev-server --open --config webpack.config.js”
PS：--config webpack.config.js 用于设置运行文件名，不设置默认运行 webpack.config.js

### node 设置方法

dev-server.js

```js
const webpackDevServer = require('webpack-dev-server');
const webpack = require('webpack');

const config = require('./webpack.config.js');
const options = {
  contentBase: './dist',
  hot: true,
  host: 'localhost'
};

webpackDevServer.addDevServerEntrypoints(config, options);
const compiler = webpack(config);
const server = new webpackDevServer(compiler, options);

server.listen(5000, 'localhost', () => {
  console.log('dev server listening on port 5000');
});
```

运行配置：
node dev-server.js
在 package.js 中 script 设置，"start":“node dev-server.js”
