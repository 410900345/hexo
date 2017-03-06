---
title: git使用技巧
categories: 'tools'
date: 2016-07-20 09:55:28
tags:
---
## ssh-key的作用
我们使用ssh登录服务器时，一般常见的会使用用户名/密码方式登录，
也可以使用ssh key实行免密码登录，一般现在这种方式被Git服务器使用的比较多。
## 解决本地多个ssh-key的配置
1.生成不同的密钥,ssh会根据登陆不同的域来读取相应的私钥文件

```
ssh-keygen -t rsa -f ~/.ssh/id_rsa.work -C "Key for Work"  
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "Key for GitHub"  

```
在 `~/.ssh/config` 目录内修改文件config

```
Host *.workdomain.com   
  
    IdentityFile ~/.ssh/id_rsa.work  
    User lee  
   
Host github.com  
    IdentityFile ~/.ssh/id_rsa.github  
    User git  
```
用下面的命令测试一下

```
ssh -T git@github.com
```

返回成功

```
Hi sukeyang! You've successfully authenticated, but GitHub does not provide shell access.
```
* 1.提示 WARNING: UNPROTECTED PRIVATE KEY FILE!  

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/Users/yangshuo/.ssh/winid_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
```
解决办法：在命令行输入chmod 700 id_rsa.github即可。这里“id_rsa.githu”就是warning里给出的密钥文件名。
* 2.报错No submodule mapping found in .gitmodules for path;

```
git submodule status
git rm --cached Classes/lib/AFKissXMLRequestOperation
```
查看状态,Classes/lib/AFKissXMLRequestOperation
为要删除的路径,然后就oK了.
* 3.多帐号github配置
生成第二个ssh key,并按上面的方法进行测试

```
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "Key for GitHub"
```
修改在.ssh/下创建config文件 内容如下：

```
Host github.com  
    HostName github.com  
    IdentityFile ~/.ssh/id_rsa  
  
Host my.github.com  
    HostName github.com  
    IdentityFile ~/.ssh/my  
```
进行验证

```
ssh -T git@my.github.com
```
打开.Git/config文件,修改下面url地址就可以了

```
#更改[remote "origin"]项中的url中的  
#my.github.com 对应上面配置的host  
[remote "origin"]  
    url = git@my.github.com:itmyline/blog.git  
```