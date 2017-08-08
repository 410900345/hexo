---
title: codepush使用
categories: 'ios,技巧,tools,js,原理,iphone,小技巧<!--选一个-->'
date: 2017-08-07 14:09:18
tags:
---

<!--{% qnimg alfred.png title:配置 alt:preferrence 'class:class1 class2' extend:?imageView2/2/w/1400 %}-->

### 简介

CodePush是提供给 React Native 和 Cordova 开发者直接部署移动应用更新给用户设备的云服务。CodePush 作为一个中央仓库，开发者可以推送更新到 (JS, HTML, CSS and images)，应用可以从客户端 SDKs 里面查询更新。CodePush 可以让应用有更多的可确定性，也可以让你直接接触用户群。在修复一些小问题和添加新特性的时候，不需要经过二进制打包，可以直接推送代码进行实时更新。

[codepush官方地址](https://github.com/Microsoft/code-push)

[文档](https://microsoft.github.io/code-push/docs/react-native.html#link-9)

### 安装说明

安装

```
npm install -g code-push-cli
```

注册账号/登录（Register/Login,命令还是会自动打开浏览器，复制这个Key(会等待一会)

```
code-push login
```

```
code-push access-key <command>
命令：
  add     添加一个新的Access Key
  remove  删除一个已经存在的Access key
  rm      删除一个已经存在的Access key
  list    列出与你账户关联的所有Access key
  ls      列出与你账户关联的所有Access key
```

创建新的app,安卓和ios分别建立对应app

```
code-push app add <AppName>
示例：
    code-push app add AppDemo
```

其它命令：

```
code-push app <command>
命令：
  add       创建一个新的App
  remove    删除App
  rm        删除App
  rename    重命名已经存在App
  list      列出与你账户关联的所有App
  ls        列出与你账户关联的所有App
  transfer  将一个App的所有权转让给另一个帐户

```

## 部署app

列出App中所有部署

```
code-push deployment ls <appName> [--format <format>] [--displayKeys]
选项：
  --format           终端打印格式 ("json" or "table")  [string] [默认值: "table"]
  --displayKeys, -k  是否显示Deployment Key  [boolean] [默认值: false]
示例：
  code-push deployment ls MyApp 
  code-push deployment ls MyApp --format json
```

发布（Release）

- 第一步

```
## 创建文件夹打包路径文件夹 
mkdir ios/bundle android/bundle

## ios的路径
react-native bundle --entry-file index.ios.js  --bundle-output ios/bundle/main.jsbundle

## android的路径
react-native bundle --entry-file index.android.js  --bundle-output android/bundle/main.jsbundle

```

- 第二步

```
code-push release FindFood-ios -d Production ios/bundle/main.jsbundle 1.0.0

code-push release FindFood-android -d Production android/bundle/main.jsbundle 1.0.0

```
解释

```
code-push release-react
Usage: code-push release-react <appName> <platform> [options]

Options:
  --bundleName, -b           Name of the generated JS bundle file. If unspecified, the standard bundle name will be used, depending on the specified platform: "main.jsbundle" (iOS) and "index.android.bundle" (Android)  [string] [default: null]
  --deploymentName, -d       Deployment to release the update to  [string] [default: "Staging"]
  --description, --des       Description of the changes made to the app with this release  [string] [default: null]
  --development, --dev       Specifies whether to generate a dev or release build  [boolean] [default: false]
  --disabled, -x             Specifies whether this release should be immediately downloadable  [boolean] [default: false]
  --entryFile, -e            Path to the app's entry Javascript file. If omitted, "index.<platform>.js" and then "index.js" will be used (if they exist)  [string] [default: null]
  --mandatory, -m            Specifies whether this release should be considered mandatory  [boolean] [default: false]
  --rollout, -r              Percentage of users this release should be immediately available to  [string] [default: "100%"]
  --sourcemapOutput, -s      Path to where the sourcemap for the resulting bundle should be written. If omitted, a sourcemap will not be generated.  [string] [default: null]
  --targetBinaryVersion, -t  Semver expression that specifies the binary app version(s) this release is targetting (e.g. 1.1.0, ~1.2.3). If omitted, the release will target the exact version specified in the "Info.plist" (iOS) or "build.gradle" (Android) files.  [string] [default: null]

Examples:
  release-react MyApp ios                    Releases the React Native iOS project in the current working directory to the "MyApp" app's "Staging" deployment
  release-react MyApp android -d Production  Releases the React Native Android project in the current working directory to the "MyApp" app's "Production" deployment
```

查看发布历史

```
code-push deployment history FindFood-ios Production
code-push deployment history FindFood-ios Staging
```

[参考地址](http://www.cnblogs.com/rayshen/p/5502538.html)