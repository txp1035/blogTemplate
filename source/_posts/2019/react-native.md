---
title: 'reactNative'
category: 技术
tags: [笔记, 前端]
date: 2019-4-8
---

感受用 react-native 写 app...

<!-- more -->

## 环境搭建

### Mac 上安卓 App 开发

必须安装的依赖有：Node、Watchman 和 React Native 命令行工具以及 JDK 和 Android Studio。
其中大部分安装在 [flutter](../flutter) 已有。

### 创建项目

运行`react-native init [项目名]`在当前目录创建项目

## 运行调试

在项目根目录运行`react-native run-android`启动项目

### 虚拟机

双击 r 刷新

### 真机

摇一摇手机呼出调试面板，点击`Enable Hot Reloading`启用热加载（Ps：需要保证电脑和手机在同一网络中）。

## 打包发布

### 生成一个签名密钥

在终端输入命令`keytool -genkeypair -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000`，根据提示输入密码、信息等，看到提示说是否正确是填入`y`回车，就能在当前目录生成你的签名密钥了，这个时候终端会提示让你输入命令迁移到新版本密钥，根据提示输入`keytool -importkeystore -srckeystore my-release-key.keystore -destkeystore my-release-key.keystore -deststoretype pkcs12`，执行完当前目录会多出一个.old 的文件（原来密钥的备份文件）。

### 设置 gradle 变量

首先把 my-release-key.keystore 文件（你的密钥文件）放到你工程中的 android/app 文件夹下。

编辑~/.gradle/gradle.properties（全局配置，对所有项目有效）或是项目目录/android/gradle.properties（项目配置，只对所在项目有效）。如果没有 gradle.properties 文件你就自己创建一个，添加如下的代码（注意把其中的\*\*\*\*替换为相应密码）

```js
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```

### 把签名配置加入到项目的 gradle 配置中

编辑你项目目录下的 android/app/build.gradle，添加如下的签名配置：

```js
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }//这个必须写在buildTypes前面要不buildTypes读取不到signingConfigs会报错
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```

### 生成发行 APK 包

只需在终端中运行以下命令：

```js
cd android
./gradlew assembleRelease
```

生成的 APK 文件位于 android/app/build/outputs/apk/release/app-release.apk，它已经可以用来发布了。

## 路由

目前为止已经能够在手机上安装并运行自己开发的 APP 了，但是只有一个页面啊。虽然可以在一个页面里写多个组件然后条件判断渲染出多个页面的效果，但总归不是长久之计。于是就是开始学习路由啦。

1、通过命令 `npm i react-navigation`、`npm i react-native-gesture-handler`安装包。
2、通过命令`react-native link react-native-gesture-handler`链接依赖。
3、在根目录创建路由文件夹`navigators`，并在里面创建路由文件`AppNavigators.js`如下。

```js
import { createStackNavigator } from 'react-navigation';
// import React, { Component } from 'react';
// import { Text, View, Image } from 'react-native';
import HomePage from '../views/HomePage';
import Calculation from '../views/Calculation';
import Settlement from '../views/Settlement';
// import Page3 from '../views/Page3';
// import Page4 from '../views/Page4';
// import Page5 from '../views/Page5';
export const AppStackNavigator = createStackNavigator({
  HomePage: {
    screen: HomePage
  },
  Calculation: {
    screen: Calculation
  },
  Settlement: {
    screen: Settlement
  }
  // Page2: {
  //   screen: Page2,
  //   navigationOptions: {
  //     title: `这是一个页面2`
  //   }
  // },
  // Page3: {
  //   screen: Page3,
  //   navigationOptions: ({ props }) => {
  //     const { navigation } = props;
  //     const { state, setParams } = navigation;
  //     const { params } = state;
  //     return { title: params.title ? params.title : 'this is page3', headerRight: <Text>123 </Text> };
  //   }
  // }
});
```

## 开发时的问题

1、不能写 css 文件，需要在 js 中以对象的形式来描述 css，但是没有代码提示。
解决方案：添加一个中间文件来处理。

```js
import { StyleSheet as RnStyleSheet, ViewStyle, TextStyle, ImageStyle } from 'react-native';
type StyleProps = Partial<ViewStyle | TextStyle | ImageStyle>;
export const StyleSheet = {
  create(styles: { [className: string]: StyleProps }) {
    return RnStyleSheet.create(styles);
  }
};
```

引入这个文件就有代码提示了。

```js
import { StyleSheet } from './utils/utils.js';
const styles = StyleSheet.create({
    ...
});
```

2、 把组件放入目录中引入会报错`The development server returned response error code: 500`。
解决方案：组件放在根目录（感觉只是临时解决）。

3、重新创建 react native 项目后，gradle 可能更新，下载很慢。
解决方案：1、科学上网。2、安装你原来能够运行的 react native 版本。`react-native init demo --verbose --version 0.59.4`

4、更换图标后安装程序，手机桌面图标修改成功，打开后台程序图标还是之前的没有变。
解决方案：因为缓存问题，重新下手机就好了。

## 参考资料

[React Native 中文网](https://reactnative.cn/)
