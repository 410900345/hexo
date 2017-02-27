---
title: 创建自己Carthage支持的库(二)
categories: 'tools'
date: 2016-12-01 17:34:32
tags:
---

## 创建自己Carthage支持的库
### 首先创建一个framework
1.选择你的工程

2.选择framework所在的Target

3.选择Build Phases

4.点击Header左下角的+号把你要暴露的头文件添加到Public里面（默认添加到Project里面，用鼠标把它拽过去）

5.在Compile source里面添加实现的.m文件
### 在framework的BuildSettings的Packaging里面,把Produce Module Name 和 Produce Name改成想要的名字XXXX
1.如果你使用了类别,那么你需要在Build Settings的Linking的Other Linker Flags里加上-all_load

2.如果你想你的工程支持bitcode,需要在Other C Flags 里加上-fembed-bitcode

3.选择 Manager Schemes,勾上shared(这样Carthage就可以编译你的工程)

4.cd到项目文件夹,运行

```
$ carthage build --no-skip-current
```
命令运行完成后,你会发现你的项目文件夹里面多了一个Carthage文件夹`Carthage->Build->iOS->xxxx.framework!`
### 要给别人使用的话你还需要最后一步,给你的工程打上tag,push上去
在Cartfile文件添加,

```
github "yourname/xxxx" "master"
```
然后运行下面代码更新,frmework

```
carthage update
```



## `参考连接`

创建自己的[Cartfile支持的库](http://blog.csdn.net/ruglcc/article/details/53725251)