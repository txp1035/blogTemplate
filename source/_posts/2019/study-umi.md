---
title: '学习UMI'
category: 技术
tags: [笔记, 前端]
date: 2019-1-24
updated: 2019-1-24
---

看看开源代码...

<!-- more -->

# 学习 UMI

## 目录

```js
const DirectoryTree = {
  docs: { dec: '说明文档', child: null },
  examples: { dec: '例子', child: null },
  packages: { dec: 'npm包', child: null },
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
  '.yarnrc': 'yarn配置文件',
  'jest.config.js': 'jest配置文件',
  'lerna.json': 'lerna配置文件|Lerna 是一个用来优化托管在git、npm上的多package代码库的工作流的一个管理工具。',
  'package.json': null,
  'rollup.config.js': 'rollup配置文件|rollup也是一款打包工具'
};
```
