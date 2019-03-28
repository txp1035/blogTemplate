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
  'jasmine.js': ' Jasmine配置文件|Jasmine是一个测试框架，配置了超时时间',
  'jest.config.js': 'jest配置文件',
  'lerna.json': 'lerna配置文件|Lerna 是一个用来优化托管在git、npm上的多package代码库的工作流的一个管理工具。',
  'package.json': null,
  'rollup.config.js': 'rollup配置文件|rollup是一款打包工具'
  'tsconfig.json': 'TypeScript配置文件'
};
```

整个目录看下来光工具和包很多都没接触过，代码检查有用过 eslint，项目落地还是不多，这个月看来要恶补一番前端开发规范啊。

## package.json

```json
{
  "private": true, //私有，防止npm意外发布
  "scripts": {
    "bootstrap": "lerna bootstrap",
    "build": "./scripts/build.js",
    "changelog": "lerna-changelog",
    "chore:update-deps": "./scripts/update_deps.sh",
    "test": "node scripts/test.js",
    "test:coverage": "./packages/umi-test/bin/umi-test.js --coverage",
    "debug": "./packages/umi-test/bin/umi-test.js",
    "coveralls": "cat ./coverage/lcov.info | coveralls",
    "lint": "eslint --ext .js packages",
    "precommit": "lint-staged",
    "doc:dev": "./website/node_modules/.bin/vuepress dev ./docs",
    "doc:deploy": "rm -rf ./website/yarn.lock && cd ./website && npm run deploy && cd -",
    "publish": "./scripts/publish.js",
    "ui:dev": "APP_ROOT=packages/umi-build-dev/src/plugins/commands/ui ./packages/umi/bin/umi.js dev",
    "ui:build": "APP_ROOT=packages/umi-build-dev/src/plugins/commands/ui ./packages/umi/bin/umi.js build"
  }, //脚本
  "lint-staged": {
    "*.(t|j)s": ["prettier --trailing-comma all --single-quote --write", "git add"]
  },
  "devDependencies": {
    "@types/jest": "^24.0.5", //Jest的TypeScript定义
    "babel-eslint": "10.0.1", //eslint的解析器，一个对Babel解析器的包装，使其能够与 ESLint 兼容。
    "chokidar": "2.0.4", //监听文件变化
    "coveralls": "3.0.2", //代码覆盖率
    "dva": "2.4.1", //数据流管理
    "eslint": "5.10.0", //可组装的JavaScript和JSX检查工具
    "eslint-config-airbnb": "17.1.0", //airbnb的eslint规范
    "eslint-plugin-import": "2.14.0", //导入导出文件检查
    "eslint-plugin-jsx-a11y": "6.1.2", //用于JSX元素的可访问性规则的静态AST检查器
    "eslint-plugin-react": "7.11.1", //react检查器扩展插件
    "form-data": "^2.3.3", //用于创建可读"multipart/form-data"流的库。可用于将表单和文件上载提交到其他Web应用程序。
    "got": "9.3.2", //简化的HTTP请求
    "husky": "1.2.0", //git commit、git push前检查代码
    "lerna": "3.6.0", //包管理工具
    "lerna-changelog": "0.8.2", //为 Lerna repo  生成变更日志
    "lint-staged": "8.1.0", //提交前运行阻止提交不合规范代码
    "mkdirp": "^0.5.1", //递归创建目录及其子目录,代替mkdir -p
    "prettier": "1.15.3", //格式化
    "puppeteer": "1.11.0", //Puppeteer是一个Node库，它提供了一个高级API来控制DevTools协议上的 Chrome或Chromium 。
    "react-router-dom": "4.3.1", //react路由
    "react-test-renderer": "16.6.3", //单元测试
    "serve-handler": "5.0.8", //此包代表正在运行的服务和静态部署的核心。
    "serve-static": "^1.13.2", //这是一个通过npm注册表提供的Node.js模块。
    "shelljs": "0.8.3", //ShellJS是Node.js API之上的Unix shell命令的可移植（Windows / Linux / OS X）实现。
    "test-build-result": "^1.1.2", //测试构建结果
    "umi-tools": "^0.4.0" //用于构建umi的工具。
  }
}
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

1. `lerna init`：创建新的 lerna repo 或将现有 repo 升级到当前版本的 Lerna。
2. `lerna bootstrap`：将把 repo 中的依赖关系链接在一起。
3. `lerna publish`：将帮助发布任何更新的包。

基本使用会了，让我们回到 umi 中看看`lerna.json`都配置了些什么。

```json
{
  "changelog": {
    "labels": {
      "pr: enhancement": ":rocket: Enhancement", //增强
      "pr: bug": ":bug: Bug Fix", //错误修复
      "pr: documentation": ":book: Documentation", //文档
      "pr: dependency": ":deciduous_tree: Dependency"
    }, //GitHub PR标签映射到changelog部分标头
    "repo": "umijs/umi", //你在GitHub上的“组织/回购”（从package.json文件中自动推断）
    "cacheDir": ".changelog" //GitHub API响应缓存的路径以避免限制（例如.changelog）
  },
  "packages": ["packages/*"], //包位置
  "command": {
    "version": {
      "exact": true
    }
  },
  "npmClient": "yarn", //一个选项，用于指定运行命令的特定客户端（也可以基于每个命令指定）。更改为"yarn"使用yarn运行所有命令。默认为“npm”
  "version": "independent" //存储库的当前版本，使用独立模式
}
```

## Travis

Travis 是一款持续集成工具。那么持续集成是什么呢？

> 持续集成是一种软件开发实践，即团队开发成员经常集成它们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误。

如何使用 Travis？

1. 在 Travis 官网使用 github 账号注册登录，会看到你仓库所有的项目。
2. 打开你想持续集成的项目开关。
3. 在该项目创建`.travis.yml`文件，文件内容至少包含`language: node_js`和`node_js: - '6'`
4. 提交代码，Travis 就会自动进行构建了。
5. 构建成功会在 Travis 中显示 build pass 的按钮，点击按钮会有个弹窗，选择 markdown 格式复制链接到项目 readme 中就拥有构建徽章了。

大概了解了下 Travis，接下来看看 umi 中`.travis.yml`文件写了些什么。

```yml
# 指定语言
language: node_js
# 指定版本
node_js:
  - '8'
  - '10'
# 脚本阶段之前
before_script:
  - npm run build
  - npm run bootstrap
# 构建成功
after_success:
  - npm run coveralls
# 缓存Node.js模块
cache:
  directories:
    - node_modules

git:
  depth: 5
```

## rollup

## EditorConfig

```ini
# http://editorconfig.org
#应在任何部分之外的文件顶部指定的特殊属性。设置为true以停止.editorconfig在当前文件上搜索文件。
root = true

#所有文件配置
[*]
#设置缩进风格为空格
indent_style = space
#缩进大小（单行间距）
indent_size = 2
#行结束文件格式（Unix，DOS，Mac）换行符
end_of_line = lf
#文件字符编码
charset = utf-8
#设置为true以删除换行符前面的任何空白字符，并设置为false以确保不会。
trim_trailing_whitespace = true
#设置为真以换行符节能时，确保文件最终假，以确保它不会。
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false

[Makefile]
indent_style = tab
```

## eslintrc

```json
{
  "parser": "babel-eslint", //指定解析器
  "extends": "airbnb", //使用airbnb配置扩展
  "env": {
    "browser": true,
    "jest": true
  }, //指定配置文件中的环境
  "rules": {
    "jsx-a11y/href-no-hash": [0],
    "jsx-a11y/click-events-have-key-events": [0],
    "jsx-a11y/anchor-is-valid": [
      "error",
      {
        "components": ["Link"],
        "specialLink": ["to"]
      }
    ],
    "generator-star-spacing": [0],
    "consistent-return": [0],
    "react/react-in-jsx-scope": [0],
    "react/forbid-prop-types": [0],
    "react/jsx-filename-extension": [1, { "extensions": [".js"] }],
    "global-require": [1],
    "import/prefer-default-export": [0],
    "react/jsx-no-bind": [0],
    "react/prop-types": [0],
    "react/prefer-stateless-function": [0],
    "no-else-return": [0],
    "no-restricted-syntax": [0],
    "import/no-extraneous-dependencies": [0],
    "no-use-before-define": [0],
    "jsx-a11y/no-static-element-interactions": [0],
    "no-nested-ternary": [0],
    "arrow-body-style": [0],
    "import/extensions": [0],
    "no-bitwise": [0],
    "no-cond-assign": [0],
    "import/no-unresolved": [0],
    "require-yield": [1],
    "no-param-reassign": [0],
    "no-shadow": [0],
    "no-underscore-dangle": [0],
    "spaced-comment": [0],
    "indent": [0],
    "quotes": [0],
    "func-names": [0],
    "arrow-parens": [0],
    "space-before-function-paren": [0],
    "no-useless-escape": [0],
    "object-curly-newline": [0],
    "function-paren-newline": [0],
    "class-methods-use-this": [0],
    "no-new": [0],
    "import/newline-after-import": [0],
    "no-console": [0]
  }, //规则覆盖
  "parserOptions": {
    "ecmaFeatures": {
      "experimentalObjectRestSpread": true
    } //启用对实验对象休息/传播属性的支持,弃用
  } //指定解析器选项
}
```

## jest

```js
module.exports = {
  testPathIgnorePatterns: [
    '/node_modules/',
    '/examples/',
    '/lib/',
    '/packages/umi/src/scripts/test.js',
    '/packages/umi/src/test.js',
    '/packages/umi-build-dev/src/fixtures',
    '/packages/umi-build-dev/src/routes/fixtures',
    '/packages/umi-plugin-dva/src/fixtures',
    '/packages/umi-utils/src/fixtures',
    '/packages/umi-library/src/fixtures',
    '/packages/umi/test/fixtures'
  ], //排除测试的文件
  setupFilesAfterEnv: ['./jasmine.js'], //在每次测试之前运行一些代码以配置或设置测试框架的模块的路径列表。
  collectCoverageFrom: ['packages/**/src/**/*.{js,jsx}'], //应收集覆盖率信息的一组文件。
  coveragePathIgnorePatterns: [
    '/packages/umi-plugin-dva/src/fixtures',
    '/packages/umi-build-dev/src/fixtures',
    '/packages/umi-build-dev/src/routes/fixtures',
    '/packages/umi-build-dev/src/plugins/commands/generate/generators',
    '/packages/umi-library/src/fixtures',
    '/packages/umi-utils/src/fixtures',
    '/packages/umi/test/fixtures'
  ] //覆盖率排除的文件。
};
```

## a

```js
{
  "compilerOptions": {
    "target": "esnext",//指定ECMAScript的目标版本,"ESNext"目标是最新支持的ES提议功能。
    "moduleResolution": "node",//确定如何解决模块。
    "jsx": "preserve",//在.tsx文件中支持JSX
    "esModuleInterop": true//发布__importStar和生成器__importDefault兼容性，用于运行时babel生态系统兼容性，并支持--allowSyntheticDefaultImports类型系统兼容性。
  }
}

```

## 参考

[创建并发布一个小而美的 npm 包，没你想的那么难！](https://juejin.im/post/5c26c1b65188252dcb312ad6#heading-0)
[lerna 管理前端 packages 的最佳实践](https://juejin.im/post/5a989fb451882555731b88c2)
[lerna 文档](https://github.com/lerna/lerna/#getting-started)
[lerna-changelog 文档](https://github.com/lerna/lerna-changelog)
[前端开源项目持续集成三剑客](https://efe.baidu.com/blog/front-end-continuous-integration-tools/)
[editorconfig](https://editorconfig.org/)
[eslint](https://eslint.org/docs/user-guide/getting-started)
