---
title: 'VSCode'
category: 技术
tags: [工具]
date: 2018-08-12
updated: 2018-08-12
---

工欲善其事必先利其器...

<!-- more -->

# 常用插件

Add jsdoc comments(快速添加 jsdoc 插件)
Atom One Dark Theme(Atom 颜色主题)
Bracket Pair Colorizer(每一对括号用不同颜色区别)
cssrem(px 转 rem)
Debugger for Chrome(在编辑器里面 debug)
ESLint(代码检查)
Git History(图形化 git 历史记录)
GitLens — Git supercharged(显示每行代码作者|日期|提交备注)
HTML CSS Support(HTML 中 CSS 智能提示)
Markdown All in One(Markdown 快捷输入)
markdownlint(Markdown 检查)
open in browser(通过浏览器运行 HTML)
Path Intellisense(路径智能提示)
Prettier - Code formatter(代码格式化)
Settings Sync(多台电脑同步配置)
Sublime Text Keymap and Settings Importer(sublime 键位设置)
Vetur(vue 提示扩展)
vscode-icons(图标主题)

# 用户设置

## Commonly Used(常用)

```
"editor.fontSize": 13, //以像素为单位控制字号
"editor.fontFamily": "Consolas", //控制字体系列
"editor.tabSize": 2, //一个制表符等于的空格数
"editor.renderWhitespace": "none",//控制编辑器在空白字符上显示特殊符号的方式。
"editor.multiCursorModifier": "ctrlCmd", //在通过鼠标添加多个光标时使用的修改键。
"files.exclude": {
"**/.idea": true,
"**/yarn.lock": true,
"**/tmp": true
}, //配置 glob 模式以在搜索中排除文件和文件夹。例如，文件资源管理器根据此设置决定文件或文件夹的显示和隐藏。
"files.associations": {
"_.vue": "vue",
"_.wxss": "css"
}, //配置语言的文件关联(如: "*.extension": "html")。这些关联的优先级高于已安装语言的默认关联。
```

## 整个配置

```
{
  // "apicloud.port": "23450", // 开启apicloud在vscode中的wifi真机同步
  // "apicloud.subdirectories": "/apiclouduser", // 设置apicloud在vscode中的wifi真机同步根目录
  /*编辑器*/
  //每行字数 防止{} []换行
  "editor.cursorBlinking": "smooth",
  //控制字体系列
  "editor.fontFamily": "Consolas",
  //以像素为单位控制字号
  "editor.fontSize": 13,
  //控制编辑器是否应自动设置粘贴内容的格式。
  "editor.formatOnPaste": true,
  //保存时设置文件的格式。格式化程序必须可用，不能自动保存文件，并且不能关闭编辑器。
  "editor.formatOnSave": true,
  //控制行高。使用 0 通过字号计算行高。
  "editor.lineHeight": 24,
  //在通过鼠标添加多个光标时使用的修改键。
  "editor.multiCursorModifier": "ctrlCmd",
  //控制编辑器应如何呈现当前行突出显示，可能为“无”、“装订线”、“线”和“全部”。
  "editor.renderLineHighlight": "none",
  //控制编辑器在空白字符上显示特殊符号的方式。
  "editor.renderWhitespace": "none",
  //控制是否将代码段与其他建议一起显示以及它们的排序方式。
  "editor.snippetSuggestions": "top",
  //一个制表符等于的空格数
  "editor.tabSize": 2,
  /*工作台*/
  //指定在工作台中使用的图标主题，或指定 "null" 以不显示任何文件图标。
  "workbench.iconTheme": "vscode-icons",
  //在未能恢复上一会话信息的情况下，控制启动时显示的编辑器。
  "workbench.startupEditor": "newUntitledFile",
  /*窗口*/
  //调整窗口的缩放级别。原始大小是 0，每次递增(例如 1)或递减(例如 -1)表示放大或缩小 20%。也可以输入小数以便以更精细的粒度调整缩放级别。
  "window.zoomLevel": 2,
  /*文件*/
  //配置语言的文件关联(如: "*.extension": "html")。这些关联的优先级高于已安装语言的默认关联。
  "files.associations": {
    "_.vue": "vue",
    "_.wxss": "css"
  },
  //配置 glob 模式以在搜索中排除文件和文件夹。例如，文件资源管理器根据此设置决定文件或文件夹的显示和隐藏。
  "files.exclude": {
    "**/.idea": true,
    "**/yarn.lock": true,
    "**/tmp": true
  },
  //保存裁剪空格
  "files.trimTrailingWhitespace": true,
  /*搜索*/
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
  /*HTML*/
  //配置内置 HTML 语言支持是否建议 Angular V1 标记和属性。
  "html.suggest.angular1": false,
  //配置内置 HTML 语言支持是否建议 Ionic 标记、属性和值。
  "html.suggest.ionic": false,
  /*TypeScript*/
  //在 VS Code 中重命名或移动文件时启用或禁用自动更新 import 语句的路径。
  "javascript.updateImportsOnFileMove.enabled": "always",
  /*ESLint*/
  //文件保存时，是否自动根据 eslint 进行格式化
  "eslint.autoFixOnSave": false,
  // 是否开启 eslint 检测
  "eslint.enable": false,
  //eslint 配置文件
  "eslint.options": {
    "plugins": [
      "html",
      "javascript",
      {
        "language": "vue",
        "autoFix": true
      },
      "vue"
    ]
  },
  //eslint 能够识别的文件后缀类型
  "eslint.validate": ["javascript", "javascriptreact", "html", "vue", "typescript", "typescriptreact"],
  /*Gitlens Configuration*/
  //细节,配置 gitlen 中 git 提交历史记录的信息显示情况
  "gitlens.advanced.messages": {
    "suppressShowKeyBindingsNotice": true,
    "suppressUpdateNotice": true
  },
  //开启 eslint 规则
  // prettier 进行格式化时是否安装 eslint 配置去执行，建议 false
  "prettier.eslintIntegration": true,
  //如果为真，则将多行JSX元素的“>”放在最后一行的末尾，而不是单独在下一行上。
  "prettier.jsxBracketSameLine": true,
  //在该行限制中拟合代码
  "prettier.printWidth": 200,
  //启用单引号
  "prettier.singleQuote": true,
  /*代码同步配置*/
  "sync.askGistName": false,
  "sync.autoDownload": false,
  "sync.autoUpload": false,
  "sync.forceDownload": false,
  "sync.gist": "15fbbb532bfd2b103dc345b36e298f4b",
  "sync.quietSync": false,
  "sync.removeExtensions": true,
  "sync.syncExtensions": true,
  "sync.host": "",
  "sync.pathPrefix": "",
  "sync.lastUpload": "",
  "sync.lastDownload": "2018-08-17T02:21:37.318Z",
  /*Git*/
  //是否启用自动拉取
  "git.autofetch": true,
  //在没有暂存的更改时提交所有更改。
  "git.enableSmartCommit": true,
  /*Emmet*/
  //在默认不支持 Emmet 的语言中启用 Emmet 缩写功能。
  "emmet.includeLanguages": {
    "jsx-sublime-babel-tags": "javascriptreact"
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
  "emmet.triggerExpansionOnTab": true
}
```

# 快捷键

```
{
"key": "cmd+h",
"command": "workbench.action.terminal.toggleTerminal"
},//打开和关闭终端窗口，关闭窗口后里面的命令行会照常运行，再次打开后依然可见
{
"key": "cmd+t",
"command": "workbench.action.terminal.new",
"when": "terminalFocus"
},新建终端，一个终端窗口中，可以创建多个终端
{
"key": "cmd+right",
"command": "workbench.action.terminal.focusNext",
"when": "terminalFocus"
},可以在终端间切换
{
"key": "cmd+left",
"command": "workbench.action.terminal.focusPrevious",
"when": "terminalFocus"
},
{
"key": "cmd+w",
"command": "workbench.action.terminal.kill",
"when": "terminalFocus"
}不想要的终端，用 cmd-w 来关闭
```
