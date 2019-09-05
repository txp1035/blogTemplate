---
title: 'VSCode'
category: 技术
tags: [工具]
date: 2018-08-12
---

工欲善其事必先利其器...

<!-- more -->

## 常用插件

### 我的插件

1. 必备插件：
   - Chinese (Simplified) Language Pack for Visual Studio Code(简体中文)
   - Settings Sync(多台电脑同步配置)
2. 编辑器插件：
   - Sublime Text Keymap and Settings Importer(sublime 键位设置)
   - vscode-icons(图标主题)
   - Bracket Pair Colorizer(每一对括号用不同颜色区别)
3. git 管理：
   - Git History(图形化 git 历史记录)
   - GitLens — Git supercharged(git 管理利器)
4. 代码风格标准：
   - ESLint(js、ts 代码检查提示)
   - stylelint(css、less 代码检查提示)
   - markdownlint(Markdown 代码检查提示)
   - EditorConfig for VS Code(编辑器统一风格插件)
   - Prettier - Code formatter(代码格式化)
5. 自动处理：
   - Markdown All in One(Markdown 快捷输入)
   - Umi Pro(umi 使用更方便)

### 推荐插件

Add jsdoc comments(快速添加 jsdoc 插件)
Atom One Dark Theme(Atom 颜色主题)
cssrem(px 转 rem)
Debugger for Chrome(在编辑器里面 debug)
Easy LESS(less 文件转 css)
ES7 React/Redux/GraphQL/React-Native snippets（react 常用代码片段）
HTML CSS Support(HTML 中 CSS 智能提示)
open in browser(通过浏览器运行 HTML)
Path Intellisense(路径智能提示)
Power Mode(输入代码很酷炫的效果)
Vetur(vue 提示扩展)
Dart(flutter 需要)
Flutter(flutter 需要)
pont（mock 数据自动化）
React Native Tools(native 需要)
Smarty(一个模板引擎高亮)
TSLint(代码检查工具)

## 用户设置

### vscode 配置

```json
   /* 文本编辑器 start */
  //以像素为单位控制字号
  "editor.fontSize": 15,
  //控制编辑器是否应自动设置粘贴内容的格式。
  "editor.formatOnPaste": true,
  //保存时设置文件的格式。格式化程序必须可用，不能自动保存文件，并且不能关闭编辑器。
  "editor.formatOnSave": true,
  //控制行高。使用 0 通过字号计算行高。
  "editor.lineHeight": 25,
  //控制是否显示 minimap
  "editor.minimap.enabled": false,
  //在通过鼠标添加多个光标时使用的修改键。
  "editor.multiCursorModifier": "ctrlCmd",
  //控制编辑器应如何呈现当前行突出显示，可能为“无”、“装订线”、“线”和“全部”。
  "editor.renderLineHighlight": "none",
  //控制是否将代码段与其他建议一起显示以及它们的排序方式。
  "editor.snippetSuggestions": "top",
  //一个制表符等于的空格数
  "editor.tabSize": 2,
  //在未能恢复上一会话信息的情况下，控制启动时显示的编辑器。
  "workbench.startupEditor": "newUntitledFile",
  //配置语言的文件关联(如: "*.extension": "html")。这些关联的优先级高于已安装语言的默认关联。
  "files.associations": {
    "_.vue": "vue",
    "_.wxss": "css"
  },
  //配置 glob 模式以在搜索中排除文件和文件夹。例如，文件资源管理器根据此设置决定文件或文件夹的显示和隐藏。
  "files.exclude": {
    "**/.idea": true,
    "**/yarn.lock": true,
    "**/node_modules": true,
    "**/dist": true,
    "**/tmp": true
  },
  //配置 glob 模式以在搜索中排除文件和文件夹。
  "search.exclude": {
    "**/dist": true,
    "**/build": true,
    "**/elehukouben": true,
    "**/.git": true,
    "**/.gitignore": true,
    "**/.svn": true,
    "**/.DS_Store": true,
    "**/.idea": true,
    "**/.vscode": false,
    "**/yarn.lock": true,
    "**/tmp": true
  },
  //保存裁剪空格
  "files.trimTrailingWhitespace": true,
  /* 文本编辑器 end */
  /* 工作台 start */
  "workbench.activityBar.visible": false,
  "workbench.iconTheme": "vscode-icons",
  /* 工作台 end */
  /* 窗口 start */
  //调整窗口的缩放级别。原始大小是 0，每次递增(例如 1)或递减(例如 -1)表示放大或缩小 20%。也可以输入小数以便以更精细的粒度调整缩放级别。
  "window.zoomLevel": 2,
  /* 窗口 end */
  /* 功能 start */
  //控制终端的行高，此数字乘上终端字号得到实际行高(以像素为单位)。
  "terminal.integrated.lineHeight": 1.8,
  //解决cpu占用大问题，rg服务。
  "search.followSymlinks": false,
  /* 功能 end */
  /* 内部扩展 start */
  /* Git */
  //是否启用自动拉取
  "git.autofetch": true,
  //在没有暂存的更改时提交所有更改。
  "git.enableSmartCommit": true,
  //在同步git存储库之前确认。
  "git.confirmSync": false,
  /* TypeScript */
  //在 VS Code 中重命名或移动文件时启用或禁用自动更新 import 语句的路径。
  "javascript.updateImportsOnFileMove.enabled": "always",
  "typescript.updateImportsOnFileMove.enabled": "always",
  /* CSS */
  //启用或禁用所有验证。
  "css.validate": true,
  /* LESS */
  "less.validate": true,
  /* Emmet */
  //在默认不支持 Emmet 的语言中启用 Emmet 缩写功能。
  "emmet.includeLanguages": {
    "jsx-sublime-babel-tags": "javascriptreact",
    "javascript": "javascriptreact"
  },
  //为指定的语法定义配置文件或使用带有特定规则的配置文件。
  "emmet.syntaxProfiles": {
    "vue-html": "html",
    "vue": "html",
    "javascript": "javascriptreact",
    // xml 类型文件默认都是单引号，开启对非单引号的 emmet 识别
    "xml": {
      "attr_quotes": "single"
    }
  },
  //启用后，按下 TAB 键，将展开 Emmet 缩写。
  "emmet.triggerExpansionOnTab": true,
  /* Node debug */
  "terminal.integrated.shell.osx": "zsh",
  /* 内部扩展 end */
```

### 外部插件

```json
{
  /* 外部扩展 start */
  /* Gitlens Configuration */
  //细节,配置 gitlen 中 git 提交历史记录的信息显示情况
  "gitlens.advanced.messages": {
    "suppressShowKeyBindingsNotice": true,
    "suppressUpdateNotice": true
  },
  /* ESLint */
  //文件保存时，是否自动根据 eslint 进行格式化
  "eslint.autoFixOnSave": true,
  // 是否开启 eslint 检测
  "eslint.enable": true,
  //eslint 能够识别的文件后缀类型
  "eslint.validate": [
    {
      "language": "html",
      "autoFix": false
    },
    {
      "language": "javascript",
      "autoFix": false
    },
    {
      "language": "javascriptreact",
      "autoFix": false
    },
    {
      "language": "typescript",
      "autoFix": false
    },
    {
      "language": "typescriptreact",
      "autoFix": false
    },
    {
      "language": "vue",
      "autoFix": false
    }
  ],
  /* prettier */
  //开启 eslint 规则
  // prettier 进行格式化时是否安装 eslint 配置去执行，建议 false
  "prettier.eslintIntegration": true,
  //如果为真，则将多行JSX元素的“>”放在最后一行的末尾，而不是单独在下一行上。
  "prettier.jsxBracketSameLine": true,
  //在该行限制中拟合代码
  "prettier.printWidth": 200,
  //启用单引号
  "prettier.singleQuote": true
  /* 外部扩展 end */
}
```

## 快捷键

```js
// 将按键绑定配置放入此文件中即可覆盖默认值
[
  {
    key: 'ctrl+f1',
    command: 'extension.openInBrowser'
  },
  {
    key: 'alt+b',
    command: '-extension.openInBrowser'
  },
  {
    key: 'alt+t',
    command: 'toggleFindInSelection',
    when: 'editorFocus'
  },
  {
    key: 'alt+l',
    command: '-toggleFindInSelection',
    when: 'editorFocus'
  },
  /*方向键和选择提示键位*/
  {
    key: 'alt+j',
    command: 'cursorLeft',
    when: 'textInputFocus'
  },
  {
    key: 'left',
    command: '-cursorLeft',
    when: 'textInputFocus'
  },
  {
    key: 'alt+i',
    command: 'cursorUp',
    when: 'textInputFocus'
  },
  {
    key: 'up',
    command: '-cursorUp',
    when: 'textInputFocus'
  },
  {
    key: 'alt+k',
    command: 'cursorDown',
    when: 'textInputFocus'
  },
  {
    key: 'down',
    command: '-cursorDown',
    when: 'textInputFocus'
  },
  {
    key: 'alt+l',
    command: 'cursorRight',
    when: 'textInputFocus'
  },
  {
    key: 'right',
    command: '-cursorRight',
    when: 'textInputFocus'
  },
  {
    key: 'alt+i',
    command: 'selectPrevSuggestion',
    when: 'suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus'
  },
  {
    key: 'up',
    command: '-selectPrevSuggestion',
    when: 'suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus'
  },
  {
    key: 'alt+k',
    command: 'selectNextSuggestion',
    when: 'suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus'
  },
  {
    key: 'down',
    command: '-selectNextSuggestion',
    when: 'suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus'
  }
];
```

## 代码片段

```json
{
  "head": {
    "prefix": "head",
    "body": ["---", "title: '$1'", "category: $2", "tags: [$3]", "date: $4", "---"],
    "description": "快速输入博客头部"
  },
  "log": {
    "prefix": "log",
    "body": "console.log($1)"
  },
  "warn": {
    "prefix": "warn",
    "body": "console.warn(${1:'后端返回数据问题'});"
  },
  "ims": {
    "prefix": "ims",
    "body": "import ${1:styles} from '${2:./index.less}';"
  },
  "dva": {
    "prefix": "dva",
    "body": "import { connect } from 'dva';"
  },
  "dvac": {
    "prefix": "dvac",
    "body": ["@connect(({ ${1:sale} }) => ({", "  ${2:sale},", "}))"]
  },
  "menuSetting": {
    "prefix": "menuSetting",
    "body": ["{", "  path: '${1:/dashboard}',", "  name: '${2:dashboard}',", "  icon: '${3:dashboard}',", "  routes: [$4],", "},"],
    "description": "菜单"
  }
}
```
