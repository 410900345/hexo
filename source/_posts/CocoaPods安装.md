---
title: iOS CocoaPods安装使用错误记录
date: 2016-08-02 16:40:33
tags:
  [tools,效率]
categories: "tools"
---
# 1.gem install cocoapods

```
ERROR:  While executing gem ... (Errno::EPERM)
Operation not permitted - /usr/bin/pod
```
用下面命名安装

```
sudo gem install -n /usr/local/bin cocoapods
```
    
# 2.更换更新数据源国内镜像,每天都更新[code.net](https://git.coding.net/CocoaPods/Specs.git)

```
pod repo remove master
pod repo add master https://git.coding.net/CocoaPods/Specs.git    
pod setup
```

安装自己的私有仓库pod

```
pod repo add sdkMaster https://gitlab.coding.net/Specs.git
```

# 3.常用更新安装命名,不进行本地库更新

更新pod

	pod update --verbose --no-repo-update 

安装pod命令

	pod install --verbose --no-repo-update

# 4 安装和卸载pod
   
```   
sudo gem uninstall cocoapods  卸载
sudo gem install cocoapods    指定版本追加(-v 0.39) 安装
```
# 4 pod错误
ocoapods: Failed to connect to GitHub to update the CocoaPods/Specs specs repo

更新pod和ruby

```
brew install ruby
sudo gem install cocoapods
```
[stackoverflow](https://stackoverflow.com/questions/38993527/cocoapods-failed-to-connect-to-github-to-update-the-cocoapods-specs-specs-repo)

