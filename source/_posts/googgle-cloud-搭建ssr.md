---
title: googgle cloud 搭建ssr 免费使用一年
categories: 'tools'
date: 2017-10-26 10:21:24
tags:
---

由于最近翻墙困难,各种免费ss帐号也不靠谱,所以选择google cloud自己搭建梯子!

## 一.准备条件
* 能访问[google cloud](https://cloud.google.com/),和创建google帐号.
* 有一张Visa、Master等美元支付信用卡（会冻结$1),按照要求填写信用卡信息,本人交行visa信用卡,直接成功,(注册成功后风控人员还打了电话回访)
![google cloud](https://suiyuanjian.com/wp-content/uploads/2017/08/%E4%BD%BF%E7%94%A8google-cloud-platformgcp-gce%E5%AE%89%E8%A3%85ssrbbr%E6%95%99%E7%A8%8B-1.jpg)

## 二.具体步骤
### 1.创建实例

点击菜单`产品与服务->计算引擎->VM实例->创建实例`,

* 名称随意,地区选择区建议选亚洲的（asia-east台湾、asia-northeast日本、asia-southeast新加坡）
* 机器类型把默认的3.75GB主机换成微型0.6GB的，搭建SS足够了，这样可以把主机月使用费降低
* 映像建议选择Ubuntu 16.04.(CentOS 7也可以，但是我用了之后有问题，后文会提到）
* 防火墙：允许HTTP流量，允许HTTPS流量

<!-- more -->

![](http://raychinki.com/wp-content/uploads/2017/06/SSR_1.png)
* vm创建完成后，进入控制台-网络-外部IP地址，将vm分配的外部地址由临时改为静态,需要一个固定地址ip为ss访问
![](http://raychinki.com/wp-content/uploads/2017/06/SSR_2.png)

### 2.进入`控制台-vpc网络-防火墙规则`，允许tcp所有端口

* 创建防火墙规则（未提及的全部默认）：流量方向入站、来源ip地址0.0.0.0/0、协议和端口全部允许,允许协议和端口填tcp:1-65535; udp:1-65535
* 流量方向出站、来源ip地址0.0.0.0/0、协议和端口全部允许（注意要创建两次防火墙规则，一次出站，一次入站）,允许协议和端口填tcp:1-65535; udp:1-65535

![](http://raychinki.com/wp-content/uploads/2017/06/SSR_3.png)

### 3.配置SS以及BBR
进入控制台-计算引擎-VM实例，点击连接-SSH，在浏览器中可以直接打开控制台，并且支持复制粘贴
![](http://51.ruyo.net/wp-content/uploads/2016/09/8.png)

* 首先获得root权限，在SSH里输入

```
sudo -i
```

 
* 下面安装Google的开源TCP BBR拥塞控制算法[秋水逸冰的BBR一键安装脚本地址](https://teddysun.com/489.html)三行命令

```
wget –no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```
 
 可以使用下面命令校验

```
sysctl net.ipv4.tcp_available_congestion_control
```
 
 出现
 
```
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```
 
 类似含有bbr字样即成功。
 
* 安装[ShadowSocks脚本,秋水逸冰的四合一一键安装脚本](https://teddysun.com/489.html),三行命令
 
```
wget –no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```
 
选择SS版本（我这里选择的第二个，SSR，目前安全性最高），依次输入端口号和密码等,等待安装结束重启

### 4.配置SS和修改

将ShadowSocks服务加入自动重启,`很重要!` 

```
sudo vim /etc/rc.local
```
 
输入下面命令`exit 0`上面

```
sleep 10
/usr/bin/ssserver /etc/init.d/shadowsocks-r start
exit 0
```

输入完成后，ESC键后输入:wq，保存退出,SSH中输入reboot重启，如果SSR服务自动启动表明成功,

-----------

建立完成后,家里可以使用.单位链接不上?有知道的能否解答一下?


[站长工具 > Ping检测](http://ping.chinaz.com/)

[ShadowsocksX-NG官方地址](https://github.com/shadowsocks/ShadowsocksX-NG)

[参考链接1](http://raychinki.com/?p=1020)

[参考链接2](http://51.ruyo.net/p/2144.html)
