---
title: '学习UMI'
category: 技术
tags: [笔记, 前端]
date: 2019-1-24
updated: 2019-1-24
---

第一次认真学习开源项目，看一次开源代码...

<!-- more -->

# 学习 UMI

## 目录

```js
const DirectoryTree = {
  docs: { dec: '说明文档', child: null },
  examples: { dec: '例子', child: null },
  packages: {
    dec: 'npm包',
    child: {
      'af-webpack': null
      'babel-preset-umi': null
      'eslint-config-umi': null
      'umi': null
      'umi-build-dev': null
      'umi-core': null
      'umi-library': null
      'umi-mock': null
      'umi-plugin-dll': null
      'umi-plugin-dva': null
      'umi-plugin-hd': null
      'umi-plugin-locale': null
      'umi-plugin-polyfills': null
      'umi-plugin-react': null
      'umi-plugin-routes': null
      'umi-serve': null
      'umi-test': null
      'umi-types': null
      'umi-utils': null
    }
  },
  scripts: {
    dec: '脚本',
    child: {
      'build.js': '打包脚本',
      'publish.js': '发布脚本',
      'startDevServers.js': '启动开发服务脚本',
      'test.js': '测试脚本'
    }
  },
  website: null,
  '.editorconfig': 'EditorConfig配置文件|EditorConfig有助于为跨越各种编辑器和IDE的同一项目的多个开发人员维护一致的编码样式',
  '.eslintignore': '设置ESlint不跟踪的文件，同.gitignore一样',
  '.eslintrc': 'ESlint配置文件|JavaScript代码检测, JavaScript代码风格检测, JavaScript代码自动格式化',
  '.gitignore': '设置git不跟踪的文件',
  '.prettierignore': '设置Prettier不跟踪的文件，同.gitignore一样|Prettier是一个前端代码格式化工具',
  '.travis.yml': 'Travis配置文件|Travis CI 提供的是持续集成服务',
  '.yarnrc': 'yarn配置文件，配置了使用官方镜像源',
  'jest.config.js': 'jest配置文件',
  'lerna.json': 'lerna配置文件|Lerna 是一个用来优化托管在git、npm上的多package代码库的工作流的一个管理工具。',
  'package.json': null,
  'rollup.config.js': 'rollup配置文件|rollup是一款打包工具'
};
```

## Lerna

从目录架构来看，首先要学的是多包管理与发布。通过多包管理可以把作者多个包放在一起用一个仓库储存来维护。（PS：npm 包上传后不能删除，强迫症患者需要慎重取名）

使用说明：

1. 全局安装 lerna 包`npm install lerna -g`。
2. 在 github 创建一个仓库，并拉下来备用。
3. 在该仓库根目录初始化 lerna`lerna init`。
   初始化成功会多出 3 个文件： packages(目录，用于存放包)、 lerna.json(配置文件，用于 lerna 配置)、package.json(工程描述文件)
4. 修改 lerna.json 文件中的 version 值，默认是`"version": "0.0.0"`（使用这个模式，在发布包的时候所有的包都会发布，并使用 lerna.json 中设置的版本号），修改为`"version": "independent"`（使用这个模式，可以单独发布包更新，可喜的是发布包可以自动生成版本号供你选择）。
5. 在 packages 目录中创建自己的包，在当前包目录执行`lerna publish`来发布包。（发布包需要确定 npm 镜像源是`https://registry.npmjs.org/`，发布包前需要登录 npm，使用`npm login`登录。）

常用命令：

1. `lerna init`：初始化一个包管理项目。
2. `lerna bootstrap`：安装依赖。
3. `lerna publish`：发布包。

## Travis

Travis 是一款持续集成工具。那么持续集成是什么呢？

> 持续集成是一种软件开发实践，即团队开发成员经常集成它们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误。

如何使用 Travis？

1. 在 Travis 官网使用 github 账号注册登录，会看到你仓库所有的项目。
2. 打开你想持续集成的项目开关。
3. 在该项目创建`.travis.yml`文件，文件内容至少包含

```yml
vlanguage: node_js
node_js:
  - '6'
```

4. 提交代码，Travis 就会自动进行构建了。

## 参考

[创建并发布一个小而美的 npm 包，没你想的那么难！](https://juejin.im/post/5c26c1b65188252dcb312ad6#heading-0)
[lerna 管理前端 packages 的最佳实践](https://juejin.im/post/5a989fb451882555731b88c2)
[前端开源项目持续集成三剑客](https://efe.baidu.com/blog/front-end-continuous-integration-tools/)
