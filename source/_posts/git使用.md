---
title: git使用技巧
categories: 'tools'
date: 2017-02-20 09:55:28
tags:
---
### ssh-key的作用
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



