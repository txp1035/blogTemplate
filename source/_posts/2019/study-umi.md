---
title: '学习UMI'
category: 技术
tags: [笔记, 前端]
date: 2019-3-2
---

第一次认真学习开源项目，看一次开源代码...

<!-- more -->

## 学习 UMI（一）

umi@2.6.17

### 目录

```js
const DirectoryTree = {
  '.github': { dec: undefined, child: null },
  docs: { dec: '说明文档', child: null },
  examples: { dec: '例子', child: null },
  packages: {
    dec: 'npm包',
    child: {
      'af-webpack': null,
      'babel-preset-umi': null,
      'eslint-config-umi': null,
      umi: null,
      'umi-build-dev': null,
      'umi-core': null,
      'umi-library': null,
      'umi-mock': null,
      'umi-plugin-dll': null,
      'umi-plugin-dva': null,
      'umi-plugin-hd': null,
      'umi-plugin-locale': null,
      'umi-plugin-polyfills': null,
      'umi-plugin-react': null,
      'umi-plugin-routes': null,
      'umi-serve': null,
      'umi-test': null,
      'umi-types': null,
      'umi-utils': null
    }
  },
  scripts: {
    dec: '脚本',
    child: {
      'build.js': '构建脚本',
      'publish.js': '发布脚本',
      'reinstall_deps.sh': undefined,
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
  '（废弃集成到了umi-tools中）rollup.config.js': 'rollup配置文件|rollup是一款打包工具',
  'tsconfig.json': 'TypeScript配置文件|指定ts编译的一些参数信息'
};
```

整个目录看下来光工具和包很多都没接触过，代码检查有用过 eslint，项目落地还是不多，这个月看来要恶补一番前端开发规范啊。

### 一级目录

#### package.json

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

#### Lerna

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

#### Travis

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

#### Jest

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

#### EditorConfig

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

#### ESLint

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

#### Typescript

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

### scripts 文件夹

#### build.js

```js
/*
child_process 模块提供了以与 popen(3) 类似但不相同的方式衍生子进程的功能。
child_process.fork():衍生一个新的 Node.js 进程，并通过建立 IPC 通信通道来调用指定的模块，该通道允许在父进程与子进程之间发送消息。
*/
const { fork } = require('child_process');
/*
path 模块提供用于处理文件路径和目录路径的实用工具。
*/
const { join } = require('path');

function runUmiTools(...args) {
  console.log(['>> umi-tools', ...args].join(' '));
  /*
  child_process.fork(modulePath[, args][, options])
  modulePath <string> 要在子进程中运行的模块。
  args <string[]> 字符串参数的列表。
  options <Object>
    stdio <Array> | <string> 参阅 child_process.spawn() 的 stdio。当提供此选项时，则它覆盖 silent 选项。如果使用了数组变量，则它必须包含一个值为 'ipc' 的元素，否则会抛出错误。例如 [0, 1, 2, 'ipc']。
    cwd <string> 子进程的当前工作目录。
  返回: <ChildProcess>
  */
  /*
  path.join([...paths])
  ...paths <string> 路径片段的序列。
  返回: <string>
  path.join() 方法使用平台特定的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。
  零长度的 path 片段会被忽略。 如果连接的路径字符串是零长度的字符串，则返回 '.'，表示当前工作目录。
  */
  /*
   process.cwd() 方法返回 Node.js 进程的当前工作目录。
  */
  return fork(join(process.cwd(), 'node_modules/.bin/umi-tools'), [...args].concat(process.argv.slice(2)), {
    stdio: 'inherit',
    cwd: process.cwd()
  });
}

const cp = runUmiTools('build');
/*
'error' 事件
err <Error> 错误对象。
当出现以下情况时触发 'error' 事件：
1.无法衍生进程；
2.无法杀死进程；
3.向子进程发送信息失败。
发生错误后，'exit' 事件可能会也可能不会触发。如果同时监听了 'exit' 和 'error' 事件，可能会多次调用处理函数。
*/
cp.on('error', err => {
  console.log(err);
});
/*
'message' 事件
  message <Object> JSON 对象或原始值。
  sendHandle <Handle> net.Socket 或 net.Server 对象，或 undefined。
当子进程使用 process.send() 发送消息时触发。
消息通过序列化和解析传递，收到的消息可能跟发送的不完全一样。
*/
cp.on('message', message => {
  if (message === 'BUILD_COMPLETE') {
    runUmiTools('rollup', '-g', 'dva:dva,antd:antd');
  } //构建完成打包
});
```

#### publish.js

```js
/*
ShellJS是 Node.js API之上的Unix shell 命令的可移植（Windows / Linux / OS X）实现。您可以使用它来消除shell脚本对Unix的依赖性，同时仍保留其熟悉且功能强大的命令。您也可以在全局安装它，这样您就可以从Node项目外部运行它- 告别那些粗糙的Bash脚本！
*/
const shell = require('shelljs');
const { join } = require('path');
const { fork } = require('child_process');
/*
shell.exec(command [, options] [, callback])
执行命令
options：
  async：异步执行。如果提供了回调，则true无论传递的值如何（默认值:)，都将设置为回调  false。
  silent：不要将程序输出回显到控制台（默认值:) false。
  encoding：要使用的字符编码。影响返回到stdout和stderr的值，以及未处于静默模式时写入stdout和stderr的值（默认值:) 'utf8'。
以及Node.js可用的任何选项 child_process.exec()
除非另有说明，否则command同步执行给定的给定。
在同步模式下，这将返回ShellString。否则，这将返回子进程对象，并callback接收参数(code, stdout, stderr)。
*/
if (!shell.exec('npm config get registry').stdout.includes('https://registry.npmjs.org/')) {
  console.error('Failed: set npm registry to https://registry.npmjs.org/ first');
  process.exit(1); //退出进程
} //判断当前npm镜像源是否为npm官方源，不是则失败提示请设置镜像源

const cwd = process.cwd();
const ret = shell.exec('./node_modules/.bin/lerna updated').stdout; //运行lerna updated时的输出
const updatedRepos = ret
  .split('\n')
  .map(line => line.replace('- ', ''))
  .filter(line => line !== ''); //筛选出需要更新的仓库

if (updatedRepos.length === 0) {
  console.log('No package is updated.');
  process.exit(0);
} //没有需要更新仓库的情况

const { code: buildCode } = shell.exec('npm run build'); //执行构建
if (buildCode === 1) {
  console.error('Failed: npm run build');
  process.exit(1);
} //构建失败情况

const { code: uiBuildCode } = shell.exec('npm run ui:build'); //执行ui构建
if (uiBuildCode === 1) {
  console.error('Failed: npm run ui:build');
  process.exit(1);
} //ui构建失败情况

const cp = fork(join(process.cwd(), 'node_modules/.bin/lerna'), ['version'].concat(process.argv.slice(2)), {
  stdio: 'inherit',
  cwd: process.cwd()
});
cp.on('error', err => {
  console.log(err);
});
/*
code <number> 子进程的退出码。
signal <string> 终止子进程的信号。
当子进程的 stdio 流被关闭时触发。 与 'exit' 事件的区别是，多个进程可能共享同一 stdio 流。
*/
cp.on('close', code => {
  console.log('code', code);
  if (code === 1) {
    console.error('Failed: lerna publish');
    process.exit(1);
  }

  publishToNpm();
});

function publishToNpm() {
  console.log(`repos to publish: ${updatedRepos.join(', ')}`);
  updatedRepos.forEach(repo => {
    shell.cd(join(cwd, 'packages', repo));
    const { version } = require(join(cwd, 'packages', repo, 'package.json'));
    if (version.includes('-rc.') || version.includes('-beta.') || version.includes('-alpha.')) {
      console.log(`[${repo}] npm publish --tag next`);
      shell.exec(`npm publish --tag next`);
    } else {
      console.log(`[${repo}] npm publish`);
      shell.exec(`npm publish`);
    } //版本包含-rc.-beta.-alpha.字眼更新标签，否则直接发布
  });
}
```

#### startDevServers.js

```js
const { fork } = require('child_process');
const { join, dirname } = require('path');

const DEV_SCRIPT = join(__dirname, '../packages/umi/bin/umi.js');

function startDevServer(opts = {}) {
  const { port, cwd } = opts;
  return new Promise(resolve => {
    const child = fork(DEV_SCRIPT, ['dev', '--port', port, '--cwd', cwd], {
      env: {
        ...process.env,
        CLEAR_CONSOLE: 'none',
        BROWSER: 'none',
        UMI_DIR: dirname(require.resolve('../packages/umi/package'))
      }
    });
    child.on('message', args => {
      if (args.type === 'DONE') {
        resolve(child);
      }
    });
  });
}

function start() {
  const devServers = [
    [12341, '../packages/umi/test/fixtures/e2e/normal'],
    [12342, '../packages/umi/test/fixtures/e2e/hashHistory'],
    [12351, '../packages/umi-plugin-react/test/normal'],
    [12352, '../packages/umi-plugin-react/test/with-dva'],
    [12353, '../packages/umi-plugin-react/test/pwa']
  ];

  return Promise.all(
    devServers.map(([port, cwd]) => {
      return startDevServer({ port, cwd: join(__dirname, cwd) });
    })
  );
}

module.exports = start;

if (require.main === module) {
  start()
    .then(() => {
      console.log('All dev servers are started.');
    })
    .catch(e => {
      console.log(e);
    });
}
```

#### test.js

```js
/*
child_process.spawn() 方法异步地衍生子进程，且不阻塞 Node.js 事件循环。 child_process.spawnSync() 方法则以同步的方式提供等效功能，但会阻止事件循环直到衍生的进程退出或终止。
*/
const { spawn } = require('child_process');
const startDevServers = require('./startDevServers');

startDevServers()
  .then(devServers => {
    const testCmd = spawn(/^win/.test(process.platform) ? 'npm.cmd' : 'npm', ['run', 'test:coverage'], {
      stdio: 'inherit'
    });
    testCmd.on('exit', code => {
      devServers.forEach(devServer => devServer && devServer.kill('SIGINT'));
      process.exit(code);
    });
  })
  .catch(e => {
    console.log(e);
  });
```

### 总结

#### 2019/3/31

通过了解 umi 的源码知道了很多有意思的东西：npm 包发布、通过 lerna 来管理包、使用 Travis 持续集成项目、EditorConfig 来保证不同编辑器风格一致、ESLint 保证代码风格一致、Jest 测试保证代码可靠性、lint-staged 和 husky 阻止代码提交（最开始在 ant design pro 有遇到），shelljs 执行脚本命令。

### demo 地址

[准备用来存些常用库的仓库](https://github.com/ShawDanon/txp)

### 参考一

[创建并发布一个小而美的 npm 包，没你想的那么难！](https://juejin.im/post/5c26c1b65188252dcb312ad6#heading-0)
[lerna 管理前端 packages 的最佳实践](https://juejin.im/post/5a989fb451882555731b88c2)
[lerna 文档](https://github.com/lerna/lerna/#getting-started)
[lerna-changelog 文档](https://github.com/lerna/lerna-changelog)
[前端开源项目持续集成三剑客](https://efe.baidu.com/blog/front-end-continuous-integration-tools/)
[editorconfig](https://editorconfig.org/)
[eslint](https://eslint.org/docs/user-guide/getting-started)
[Node.js 中文网](http://nodejs.cn/api/)
[shelljs](http://documentup.com/shelljs/shelljs)

## 学习 UMI（二）

umi@2.6.17
正式开始看源码了

### packages/umi

#### 重要的

##### packages/umi/package.json

先来看看 package.json 文件。

```json
{
  "name": "umi",
  "version": "2.6.16",
  "description": "Pluggable enterprise-level react application framework.",
  "dependencies": {
    "@babel/core": "7.2.2", //babel核心包
    "@babel/runtime": "7.3.0", //一个包含Babel模块化运行时助手和一个版本的库
    "@types/react": "16.x", //react
    "@types/react-router-dom": "4.x", //react路由
    "babel-preset-umi": "1.4.1", //云谦的babel预设
    "debug": "4.1.0", //一个微小的JavaScript调试工具，以Node.js核心的调试技术为模型。适用于Node.js和Web浏览器。
    "dotenv": "6.2.0", //Dotenv是一个零依赖模块，可以将.env文件中的环境变量加载到process.env。在与代码分开的环境中存储配置基于The Twelve-Factor App方法。
    "is-windows": "1.0.2", //如果平台是windows，则返回true。UMD模块，适用于node.js，commonjs，浏览器，AMD，电子等。
    "lodash": "4.17.11", //一个现代JavaScript实用程序库，提供模块化，性能和附加功能。深拷贝用过
    "react-loadable": "5.5.0", //用于加载具有动态导入的组件的更高阶组件。
    "resolve-cwd": "2.0.0", //解析模块的路径，require.resolve()但是从当前工作目录中解析
    "semver": "5.6.0", //节点的semver解析器，语义化版本
    "signale": "1.3.0", //可记录和可配置到核心，signale可用于记录目的，状态报告，以及处理其他节点模块和应用程序的输出呈现过程。
    "umi-build-dev": "1.8.3", //未有readme文件具体功能暂时不知
    "umi-utils": "1.4.1", //工具类
    "update-notifier": "2.5.0", //更新CLI应用程序的通知
    "yargs-parser": "13.0.0" //Yargs通过解析参数和生成优雅的用户界面来帮助您构建交互式命令行工具。
  }, //依赖包
  "module": "index.js",
  "sideEffects": ["./lib/renderRoutes.js"],
  "bin": {
    "umi": "./bin/umi.js"
  }, //很多软件包都有一个或多个可以安装到PATH中的可执行文件。
  "license": "MIT",
  "repository": {
    "type": "git",
    "url": "https://github.com/umijs/umi/tree/master/packages/umi"
  },
  "homepage": "https://github.com/umijs/umi/tree/master/packages/umi",
  "authors": ["chencheng <sorrycc@gmail.com> (https://github.com/sorrycc)"],
  "bugs": {
    "url": "https://github.com/umijs/umi/issues"
  },
  "files": [
    "lib",
    "src",
    "bin",
    "index.js",
    "index.d.ts",
    "babel.js",
    "dynamic.d.ts",
    "link.d.ts",
    "navlink.d.ts",
    "prompt.d.ts",
    "redirect.d.ts",
    "router.d.ts",
    "withRouter.d.ts",
    "routerTypes.d.ts"
  ], //可选files字段是一个文件模式数组，描述了将软件包作为依赖项安装时要包含的条目。
  "umiTools": {
    "browserFiles": [
      "src/createHistory.js",
      "src/dynamic.js",
      "src/link.js",
      "src/navlink.js",
      "src/prompt.js",
      "src/redirect.js",
      "src/renderRoutes.js",
      "src/Route.js",
      "src/router.js",
      "src/runtimePlugin.js",
      "src/utils.js",
      "src/withRouter.js"
    ]
  }
}
```

#### 提供接口相关的文件

##### packages/umi/index.js

```js
export { default as Link } from './lib/link';
export { default as NavLink } from './lib/navlink';
export { default as Redirect } from './lib/redirect';
export { default as dynamic } from './lib/dynamic';
export { default as router } from './lib/router';
export { default as withRouter } from './lib/withRouter';
export { default as Route } from './lib/Route';
```

umi 输出的 api 对应[官方文档](https://umijs.org/zh/api/)。

##### packages/umi/link.js

link 组件直接使用 react-router 的 link 组件

```js
import { Link } from 'react-router-dom';
export default Link;
```

##### packages/umi/NavLink.js

NavLink 组件直接使用 react-router 的 NavLink 组件

```js
import { NavLink } from 'react-router-dom';
export default NavLink;
```

##### packages/umi/Redirect.js

Redirect 组件直接使用 react-router 的 Redirect 组件

```js
import { Redirect } from 'react-router-dom';
export default Redirect;
```

##### packages/umi/router.js

js 路由操作文件

```js
/* global window */

export function push(...args) {
  window.g_history.push(...args);
}

export function replace(...args) {
  window.g_history.replace(...args);
}

export function go(...args) {
  window.g_history.go(...args);
}

export function goBack(...args) {
  window.g_history.goBack(...args);
}

export function goForward(...args) {
  window.g_history.goForward(...args);
}

export default {
  push,
  replace,
  go,
  goBack,
  goForward
};
```

##### packages/umi/withRouter.js

withRouter 组件直接使用 react-router 的 withRouter 组件

```js
import { withRouter } from 'react-router-dom';
export default withRouter;
```

##### packages/umi/Route.js

Route 组件直接使用 react-router 的 Route 组件

```js
import { Route } from 'react-router-dom';
export default Route;
```

##### packages/umi/dynamic.js

```js
import React from 'react';
import Loadable from 'react-loadable';

// Thanks to next.js
// ref: https://github.com/zeit/next.js/blob/canary/lib/dynamic.js
export default function(dynamicOptions, options) {
  let loadableFn = Loadable;
  let loadableOptions = {
    loading: ({ error, isLoading }) => {
      if (process.env.NODE_ENV === 'development') {
        if (isLoading) {
          return <p>loading...</p>;
        }
        if (error) {
          return (
            <p>
              {error.message}
              <br />
              {error.stack}
            </p>
          );
        }
      }
      return <p>loading...</p>;
    }
  };

  // Support for direct import(),
  // eg: dynamic(import('../hello-world'))
  if (typeof dynamicOptions.then === 'function') {
    loadableOptions.loader = () => dynamicOptions;
    // Support for having first argument being options,
    // eg: dynamic({loader: import('../hello-world')})
  } else if (typeof dynamicOptions === 'object') {
    loadableOptions = { ...loadableOptions, ...dynamicOptions };
  }

  // Support for passing options,
  // eg: dynamic(import('../hello-world'), {loading: () => <p>Loading something</p>})
  loadableOptions = { ...loadableOptions, ...options };

  // Support for `render` when using a mapping,
  // eg: `dynamic({ modules: () => {return {HelloWorld: import('../hello-world')}, render(props, loaded) {} } })
  if (dynamicOptions.render) {
    loadableOptions.render = (loaded, props) => dynamicOptions.render(props, loaded);
  }

  // Support for `modules` when using a mapping,
  // eg: `dynamic({ modules: () => {return {HelloWorld: import('../hello-world')}, render(props, loaded) {} } })
  if (dynamicOptions.modules) {
    loadableFn = Loadable.Map;
    const loadModules = {};
    const modules = dynamicOptions.modules();
    Object.keys(modules).forEach(key => {
      const value = modules[key];
      if (typeof value.then === 'function') {
        loadModules[key] = () => value.then(mod => mod.default || mod);
        return;
      }
      loadModules[key] = value;
    });
    loadableOptions.loader = loadModules;
  }

  return loadableFn(loadableOptions);
}
```

#### 命令相关的文件

##### packages/umi/bin/umi.js

umi 命令的入口文件，`umi [option]`就会执行这个文件了。

```js
#!/usr/bin/env node

const resolveCwd = require('resolve-cwd');

const localCLI = resolveCwd.silent('umi/bin/umi'); //获取模块路径，测试结果为null

if (localCLI && localCLI !== __filename) {
  const debug = require('debug')('umi');
  debug('Using local install of umi');
  require(localCLI);
} else {
  require('../lib/cli');
} //执行cli
```

##### packages/umi/src/cli.js

从入口文件来到具体命令处理的文件

```js
import { dirname } from 'path';
import yParser from 'yargs-parser';
import signale from 'signale';
import semver from 'semver';
import buildDevOpts from './buildDevOpts';

//process.argv属性返回一个数组，其中包含当启动 Node.js 进程时传入的命令行参数。
const script = process.argv[2]; //获取第一个可选参数（数组前两个是路径）
const args = yParser(process.argv.slice(3)); //获取第一个可选参数之后的参数，转换成对象。如：umi dev -a -name=1，args为{_:[],a:true,name:1}

// Node版本检查
const nodeVersion = process.versions.node; //node版本号
if (semver.satisfies(nodeVersion, '<6.5')) {
  signale.error(`Node version must >= 6.5, but got ${nodeVersion}`);
  process.exit(1);
} //版本小于6.5提示node版本大于等于6.5并退出程序

// 进程退出（defer: true ）时通知更新
const updater = require('update-notifier');
const pkg = require('../package.json');
updater({ pkg }).notify({ defer: true });

process.env.UMI_DIR = dirname(require.resolve('../package')); //当前包根目录路径
process.env.UMI_VERSION = pkg.version; //当前包版本

const aliasMap = {
  '-v': 'version',
  '--version': 'version',
  '-h': 'help',
  '--help': 'help'
}; //扩展命令
//如果umi后面有build、dev、test、inspect参数就执行对应scripts文件中的脚本，否则引入umi-build-dev执行
switch (script) {
  case 'build':
  case 'dev':
  case 'test':
  case 'inspect':
    require(`./scripts/${script}`);
    break;
  default: {
    const Service = require('umi-build-dev/lib/Service').default;
    new Service(buildDevOpts(args)).run(aliasMap[script] || script, args);
    break;
  }
}
```

##### packages/umi/src/buildDevOpts.js

加载 env 环境并对应平台返回 app 目录路径

```js
//path.join() 方法使用平台特定的分隔符作为定界符将所有给定的 path 片段连接在一起，然后规范化生成的路径。
//path.isAbsolute() 方法检测 path 是否为绝对路径。
import { join, isAbsolute } from 'path';
//fs.readFileSync() 同步地读取文件的全部内容。
//fs.existsSync() 通过检查文件系统来测试给定的路径是否存在。
import { readFileSync, existsSync } from 'fs';
//isWindows 判断是否为Windows平台
import isWindows from 'is-windows';
//winPath 将Windows反斜杠路径转换为斜杠路径：foo\\bar➔foo/bar
import { winPath } from 'umi-utils';
import { parse } from 'dotenv';

export default function(opts = {}) {
  loadDotEnv(); //加载env环境
  let cwd = opts.cwd || process.env.APP_ROOT; //得到将传入路径或者环境设置路径
  if (cwd) {
    if (!isAbsolute(cwd)) {
      cwd = join(process.cwd(), cwd);
    } //cwd不是绝对路径转换为绝对路径
    cwd = winPath(cwd); //将Windows反斜杠路径转换为斜杠路径：foo\\bar➔foo/ba
    // 原因：webpack 的 include 规则得是 \ 才能判断出是绝对路径
    if (isWindows()) {
      cwd = cwd.replace(/\//g, '\\');
    } //如果是Windows平台将/替换为\\ foo/bar➔foo\\bar
    //感觉上面两步怎么不弄成一步来呢
  }

  return {
    cwd
  };
}

function loadDotEnv() {
  //process.cwd() 方法返回 Node.js 进程的当前工作目录。
  const baseEnvPath = join(process.cwd(), '.env'); //获取当前进程目录下.env路径
  const localEnvPath = `${baseEnvPath}.local`; //获取当前进程目录下.env.local路径

  const loadEnv = envPath => {
    //判断路径是否存在env的文件，存在就读取文件遍历设置env
    if (existsSync(envPath)) {
      const parsed = parse(readFileSync(envPath, 'utf-8'));
      Object.keys(parsed).forEach(key => {
        if (!process.env.hasOwnProperty(key)) {
          process.env[key] = parsed[key];
        }
      });
    }
  };
  //加载.env环境
  loadEnv(baseEnvPath);
  //加载.env.local环境覆盖.env环境
  loadEnv(localEnvPath);
}
```

##### packages/umi/src/scripts/build.js

构建执行脚本，实际调用 umi-build-dev 模块

```js
import yParser from 'yargs-parser';
import buildDevOpts from '../buildDevOpts';

process.env.NODE_ENV = 'production'; //设置环境为生产环境

const args = yParser(process.argv.slice(2));
const Service = require('umi-build-dev/lib/Service').default;
new Service(buildDevOpts(args)).run('build', args);
```

##### packages/umi/src/scripts/dev.js

开发执行脚本，实际调用 umi-build-dev 模块

```js
import fork from 'umi-build-dev/lib/fork';

const child = fork(require.resolve('./realDev.js'));
child.on('message', data => {
  if (process.send) {
    process.send(data);
  }
});
child.on('exit', code => {
  if (code === 1) {
    process.exit(code);
  }
});

process.on('SIGINT', () => {
  child.kill('SIGINT');
});
```

##### packages/umi/src/scripts/inspect.js

检查内部 Webpack 配置脚本文件

```js
import yParser from 'yargs-parser';
import buildDevOpts from '../buildDevOpts';

const args = yParser(process.argv.slice(2));

if (args.mode === 'production') {
  process.env.NODE_ENV = 'production';
} else {
  process.env.NODE_ENV = 'development';
} //如果命令指定了mode=production，则切换换生产环境否则为开发环境

const Service = require('umi-build-dev/lib/Service').default;
new Service(buildDevOpts(args)).run('inspect', args);
```

##### packages/umi/src/scripts/realDev.js

```js
import yParser from 'yargs-parser';
import buildDevOpts from '../buildDevOpts';

let closed = false;

// kill(2) Ctrl-C
process.once('SIGINT', () => onSignal('SIGINT'));
// kill(3) Ctrl-\
process.once('SIGQUIT', () => onSignal('SIGQUIT'));
// kill(15) default
process.once('SIGTERM', () => onSignal('SIGTERM'));

function onSignal(signal) {
  if (closed) return;
  closed = true;
  process.exit(0);
}

process.env.NODE_ENV = 'development';

const args = yParser(process.argv.slice(2));
const Service = require('umi-build-dev/lib/Service').default;
new Service(buildDevOpts(args)).run('dev', args);
```

#### 其他

##### packages/umi/src/test.js

测试脚本

```js
import yParser from 'yargs-parser';
import buildDevOpts from '../buildDevOpts';

process.env.NODE_ENV = 'development';

const args = yParser(process.argv.slice(2));
const Service = require('umi-build-dev/lib/Service').default;
new Service(buildDevOpts(args)).run('test', args);
```

##### packages/umi/src/babel.js

```js
export default function(context, opts = {}) {
  return {
    presets: [
      [
        require.resolve('babel-preset-umi'),
        {
          ...opts,
          preact: true
        }
      ]
    ]
  };
}
```

##### packages/umi/src/createHistory.js

```js
import createHistory from 'history/createBrowserHistory';
import { normalizePath } from './utils';

export default function(opts) {
  const history = createHistory(opts);
  if (__UMI_HTML_SUFFIX) {
    const oldPush = history.push;
    const oldReplace = history.replace;
    history.push = (path, state) => {
      oldPush(normalizePath(path), state);
    };
    history.replace = (path, state) => {
      oldReplace(normalizePath(path), state);
    };
  }
  return history;
}
```

##### packages/umi/src/prompt.js

```js
import { Prompt } from 'react-router-dom';
export default Prompt;
```

##### packages/umi/src/renderRoutes.js

```js
import React from 'react';
import { Switch, Route, Redirect } from 'react-router-dom';

const RouteInstanceMap = {
  get(key) {
    return key._routeInternalComponent;
  },
  has(key) {
    return key._routeInternalComponent !== undefined;
  },
  set(key, value) {
    key._routeInternalComponent = value;
  }
};

// Support pass props from layout to child routes
const RouteWithProps = ({ path, exact, strict, render, location, sensitive, ...rest }) => (
  <Route path={path} exact={exact} strict={strict} location={location} sensitive={sensitive} render={props => render({ ...props, ...rest })} />
);

function getCompatProps(props) {
  const compatProps = {};
  if (__UMI_BIGFISH_COMPAT) {
    if (props.match && props.match.params && !props.params) {
      compatProps.params = props.match.params;
    }
  }
  return compatProps;
}

function withRoutes(route) {
  if (RouteInstanceMap.has(route)) {
    return RouteInstanceMap.get(route);
  }

  const { Routes } = route;
  let len = Routes.length - 1;
  let Component = args => {
    const { render, ...props } = args;
    return render(props);
  };
  while (len >= 0) {
    const AuthRoute = Routes[len];
    const OldComponent = Component;
    Component = props => (
      <AuthRoute {...props}>
        <OldComponent {...props} />
      </AuthRoute>
    );
    len -= 1;
  }

  const ret = args => {
    const { render, ...rest } = args;
    return (
      <RouteWithProps
        {...rest}
        render={props => {
          return <Component {...props} route={route} render={render} />;
        }}
      />
    );
  };
  RouteInstanceMap.set(route, ret);
  return ret;
}

export default function renderRoutes(routes, extraProps = {}, switchProps = {}) {
  return routes ? (
    <Switch {...switchProps}>
      {routes.map((route, i) => {
        if (route.redirect) {
          return <Redirect key={route.key || i} from={route.path} to={route.redirect} exact={route.exact} strict={route.strict} />;
        }
        const RouteRoute = route.Routes ? withRoutes(route) : RouteWithProps;
        return (
          <RouteRoute
            key={route.key || i}
            path={route.path}
            exact={route.exact}
            strict={route.strict}
            sensitive={route.sensitive}
            render={props => {
              const childRoutes = renderRoutes(
                route.routes,
                {},
                {
                  location: props.location
                }
              );
              if (route.component) {
                const compatProps = getCompatProps({
                  ...props,
                  ...extraProps
                });
                const newProps = window.g_plugins.apply('modifyRouteProps', {
                  initialValue: {
                    ...props,
                    ...extraProps,
                    ...compatProps
                  },
                  args: { route }
                });
                return (
                  <route.component {...newProps} route={route}>
                    {childRoutes}
                  </route.component>
                );
              } else {
                return childRoutes;
              }
            }}
          />
        );
      })}
    </Switch>
  ) : null;
}
```

##### packages/umi/src/runtimePlugin.js

```js
import assert from 'assert';
import isPlainObject from 'lodash/isPlainObject';

let plugins = null;
let validKeys = [];

export function init(opts = {}) {
  plugins = [];
  validKeys = opts.validKeys || [];
}

export function use(plugin) {
  Object.keys(plugin).forEach(key => {
    // TODO: remove default
    // default 是为了兼容内部框架内置的一个 babel 插件问题
    assert(validKeys.concat('default').indexOf(key) > -1, `Invalid key ${key} from plugin`);
  });
  plugins.push(plugin);
}

export function getItem(key) {
  assert(validKeys.indexOf(key) > -1, `Invalid key ${key}`);
  return plugins.filter(plugin => key in plugin).map(plugin => plugin[key]);
}

function _compose(...funcs) {
  if (funcs.length === 1) {
    return funcs[0];
  }
  const last = funcs.pop();
  return funcs.reduce((a, b) => () => b(a), last);
}

export function compose(item, { initialValue }) {
  if (typeof item === 'string') item = getItem(item);
  return () => {
    return _compose(...item, initialValue)();
  };
}

export function apply(item, { initialValue, args }) {
  if (typeof item === 'string') item = getItem(item);
  assert(Array.isArray(item), `item must be Array`);
  return item.reduce((memo, fn) => {
    assert(typeof fn === 'function', `applied item must be function`);
    return fn(memo, args);
  }, initialValue);
}

export function applyForEach(item, { initialValue }) {
  if (typeof item === 'string') item = getItem(item);
  assert(Array.isArray(item), `item must be Array`);
  item.forEach(fn => {
    assert(typeof fn === 'function', `applied item must be function`);
    fn(initialValue);
  });
}

// shadow merge
export function mergeConfig(item) {
  if (typeof item === 'string') item = getItem(item);
  assert(Array.isArray(item), `item must be Array`);
  return item.reduce((memo, config) => {
    assert(isPlainObject(config), `Config is not plain object`);
    return { ...memo, ...config };
  }, {});
}
```

##### packages/umi/src/utils.js

```js
function addHtmlAffix(pathname) {
  if (pathname.slice(-1) === '/' || pathname.slice(-5) === '.html') {
    return pathname;
  } else {
    return `${pathname}.html`;
  }
}

export function normalizePath(path) {
  if (typeof path === 'string') {
    const [pathname, search] = path.split('?');
    return `${addHtmlAffix(pathname)}${search ? '?' : ''}${search || ''}`;
  }
  return {
    ...path,
    pathname: addHtmlAffix(path.pathname)
  };
}
```

### packages/umi-utils

辅助 umi 的模块

#### packages/umi-utils/src/winPath.js

```js
//将Windows反斜杠路径转换为斜杠路径：foo\\bar➔foo/ba
import slash from 'slash2';

export default function(path) {
  return slash(path);
}
```

### 总结 4/30

通过源码和视频学习了命令行运行包文件，虽然只是打印了`hello txp`（[demo](https://github.com/ShawDanon/txp/tree/master/packages/txp-first)）,阅读源码的同时对 node 印象更深刻了。疑惑的是 router 文件中的`window.g_history`不知道哪儿定义的，接下来需要看`umi-build-dev`模块了解构建运行的情况。

### 参考二

[配置 npm](https://docs.npmjs.com/files/package.json)
[Node.js 中文网](http://nodejs.cn/api/)
[基于 umi 封装自己的框架：sekiro](https://www.bilibili.com/video/av47877835)

## 学习 UMI（三）

umi@2.6.17

### 运行 umi 代码

阅读代码，看文档，总感觉缺点什么，经过云嫌和小虎两位大佬帮助，开始了 umi 代码调试之旅。其实上个月就想边运行边看代码，只是连安装开发依赖都没解决，所以拖到了现在。
整个流程如下（也可以参考[贡献文档](https://github.com/umijs/umi/blob/master/CONTRIBUTING.md)）：
1、克隆 umi 项目，在 umi 更目录装开发依赖，贡献文档是推荐用 yarn 装，不过要是网络不好，没有科学上网条件，会卡在装`puppeteer`上面，具体原因不是包上面是要下载`Chromium`的时候网络超时失败的。所以解决方案是通过 cnpm 装。

```js
cnpm i
```

2、安装各个包依赖，因为用的 lerna 作为包管理工具,所以运行`lerna bootstrap`进行安装，当然也可可以参照贡献文档使用`yarn bootstrap`装，这只是 umi 包的一个 script 转换而已。
3、为了方便使用需要把 umi 链接到全局，链接到全局和全局装包效果是一样的。首先切换到 umi 包目录，`cd packages/umi`，然后可以使用`npm link`或者`yarn link`，建议使用 yarn，npm 链接有点慢。
4、链接完成后就可以运行 umi 的命令了，我们试一试，结果提示找不到 lib 目录。因此我们需要切回根目录，运行`yarn build`对所有包进行构建生成 lib 目录文件，贡献文档命令是`yarn build --watch`可以实现实时构建。如此运行 umi 命令就和直接通过`npm i umi -g`命令安装一样了。

### inspect

目前能够运行本地 umi 代码了，可以在 umi 中加入`console.log()`来打印需要的参数，但是这样也不是很方面来理解代码。参照[官方文档](https://umijs.org/zh/guide/faq.html#%E5%A6%82%E4%BD%95%E6%96%AD%E7%82%B9%E8%B0%83%E8%AF%95)可以通过 inspect 进行断点调试。
inspect 调试方法：
1、全局安装 node-inspect 包

```js
npm i node-inspect -g
```

2、在 umi 包目录运行`node --inspect-brk ./bin/umi dev`,`./bin/umi`是运行文件相对执行环境位置,`dev`是执行参数。成功运行能够看到打印信息如下。

```js
Debugger listening on ws://127.0.0.1:9229/71f532b3-d619-4898-82ee-3145d817e5da
For help, see: https://nodejs.org/en/docs/inspector
```

3、进入调试器有两种方法，第一种是在谷歌浏览器输入`chrome://inspect/#devices`中打开，第二种是谷歌浏览器按 F12 唤醒开发者工具里打开，如下图。
![图一](../../img/2019/5-27-1.png)
调试器如下图，基本操作和平时调试差不多。唯一遇到的坑就是 require 其他文件的时候进不去，试过在代码里加 debugger 也不行。最后发现左侧 Node 栏里面的文件是根据代码运行变化的，require 模块后 Node 栏里就会多出相应模块的代码，然后这个时候通过 Node 栏打开代码打断点即可调试。
![图二](../../img/2019/5-27-2.png)

### umi 命令内部运行过程

目前主要看了 umi 包和 umi-build-dev 包，umi 主要提供运行时接口和编译时命令引导；umi-build-dev 包主要是编译时的工作，还包含内置插件（dev、build 等）。
例如运行`umi`这个命令不加任何参数：

1. 首先是进入 `packages/umi/bin/umi.js` 主文件，其功能是将命令分发到`packages/umi/src/cli.js`文件。
2. cli 文件对 umi 包进行检查，会提示版本更新。然后把命令分发到 script 文件执行命令，如果命令不存在直接执行命令。
3. 执行命令文件`packages/umi-build-dev/src/Service`是一个类，构造函数会注册 Babel、解析用户配置、解析插件（解析插件会把内置插件和用户配置插件整合到一个数组中）。
4. 然后命令执行运行类的 run 方法，如果 umi 命令没有参数则默认运行 help 命令。该方法会先初始化（加载环境.env、初始化插件、加载用户配置）。然后执行运行命令方法，该方法执行 umi 内部插件。

### 看过的一些源码及注释 packages/umi-build-dev

#### packages/umi-build-dev/src/Service

```js
import chalk from 'chalk'; //终端字符串样式做得很好(终端字符串颜色处理插件)
//path.dirname() 方法返回 path 的目录名，类似于 Unix 的 dirname 命令。
//path.join() 方法返回字符串拼接路径。
import { join, dirname } from 'path';
//existsSync 同步通过检查文件系统来测试给定的路径是否存在。
//readFileSync 同步读取文件
//writeFileSync 同步写入文件
import { existsSync, readFileSync, writeFileSync } from 'fs';
import assert from 'assert'; //此模块用于为您的应用程序编写单元测试
import mkdirp from 'mkdirp'; //mkdir -p作用，确保目录名称存在，如果目录不存在的就新创建一个。
//assign 浅拷贝
//cloneDeep 深拷贝
import { assign, cloneDeep } from 'lodash';
import { parse } from 'dotenv'; //Dotenv是一个零依赖模块，可以将.env文件中的环境变量加载到process.env
import signale from 'signale'; //可记录和可配置到核心，signale可用于记录目的，状态报告，以及处理其他节点模块和应用程序的输出呈现过程。终端中命令执行成功失败异常等的状态
//deprecate 用于终端上提示方法被弃用,传入(方法名，...想要提示的其他信息),调用方法终端输出提示信息。
import { deprecate } from 'umi-utils';
import getPaths from './getPaths';
import getPlugins from './getPlugins';
import PluginAPI from './PluginAPI';
import UserConfig from './UserConfig';
import registerBabel from './registerBabel';
import getCodeFrame from './utils/getCodeFrame';

const debug = require('debug')('umi-build-dev:Service');

//服务类
export default class Service {
  //构造函数传入目录
  constructor({ cwd }) {
    //cwd为app根目录
    //process.cwd() 方法返回 Node.js 进程的当前工作目录。
    this.cwd = cwd || process.cwd(); //如果不传入cwd，cwd为Node.js 进程的当前工作目录.
    try {
      this.pkg = require(join(this.cwd, 'package.json')); // 引入项目package.json，pkg为json对象
    } catch (e) {
      this.pkg = {}; //不存在package.json则pkg为空对象
    }

    registerBabel({
      cwd: this.cwd
    }); //注册Babel

    this.commands = {};
    this.pluginHooks = {};
    this.pluginMethods = {};
    this.generators = {};

    // 解析用户配置
    this.config = UserConfig.getConfig({
      cwd: this.cwd,
      service: this
    });
    debug(`user config: ${JSON.stringify(this.config)} `);

    // 解析插件，内置插件和用户插件解析
    this.plugins = this.resolvePlugins();
    this.extraPlugins = [];
    debug(`plugins: ${this.plugins.map(p => p.id).join(' | ')} `);

    // 相对路径
    this.paths = getPaths(this);
  }

  resolvePlugins() {
    try {
      assert(Array.isArray(this.config.plugins || []), `Configure item ${chalk.underline.cyan('plugins')} should be Array, but got ${chalk.red(typeof this.config.plugins)} `);
      return getPlugins({
        cwd: this.cwd,
        plugins: this.config.plugins || []
      });
    } catch (e) {
      if (process.env.UMI_TEST) {
        throw new Error(e);
      } else {
        signale.error(e);
        process.exit(1);
      }
    }
  } //解析插件

  initPlugin(plugin) {
    const { id, apply, opts } = plugin;
    try {
      assert(
        typeof apply === 'function',
        `
plugin must export a function, e.g.

export default function (api) {
  // Implement functions via api
}
`.trim()
      );
      const api = new Proxy(new PluginAPI(id, this), {
        get: (target, prop) => {
          if (this.pluginMethods[prop]) {
            return this.pluginMethods[prop];
          }
          if (
            [
              // methods
              'changePluginOption',
              'applyPlugins',
              '_applyPluginsAsync',
              'writeTmpFile',
              // properties
              'cwd',
              'config',
              'webpackConfig',
              'pkg',
              'paths',
              'routes',
              // dev methods
              'restart',
              'printError',
              'printWarn',
              'refreshBrowser',
              'rebuildTmpFiles',
              'rebuildHTML'
            ].includes(prop)
          ) {
            if (typeof this[prop] === 'function') {
              return this[prop].bind(this);
            } else {
              return this[prop];
            }
          } else {
            return target[prop];
          }
        }
      });
      api.onOptionChange = fn => {
        assert(typeof fn === 'function', `The first argument for api.onOptionChange should be function in ${id}.`);
        plugin.onOptionChange = fn;
      };
      apply(api, opts);
      plugin._api = api;
    } catch (e) {
      if (process.env.UMI_TEST) {
        throw new Error(e);
      } else {
        signale.error(
          `
Plugin ${chalk.cyan.underline(id)} initialize failed

${getCodeFrame(e, { cwd: this.cwd })}
`.trim()
        );
        debug(e);
        process.exit(1);
      }
    }
  } //初始化插件

  initPlugins() {
    this.plugins.forEach(plugin => {
      this.initPlugin(plugin);
    });

    let count = 0;
    while (this.extraPlugins.length) {
      const extraPlugins = cloneDeep(this.extraPlugins);
      this.extraPlugins = [];
      extraPlugins.forEach(plugin => {
        this.initPlugin(plugin);
        this.plugins.push(plugin);
      });
      count += 1;
      assert(count <= 10, `插件注册死循环？`);
    }

    // Throw error for methods that can't be called after plugins is initialized
    this.plugins.forEach(plugin => {
      ['onOptionChange', 'register', 'registerMethod', 'registerPlugin'].forEach(method => {
        plugin._api[method] = () => {
          throw new Error(`api.${method} () should not be called after plugin is initialized.`);
        };
      });
    });
  } //初始化插件集

  changePluginOption(id, newOpts) {
    assert(id, `id must supplied`);
    const plugin = this.plugins.filter(p => p.id === id)[0];
    assert(plugin, `plugin ${id} not found`);
    plugin.opts = newOpts;
    if (plugin.onOptionChange) {
      plugin.onOptionChange(newOpts);
    } else {
      this.restart(`plugin ${id} 's option changed`);
    }
  }

  applyPlugins(key, opts = {}) {
    debug(`apply plugins ${key}`);
    return (this.pluginHooks[key] || []).reduce((memo, { fn }) => {
      try {
        return fn({
          memo,
          args: opts.args
        });
      } catch (e) {
        console.error(chalk.red(`Plugin apply failed: ${e.message}`));
        throw e;
      }
    }, opts.initialValue);
  }

  async _applyPluginsAsync(key, opts = {}) {
    debug(`apply plugins async ${key}`);
    const hooks = this.pluginHooks[key] || [];
    let memo = opts.initialValue;
    for (const hook of hooks) {
      const { fn } = hook;
      memo = await fn({
        memo,
        args: opts.args
      });
    }
    return memo;
  }

  loadEnv() {
    const basePath = join(this.cwd, '.env'); //基础配置路径
    const localPath = `${basePath}.local`; //本地配置路径

    const load = path => {
      if (existsSync(path)) {
        debug(`load env from ${path}`);
        const parsed = parse(readFileSync(path, 'utf-8'));
        Object.keys(parsed).forEach(key => {
          if (!process.env.hasOwnProperty(key)) {
            process.env[key] = parsed[key];
          }
        });
      }
    };

    load(basePath); //加载基础配置
    load(localPath); //加载本地配置，覆盖基础配置
  } //加载环境

  writeTmpFile(file, content) {
    const { paths } = this;
    const path = join(paths.absTmpDirPath, file);
    mkdirp.sync(dirname(path));
    writeFileSync(path, content, 'utf-8');
  }

  init() {
    // 加载环境
    this.loadEnv();

    // 初始化插件
    this.initPlugins();

    // 加载用户配置
    const userConfig = new UserConfig(this);
    const config = userConfig.getConfig({ force: true });
    mergeConfig(this.config, config);
    this.userConfig = userConfig;
    if (config.browserslist) {
      deprecate('config.browserslist', 'use config.targets instead');
    }
    debug('got user config');
    debug(this.config);

    // assign user's outputPath config to paths object
    if (config.outputPath) {
      const { paths } = this;
      paths.outputPath = config.outputPath;
      paths.absOutputPath = join(paths.cwd, config.outputPath);
    }
    debug('got paths');
    debug(this.paths);
  } //初始化

  registerCommand(name, opts, fn) {
    if (typeof opts === 'function') {
      fn = opts;
      opts = null;
    }
    opts = opts || {};
    assert(!(name in this.commands), `Command ${name} exists, please select another one.`);
    this.commands[name] = { fn, opts };
  } //注册命令，在PluginAPI中调用

  run(name = 'help', args) {
    this.init(); //初始化
    return this.runCommand(name, args); //运行help命令
  } //启动servers

  runCommand(rawName, rawArgs) {
    debug(`raw command name: ${rawName}, args: ${JSON.stringify(rawArgs)}`);
    const { name, args } = this.applyPlugins('_modifyCommand', {
      initialValue: {
        name: rawName,
        args: rawArgs
      }
    });
    debug(`run ${name} with args ${JSON.stringify(args)}`);

    const command = this.commands[name];
    if (!command) {
      signale.error(`Command ${chalk.underline.cyan(name)} does not exists`);
      process.exit(1);
    }

    const { fn, opts } = command;
    if (opts.webpack) {
      // webpack config
      this.webpackConfig = require('./getWebpackConfig').default(this);
    }

    return fn(args);
  } //运行命令
}

function mergeConfig(oldConfig, newConfig) {
  Object.keys(oldConfig).forEach(key => {
    if (!(key in newConfig)) {
      delete oldConfig[key];
    }
  });
  assign(oldConfig, newConfig);
  return oldConfig;
} //合并配置项
```

#### packages/umi-build-dev/src/registerBabel

```js
import { join, isAbsolute } from 'path'; //引入拼接路径模块和判断是否为绝对路劲模块
import { existsSync } from 'fs'; //同步检查路肩是否存在模块
import registerBabel from 'af-webpack/registerBabel';
import { winPath } from 'umi-utils';
//获取umi配置文件路径的数组
import { getConfigPaths } from 'umi-core/lib/getUserConfig';

let files = null;

function initFiles(cwd) {
  if (files) return;
  files = getConfigPaths(cwd); //传入node运行时路径
} //初始化文件，若文件存在则忽略

export function addBabelRegisterFiles(extraFiles, { cwd }) {
  initFiles(cwd);
  files.push(...extraFiles);
}

export default function({ cwd }) {
  initFiles(cwd);
  const only = files.map(f => {
    const fullPath = isAbsolute(f) ? f : join(cwd, f);
    return winPath(fullPath);
  }); //转化路径

  let absSrcPath = join(cwd, 'src'); //获取src目录路径
  if (!existsSync(absSrcPath)) {
    absSrcPath = cwd;
  } //如果不存在src目录则把根目录作为src目录

  registerBabel({
    // only suport glob
    // ref: https://babeljs.io/docs/en/next/babel-core.html#configitem-type
    only,
    babelPreset: [
      require.resolve('babel-preset-umi'),
      {
        env: { targets: { node: 8 } },
        transformRuntime: false
      }
    ],
    babelPlugins: [
      [
        require.resolve('babel-plugin-module-resolver'),
        {
          alias: {
            '@': absSrcPath
          }
        }
      ]
    ]
  });
}
```

#### packages/umi-build-dev/src/UserConfig

```js
import { join } from 'path';
import requireindex from 'requireindex';
import chalk from 'chalk';
import didyoumean from 'didyoumean';
import { cloneDeep } from 'lodash';
import signale from 'signale';
import getUserConfig, { getConfigPaths, getConfigFile, getConfigByConfigFile, cleanConfigRequireCache } from 'umi-core/lib/getUserConfig';
import { watch, unwatch } from './getConfig/watch';
import isEqual from './isEqual';

class UserConfig {
  static getConfig(opts = {}) {
    const { cwd, service } = opts;
    return getUserConfig({
      cwd,
      defaultConfig: service.applyPlugins('modifyDefaultConfig', {
        initialValue: {}
      })
    });
  }

  constructor(service) {
    this.service = service;
    this.configFailed = false;
    this.config = null;
    this.file = null;
    this.relativeFile = null;
    this.watch = watch;
    this.unwatch = unwatch;
    this.initConfigPlugins();
  }

  initConfigPlugins() {
    const map = requireindex(join(__dirname, 'getConfig/configPlugins'));
    let plugins = Object.keys(map).map(key => {
      return map[key].default;
    });
    plugins = this.service.applyPlugins('_registerConfig', {
      initialValue: plugins
    });
    this.plugins = plugins.map(p => p(this));
  }

  printError(messages) {
    if (this.service.printError) this.service.printError(messages);
  }

  getConfig(opts = {}) {
    const { paths, cwd } = this.service;
    const { force, setConfig } = opts;
    const defaultConfig = this.service.applyPlugins('modifyDefaultConfig', {
      initialValue: {}
    });

    const file = getConfigFile(cwd);
    this.file = file;
    if (!file) {
      return defaultConfig;
    }

    // 强制读取，不走 require 缓存
    if (force) {
      cleanConfigRequireCache(cwd);
    }

    let config = null;
    const relativeFile = file.replace(`${paths.cwd}/`, '');
    this.relativeFile = relativeFile;

    const onError = (e, file) => {
      const msg = `配置文件 "${file.replace(`${paths.cwd}/`, '')}" 解析出错，请检查语法。
\r\n${e.toString()}`;
      this.printError(msg);
      throw new Error(msg);
    };

    config = getConfigByConfigFile(file, {
      defaultConfig,
      onError
    });

    config = this.service.applyPlugins('_modifyConfig', {
      initialValue: config
    });

    // Validate
    for (const plugin of this.plugins) {
      const { name, validate } = plugin;
      if (config[name] && validate) {
        try {
          plugin.validate.call({ cwd }, config[name]);
        } catch (e) {
          // 校验出错后要把值设到缓存的 config 里，确保 watch 判断时才能拿到正确的值
          if (setConfig) {
            setConfig(config);
          }
          this.printError(e.message);
          throw new Error(`配置 ${name} 校验失败, ${e.message}`);
        }
      }
    }

    // 找下不匹配的 name
    const pluginNames = this.plugins.map(p => p.name);
    Object.keys(config).forEach(key => {
      if (!pluginNames.includes(key)) {
        if (opts.setConfig) {
          opts.setConfig(config);
        }
        const affixmsg = `选择 "${pluginNames.join(', ')}" 中的一项`;
        const guess = didyoumean(key, pluginNames);
        const midMsg = guess ? `你是不是想配置 "${guess}" ？ 或者` : '请';
        const msg = `"${relativeFile}" 中配置的 "${key}" 并非约定的配置项，${midMsg}${affixmsg}`;
        this.printError(msg);
        throw new Error(msg);
      }
    });

    return config;
  }

  setConfig(config) {
    this.config = config;
  }

  watchWithDevServer() {
    // 配置插件的监听
    for (const plugin of this.plugins) {
      if (plugin.watch) {
        plugin.watch();
      }
    }

    // 配置文件的监听
    this.watchConfigs((event, path) => {
      signale.debug(`[${event}] ${path}`);
      try {
        const newConfig = this.getConfig({
          force: true,
          setConfig: newConfig => {
            this.config = newConfig;
          }
        });

        // 从失败中恢复过来，需要 reload 一次
        if (this.configFailed) {
          this.configFailed = false;
          this.service.refreshBrowser();
        }

        const oldConfig = cloneDeep(this.config);
        this.config = newConfig;

        for (const plugin of this.plugins) {
          const { name } = plugin;
          if (!isEqual(newConfig[name], oldConfig[name])) {
            this.service.config[name] = newConfig[name];
            this.service.applyPlugins('onConfigChange', {
              args: {
                newConfig
              }
            });
            if (plugin.onChange) {
              plugin.onChange(newConfig, oldConfig);
            }
          }
        }
      } catch (e) {
        this.configFailed = true;
        console.error(chalk.red(`watch handler failed, since ${e.message}`));
        console.error(e);
      }
    });
  }

  watchConfigs(handler) {
    const { cwd } = this.service;
    const watcher = this.watch('CONFIG_FILES', getConfigPaths(cwd));
    if (watcher) {
      watcher.on('all', handler);
    }
  }
}

export default UserConfig;
```

#### packages/umi-build-dev/src/getPaths

```js
```

#### packages/umi-build-dev/src/getPlugins

```js
//实现节点require.resolve() 算法 ，以便您可以require.resolve()异步和同步代表文件
import resolve from 'resolve';
//assert来自Node.js 的模块，用于浏览器。使用browserify，只需require('assert')或使用assert全局，您将获得此模块。目标是提供尽可能与Node.js assertAPI功能相同的API。阅读API文档的官方文档。
import assert from 'assert';
import chalk from 'chalk'; //终端字符串样式修改
import registerBabel, { addBabelRegisterFiles } from './registerBabel';
import isEqual from './isEqual';
import getCodeFrame from './utils/getCodeFrame';

const debug = require('debug')('umi-build-dev:getPlugin');

export default function(opts = {}) {
  const { cwd, plugins = [] } = opts;
  // 内置插件
  const builtInPlugins = [
    './plugins/commands/dev',
    './plugins/commands/build',
    './plugins/commands/inspect',
    './plugins/commands/test',
    './plugins/commands/help',
    './plugins/commands/generate',
    './plugins/commands/rm',
    './plugins/commands/config',
    './plugins/commands/block',
    // './plugins/commands/ui',
    './plugins/commands/version',
    './plugins/global-js',
    './plugins/global-css',
    './plugins/base',
    './plugins/mountElementId',
    './plugins/mock',
    './plugins/proxy',
    './plugins/history',
    './plugins/afwebpack-config',
    './plugins/mountElementId',
    './plugins/404', // 404 must after mock
    './plugins/targets'
  ];

  const pluginsObj = [
    // builtIn 的在最前面
    ...builtInPlugins.map(p => {
      let opts;
      if (Array.isArray(p)) {
        opts = p[1]; // eslint-disable-line
        p = p[0];
      }
      const apply = require(p); // eslint-disable-line
      return {
        id: p.replace(/^.\//, 'built-in:'),
        apply: apply.default || apply,
        opts
      };
    }),
    ...getUserPlugins(process.env.UMI_PLUGINS ? process.env.UMI_PLUGINS.split(',') : [], { cwd }),
    ...getUserPlugins(plugins, { cwd })
  ];

  debug(`plugins: \n${pluginsObj.map(p => `  ${p.id}`).join('\n')}`);
  return pluginsObj;
}

function pluginToPath(plugins, { cwd }) {
  return (plugins || []).map(p => {
    assert(Array.isArray(p) || typeof p === 'string', `Plugin config should be String or Array, but got ${chalk.red(typeof p)}`);
    if (typeof p === 'string') {
      p = [p];
    }
    const [path, opts] = p;
    try {
      return [
        resolve.sync(path, {
          basedir: cwd
        }),
        opts
      ];
    } catch (e) {
      throw new Error(
        `
Plugin ${chalk.underline.cyan(path)} can't be resolved

   Please try the following solutions:

     1. checkout the plugins config in your config file (.umirc.js or config/config.js)
     ${path.charAt(0) !== '.' && path.charAt(0) !== '/' ? `2. install ${chalk.underline.cyan(path)} via npm/yarn` : ''}
`.trim()
      );
    }
  });
}

function getUserPlugins(plugins, { cwd }) {
  const pluginPaths = pluginToPath(plugins, { cwd });

  // 用户给的插件需要做 babel 转换
  if (pluginPaths.length) {
    addBabelRegisterFiles(pluginPaths.map(p => p[0]), { cwd });
    registerBabel({
      cwd
    });
  }

  return pluginPaths.map(p => {
    const [path, opts] = p;
    let apply;
    try {
      apply = require(path); // eslint-disable-line
    } catch (e) {
      throw new Error(
        `
Plugin ${chalk.cyan.underline(path)} require failed

${getCodeFrame(e)}
      `.trim()
      );
    }
    return {
      id: path.replace(makesureLastSlash(cwd), 'user:'),
      apply: apply.default || apply,
      opts
    };
  });
}

function resolveIdAndOpts({ id, opts }) {
  return { id, opts };
}

function toIdStr(plugins) {
  return plugins.map(p => p.id).join('^^');
}

/**
 * 返回结果：
 *   pluginsChanged: true | false
 *   optionChanged: [ 'a', 'b' ]
 */
export function diffPlugins(newOption, oldOption, { cwd }) {
  const newPlugins = getUserPlugins(newOption, { cwd }).map(resolveIdAndOpts);
  const oldPlugins = getUserPlugins(oldOption, { cwd }).map(resolveIdAndOpts);

  if (newPlugins.length !== oldPlugins.length) {
    return { pluginsChanged: true };
  } else if (toIdStr(newPlugins) !== toIdStr(oldPlugins)) {
    return { pluginsChanged: true };
  } else {
    return {
      optionChanged: newPlugins.filter((p, index) => {
        return !isEqual(newPlugins[index].opts, oldPlugins[index].opts);
      })
    };
  }
}

function makesureLastSlash(path) {
  return path.slice(-1) === '/' ? path : `${path}/`;
}
```

#### packages/umi-build-dev/src/utils/deprecate

用于终端上提示方法被弃用,传入(方法名，...想要提示的其他信息),调用方法终端输出提示信息。

```js
//process.platform属性返回字符串，标识Node.js进程运行其上的操作系统平台。
const isWindows = typeof process !== 'undefined' && process.platform === 'win32';
const EOL = isWindows ? '\r\n' : '\n';
//判断是否是windows更具系统选择换行符号

const hits = {};
export default function deprecate(methodName, ...args) {
  if (hits[methodName]) return;
  hits[methodName] = true;
  //process.stderr 属性返回连接到 stderr (fd 2) 的流。 它是一个 net.Socket 流（也就是双工流），除非 fd 2 指向一个文件，在这种情况下它是一个可写流。console.error() 内部分别是由它实现的。
  const stream = process.stderr;
  //判断 Node.js 是否在 TTY 上下文中运行的首选方法是检查 process.stdout.isTTY 属性的值是否为 true：
  const color = stream.isTTY && '\x1b[31;1m';
  //如果上下文是终端设置亮黄色加粗字体

  stream.write(EOL); //终端写入换行
  if (color) {
    stream.write(color);
  }

  stream.write(`Warning: ${methodName} has been deprecated.`); //警告方法名已经被弃用
  stream.write(EOL); //换行
  args.forEach(message => {
    stream.write(message); //打印参数
    stream.write(EOL); //换行
  });
  if (color) {
    stream.write('\x1b[0m');
  } //把字体还原
  stream.write(EOL);
  stream.write(EOL);
}
```
