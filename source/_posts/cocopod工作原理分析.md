---
title: Cocopod工作原理分析
categories: '原理'
date: 2016-08-27 13:58:30
tags:
---

## Cocoapods 的工作流程
#### pod install 执行流程可分为如下五个步骤:

1.查看 ~/.cocoapods/repo/master/Specs 是否存在;

2.存在，从这个本地三方库信息库中获取 Podfile 中对应三方库的 git 地址;

3.不存在，输出 Setting up CocoaPods Master repo，并拉取三方库信息库到 ~/.cocoapods/repo/中.[Master repo地址](https://github.com/cocoapods/Specs);

4.使用 git 命令从 GitHub 上拉取 Podfile 中对应的三方库源码;

cd 进了 Alamofire 文件夹,里面都是release 版本号,当我们使用 pod search Alamofire 命令时会将这里的所有版本号输出出来。到最新版本号里面是一个 Alamofire.podspec.json 文件,可以看到这里包含了所有的三方库的相关信息，包括名字，协议，描述，Github 地址，支持平台等。

```
{
"name": "Alamofire",
  "version": "4.0.0",
  "license": "MIT",
  "summary": "Elegant HTTP Networking in Swift",
  "homepage": "https://github.com/Alamofire/Alamofire",
  "social_media_url": "http://twitter.com/AlamofireSF",
  "authors": {
    "Alamofire Software Foundation": "info@alamofire.org"
  },
  "source": {
    "git": "https://github.com/Alamofire/Alamofire.git",
    "tag": "4.0.0"
  },
  "platforms": {
    "ios": "8.0",
    "osx": "10.9",
    "tvos": "9.0",
    "watchos": "2.0"
  },
  "source_files": "Source/*.swift"
}
```
在查找到对应文件夹后，进行 json 数据解析，获得三方库的 repo 地址，调用本地 git 命令拉取源码，拉取完成后调用本地 xcodebuild 命令把三方库编译为 Framework。

#### pod setup 设置pod仓库,执行流程可分为如下步骤:
1.判断 ~/.cocoapods/repo目录是否存在

2.存在，依次调用 set_master_repo_url，set_master_repo_branch，update_master_repo 三个函数分别设置 repo 主分支地址，git checkout 到主分支，拉取主分支代码，更新repo

3.不存在，添加主分支 repo

#### Podfile.lock

这是 CocoaPods 创建的最重要的文件之一。它记录了需要被安装的 pod 的每个已安装的版本。如果你想知道已安装的 pod 是哪个版本，可以查看这个文件。推荐将 Podfile.lock 文件加入到版本控制中，这有助于整个团队的一致性。

#### 使用技巧
1.若 Podfile 中指定 Alamofire 的版本号为 4.2.0,但本地 ~/cocoapods/repo/master/Specs/Alamofire 中并没有此版本号，此时使用 pod install --no-repo-update 会出现错误;
2.我们便可以手动在 ~./cocoapods/repo/master/Specs 中添加我们需要的三方库版本信息，避免了把所有的并没有使用到的三方库信息更新到本地。
3.这样可以避免更新的内容过大就会,等待很久。

#### 原理和说明

1、第三方库会被编译成.a静态库供我们真正的工程使用。
CocoaPods会将所有的第三方库以target的方式组成一个名为Pods的工程，该工程就放在刚才新生成的Pods目录下。整个第三方库工程会生成一个名称为libPods.a的静态库提供给我们自己的CocoaPodsTest工程使用。
对于资源文件，CocoaPods提供了一个名为Pods-resources.sh的bash脚本，该脚本在每次项目编译的时候都会执行，将第三方库的各种资源文件复制到目标目录中

2、CocoaPods通过一个名为Pods.xcconfig的文件来在编译时设置所有的依赖和参数,tagert配置文件