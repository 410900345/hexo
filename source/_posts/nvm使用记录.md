---
title: nvm使用记录
categories: 小技巧
date: 2017-07-09 10:38:46
tags:
---

nvm全称Node Version Manager.
解决问题:安装和管理多版本Node,适用于mac系统,官方地址[nvm](https://github.com/creationix/nvm)
widows下参考地址[nvm-windows](https://github.com/coreybutler/nvm-windows)

## 1.卸载已安装到全局的 node/npm

```
npm ls -g --depth=0 #查看已经安装在全局的模块，以便删除这些全局模块后再按照不同的 node 版本重新进行全局安装

sudo rm -rf /usr/local/lib/node_modules #删除全局 node_modules 目录
sudo rm /usr/local/bin/node #删除 node
cd  /usr/local/bin && ls -l | grep "../lib/node_modules/" | awk '{print $9}'| xargs rm #删除全局 node 模块注册的软链
```
其他删除指令
```
sudo rm /usr/local/bin/npm
sudo rm /usr/local/share/man/man1/node.1
sudo rm /usr/local/lib/dtrace/node.d
sudo rm -rf ~/.npm
sudo rm -rf ~/.node-gyp
sudo rm /opt/local/bin/node
sudo rm /opt/local/include/node
sudo rm -rf /opt/local/lib/node_modules

```
## 2.安装NVM（前提是你安装了homebrew）


```
$ brew install nvm 
```

```
$ nvm ls-remote 查看 所有的node可用版本
$ nvm install xxx 下载你想要的版本
$ nvm use xxx 使用指定版本的node 
$ nvm alias default xxx 每次启动终端都使用该版本的node 
```

```
npm install -g react-native-cli #安装 react-native-cli 模块至全局目录，安装完成的路径是 /Users/<你的用户名>/.nvm/versions/node/v4.2.2/lib/react-native-cli

npm install hexo-cli -g
```
## 3.查看安装结果
```
$ node -v
$ npm -v 
```
## 4.卸载nvm

```
$ rm -rf ~/.nvm
```

[参考地址1](http://taobaofed.org/blog/2015/11/17/nvm-or-n/)

[参考地址1](http://www.cnblogs.com/kaiye/p/4937191.html)