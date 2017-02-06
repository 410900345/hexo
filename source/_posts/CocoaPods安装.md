---
title: iOS CocoaPods安装使用错误记录
date: 2017-02-02 16:40:33
tags:
---
# 1.gem install cocoapods
	ERROR:  While executing gem ... (Errno::EPERM)
    Operation not permitted - /usr/bin/pod
    
  用下面命名安装
  <!-- more -->
    sudo gem install -n /usr/local/bin cocoapods
    
# 2.更换更新数据源国内镜像,每天都更新[code.net](https://git.coding.net/CocoaPods/Specs.git)

	pod repo remove master
	pod repo add master https://git.coding.net/CocoaPods/Specs.git    
	pod setup
	
# 3.常用更新安装命名,不进行本地库更新
更新
	
	pod update --verbose --no-repo-update 
安装
	
	pod install --verbose --no-repo-update
	
# 4 安装和卸载pod
    sudo gem uninstall cocoapods  卸载
    sudo gem install cocoapods    指定版本追加(-v 0.39) 安装


