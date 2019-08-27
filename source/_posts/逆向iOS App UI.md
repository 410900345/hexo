---
title: 逆向iOS App UI
date: 2018-09-19 15:41:48
categories: 'ios'
tags:
---
### 环境准备
* iOS8.4越狱手机 iphone5s.版本不能太高，检查手机是否可以越狱[http://jailbreak.25pp.com/ios](http://jailbreak.25pp.com/ios).
* Reveal版本：Reveal4破解版,[下载地址](http://xclient.info/s/reveal.html?t=8aec8cdb98515fa0fac961a20fac00045ea18128)
* 盘古越狱助手 win,[下载](http://www.pangu.io/),还有 pp 助手之类的越狱工具,[越狱教程](http://jailbreak.25pp.com/ppjailbreak/?from=25pp_00119)

### 操作步骤

* 在Cydia中搜索并安装Reveal Loader,下载安装
![](http://7xooko.com1.z0.glb.clouddn.com/2016-07-27-Snip20160727_11.png)

* 在Reveal Help->Show Reveal Library in Finder->ios Library找到RevealServer.framework，然后打开RevealServer.framework找到里面的RevealServer文件,拷贝到外面修改名字为`libReveal.dylib`
![](http://7xooko.com1.z0.glb.clouddn.com/reveal/show-reveal-library-in-finder.jpg)

* 下载 pp 助手,工具->设备(5s)->文件管理->文件系统-> Library-> RHRevealLoader,没有的话新建一个`RHRevealLoader`文件夹,拷贝上的`libReveal.dylib`到这个`RHRevealLoader`目录下
* 重启手机，关闭电脑的Reveal重新打开。然后在手机->设置->Reveal->Enabled Applications->微信,里面打开你需要调试的APP，然后打开对应的APP就可以进行UI调
![](http://7xooko.com1.z0.glb.clouddn.com/2016-07-27-Snip20160727_8.png)

* 打开Reveal显示出来正在调试的 app, 就可以查看页面内容了
![](http://7xooko.com1.z0.glb.clouddn.com/2016-07-27-Snip20160727_10.png)

###  在Cydia中安装OpenSSH工具,
USB连接步骤:

* 终端中输入
	
```
brew install usbmuxd
```
	
如果你没有安装brew的话，那需要先执行
	
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

然后新开个终端输入
	
```
iproxy 4567 22
```
	
以上命令是把当前连接设备的22端口映射到电脑的4567端口上，继而来连接SSH,插上手机后另开终端输入,初始密码是`alpine`!!!! (可以在Cydia的软件OpenSSH查看到 OPenSSH Access How-to 点击进去后在底部可以看到)
	
```
ssh -p 4567 root@127.0.0.1
```

---------
[使用Reveal分析别人App的UI布局](http://chaosky.me/2016/07/27/iOS-Security-Defense-Reveal/)

[SSH连接iPhone(Wifi和USB)](https://www.jianshu.com/p/bf69cefc5f39)

[Cycript使用简介](https://www.jianshu.com/p/c93f5c3f1c7a)

<!--{% qnimg alfred.png title:配置 alt:preferrence 'class:class1 class2' extend:?imageView2/2/w/1400 %}-->