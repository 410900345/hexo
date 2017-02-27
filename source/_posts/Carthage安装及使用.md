---
title: Carthage安装及使用(一)
categories: 'tools'
date: 2016-12-01 14:58:29
tags:
---
## 简介
Carthage 使用于 Swift 语言编写，只支持动态框架，只支持 iOS8+的Cocoa依赖管理工具。是一个去中心化的Cocoa依赖管理工具;
CocoaPods对原有工程破坏性大(建立workspace,增加一堆乱七八糟的文件),侵入性太强,耦合太高;

## 环境安装
检查ruby和brew版本

```
ruby -v
brew -v
```
如果电脑中没有Homebrew,终端执行脚本安装即可

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
方法1:更新brew,安装carthage

```
brew update
brew install carthage
```
方法2:下载安装[Carthage.pkg](https://github.com/Carthage/Carthage/releases)
## 常见命令使用

```
carthage version
brew upgrade carthage  //升级
sudo brew uninstall carthage  //卸载
```

创建空的Cartfile文件

```
touch Cartfile
```
打开Cartfile添加三方库信息,如

```
github "Alamofire/Alamofire" ~> 3.0
```
保存并关闭Cartfile文件并执行,`--platform iOS` 只是iOS平台

```
carthage update --platform iOS
```
引入设置Xcode自动搜索Framework的目录,Target—>Build Setting—>Framework Search Path—>添加路径下面

```
＂$(SRCROOT)/Carthage/Build/iOS＂
```
### 1.Cartfile.resolved (需要提交到 Git)
在执行 carthage update 命令后会在根目录创建一个 Cartfile.resolved 文件，这个文件是生成后的依赖关系，不能修改。

Cartfile.resolved 文件确保提交的项目可以使用完全相同的配置与方式运行启用。 跟踪项目当前所用的依赖版本号，保持多端开发一致,出于这个原因,强烈建议提交这个文件到版本控制中

### 2.自动生成的Carthage目录 (不需要提交到 Git)

Carthage文件夹用来存放:

carthage checkout 从git拉取的依赖库源文件(Checkouts)

carthage build编译后的文件(Build),包含Mac 与 iOS对应的.framework,文件夹用来存放依赖库的源文件和编译后的文件(不需要提交到 Git，可以修改.gitignore文件，增加忽略 Carthage 文件夹就行了：#Carthage Carthage）

