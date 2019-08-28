---
title: 空间不足,清理Mac空间
categories: '小技巧'
date: 2018-04-10 09:34:18
tags:
---

笔者使用的MacBook,空间只有128G,由于安装了Xcode和 Android studio 经常由于空间不足,导致项目无法进行编译.推荐使用下面软件进行整理.

* [OmniDiskSweeper](https://www.omnigroup.com/more)查看空间占用并清理
* [CleanMyMac 3.9.4](http://xclient.info/s/cleanmymac.html?t=3e085124bbdd0183f927b846e6f380562291aace)强大的mac系统清理工具

### 针对性的大文件删除

* `~/Library/Developer/Xcode/DerivedData/`

Xcode编译时的文件缓存,build的信息等都会保存在这里,删除后在下次打开项目编译的时候将会重新生成,可以全部删掉.

* `~/Library/Developer/Xcode/iOS DeviceSupport/`

Xcode支持的真机测试对应的版本文件,真机调试的时候会自动关联生成,删掉比较老的版本文件,低于11.3版本的文件夹.

<!-- more -->

* `~/Library/Developer/Xcode/Archives/`

Xcode打包的文件dSYM等内容,保留上线版本,如果使用第三方的 bug 管理工具如 Bugly 会自动上传,可以根据情况删掉文件.

* `~/Library/Developer/CoreSimulator/Devices/`

模拟器上的APP数据,重置模拟器会删掉相应的文件,可以按时间进行排序,然后删掉比较老的文件,或者直接全部删掉,编译运行会再次重新安装 APP.

[参考地址](https://www.iwangke.me/2013/09/09/clean-xcode-to-free-up-disk-space/)
