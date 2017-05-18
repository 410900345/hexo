---
title: Atom+Nuclide开发工具(React Native)
categories: 'tools'
date: 2016-07-27 11:48:30
tags:
---

## 安装环境
### 1.安装atom [https://atom.io/](https://atom.io/),下载最新版本.
### 2.Nuclide常规安装

Nuclide项目官方地址:[https://github.com/facebook/nuclide](https://github.com/facebook/nuclide)

点击Atom->Preferences打开Setting,然后点击install，输入nuclide搜索，进行下载即可

`上面安装方式比较慢,更推荐源码安装`:

```
git clone  https://github.com/facebook/nuclide.git
cd  nuclide
npm install
apm link 
```

### 3.Nuclide常规配置

#### 1.搜索“nuclide”，点击“Settings”
选中:intall recommmended packages on startup
关闭 Atom ,重新打开.
#### 2.安装watchman 和 flow

```
brew install watchman
brew install flow
npm install fbjs
```

如果安装过，可以更新一下

```
brew upgrade watchman
brew upgrade flow
```

#### 3.常用插件
禁用自带的`nuclide-format-js`

下载格式化https://atom.io/packages/atom-beautify
jsx里面开启

消除atom 中间的线设置里面的atom->stylesheet添加下面代码

```
atom-text-editor::shadow .wrap-guide {
  visibility: hidden;
}
```


--------
[参考1](http://www.lcode.org/%E3%80%90react-native%E5%BC%80%E5%8F%91%E3%80%91react-native%E5%BC%80%E5%8F%91ide%E5%AE%89%E8%A3%85%E5%8F%8A%E9%85%8D%E7%BD%AE/)

[参考2](http://www.hangge.com/blog/cache/detail_1490.html#)