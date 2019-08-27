---
title: 逆向iOS App
date: 2019-07-19 15:41:48
categories: 'ios'
tags:
---
### 一.环境准备

- 苹果开发者，能真机联调app.
- 下载[MonkeyDev](https://github.com/AloneMonkey/MonkeyDev),一个可以直接debug的工程.
- 下载[Hopper Disassembler](https://www.waitsun.com/hopper-disassembler-4-2-0.html),反汇编工具,可以查看里面的伪代码看原来app实现逻辑.

### 二.操作步骤
- 在`TargetApp`里面放下载好的ipa,ipa可以从pp助手等越狱平台下载.

- 在`xxDylib.m`类里面写hook代码,这样可以进行断点debug内容.
在`target -> buildsettings -> 搜索user-defined` 可以修改一些选项,使用原来的bunldeid 等(逆向wx必须修改)

---------
[逆向大神的blog](http://www.alonemonkey.com/2017/07/12/monkeydev-without-jailbreak/)

[逆向大神的 MonkeyDevSpecs](https://github.com/AloneMonkey/MonkeyDevSpecs)