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
import HomePage from '../views/HomePage';
import Debug from '../views/Debug';

export const AppStackNavigator = createStackNavigator({
  HomePage: {
    screen: HomePage
  },//定义HomePage为首页路由
  Debug: {
    screen: Debug
  },//定义Debug为Debug页路由
});

});
```

4、 创建好路由文件，需要把入口改用路由文件。把根目录的 index 文件修改下。
原本的 index 文件：

```js
import { AppRegistry } from 'react-native';
import App from './App';
import { name as appName } from './app.json';

AppRegistry.registerComponent(appName, () => App); //把APP组件注册到APP
```

修改后的 index 文件：

```js
import { AppRegistry } from 'react-native';
import { createAppContainer } from 'react-navigation';
import { AppStackNavigator } from './navigators/AppNavigators';
import { name as appName } from './app.json';
const AppStackNavigatorContainer = createAppContainer(AppStackNavigator); //用路由文件创建APP控制器
AppRegistry.registerComponent(appName, () => AppStackNavigatorContainer); //把路由控制器注册到APP
```

5、这样在组件里就能够使用路由进行跳转了。

```js
//通过props获取navication
const { navigation } = this.props;
//跳转的Debug组件页面
navigation.navigate('Debug');
//跳转页面并传值
navigation.navigate('Debug', { value: '测试传值' });
```

```js
//拿到其他页面传来的值
const { value } = this.props.navigation.state.params;
console.log(value); //测试传值
```

## 持久化存储

由于希望做一个历史记录页面，所以想存一些数据在本地，像 web 的 storage 一样。

### AsyncStorage

AsyncStorage 是 react native 提供的轻量级数据持久化方案，类似于 web 端的 storage。
由于 api 过于复杂一般需要封装，这里使用常用封装好的第三方库`react-native-storage`。
1、安装包`react-native-storage`
2、在首页组件引入包->设置 storage 默认值->将它赋值给全局方面使用。

```js
import Storage from 'react-native-storage';
var storage = new Storage({
  size: 1000, //最大容量，默认值1000条数据循环存储
  storageBackend: AsyncStorage, //存储引擎：RN使用AsyncStorage，如果不指定则数据只会保存在内存中，重启后即丢失
  defaultExpires: null, //数据过期时间，默认一整天（1000 * 3600 * 24 毫秒），设为null则永不过期
  enableCache: true //读写时在内存中缓存数据，默认开启
});
global.storage = storage; //将storage保存到全局，方便各个组件里面使用
```

3、使用 storage

```js
//存值，因为在全局保存了storage，所以直接调用storage.save()以键值对存储数据，data可以是任意类型值
global.storage.save({
  key: 'testKey', // 注意:请不要在key中使用_下划线符号!
  data: '测试存值'
});
//获取数据，这里获取值是异步的。
global.storage.getAllDataForKey('testKey').then(data => {
  console.log(data); //测试存值
});
//存储一个数组
global.storage.save({
  key: 'testKeyArr', // 注意:请不要在key中使用_下划线符号!
  id: '1', // 注意:请不要在id中使用_下划线符号!
  data: '测试存值'
});
//读取值
global.storage.getAllDataForKey('testKeyArr').then(data => {
  console.log(data); //['测试存值']
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
