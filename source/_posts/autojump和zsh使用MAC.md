---
title: autojum和zsh使用MAC
categories: 'tools'
date: 2016-07-27 11:48:30
tags:
---

## 安装oh my zsh环境
### 1.安装wget [http://ftp.gnu.org/gnu/wget/](http://ftp.gnu.org/gnu/wget/),下载最新版本.
### 2.解压缩,cd到目录文件夹,依次执行命令

```
./configure --with-ssl=openssl
make
sudo make install
```
`备注:`出现错误

```
checking host system type... configure: error: can not guess host type; you must specify one  
```
执行下面的命令

```
./configure --with-ssl=openssl --host=TARGET 
```
### 3.自动安装

```
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```
或者手动安装

```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
成功后退出页面重新打开终端.

`备注:`如果没有变化可以执行切换

```
zsh
```

配置文件在`~/.zshrc`里面

### 4.切换shell

用如下命令切换shell: 

```
chsh -s /bin/zsh
```

重启terminal就好啦，应该就成功的从bash切换到zsh了:)

查看当前使用的shell

```
echo $SHELL 
```

如果你想看看自己的机子上装了哪些shell，可以使用如下命令：

```
cat /etc/shells
```

## 安装autojump

#### 1.执行命令自动安装
```
	brew install autojump
```
或者手动安装

```
wget https://github.com/downloads/joelthelion/autojump/autojump_v21.1.2.tar.gz
```
解压后进入目录,执行

```
./install.sh
```

最后把以下代码加入`~/.zshrc`：

```
[[ -s `brew --prefix`/etc/autojump.sh ]] && . `brew --prefix`/etc/autojump.sh
```

使用是

```
 j xxx文件夹
```

## 自定义设置
对RN的命名简化,在`~/.zshrc`里面最后添加

```
alias rna="react-native run-android"
alias rni="react-native run-ios"
```

以后就可以使用`rna ``rni `运行了

--------
[参考1](https://zhuanlan.zhihu.com/p/19556676?columnSlug=mactalk)

[参考2](http://blog.csdn.net/hejisan/article/details/50432993)