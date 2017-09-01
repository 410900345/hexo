---
title: auto layout VFL规则
categories: 'ios'
date: 2017-09-01 16:12:40
tags:
---

### 1.NSLayoutConstraint API

```
NSLayoutConstraint
+ (NSArray *)constraintsWithVisualFormat:(NSString *)format options:(NSLayoutFormatOptions)opts
metrics:(NSDictionary *)metrics
views:(NSDictionary *)views;
```

参数介绍:

format:此参数为你的vfl语句，比如:@"H:|-[button]-|"

opts:枚举参数，默认写0，具体跟据你所实现的需求去选择你想要的枚举

metrics:这里是一个字典，当在format中使用了动态数据比如上现这句:@"H:|-[button(==width)]-|",表示这个button的宽度为width,那么这个参数去哪里找呢？就是在这个字典里面找到key对就的值，如果没有找到这个值，app就会crash.

views:顾名思义，这是传所有你在vfl中使用到的view，那在上面这句例子中的应该怎么传呢？结果是这样的：NSDictionaryOfVariableBindings(button).如果你使用到了多个view，就可以这样NSDictionaryOfVariableBindings(button,button1,button3...),这个名字也要跟参数format中的一一对应，缺一不可.

### 2.举个栗子

```
NSArray *constraints1=[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-[button]-|"
　　　　　　　　　　　　　　　　　　　　　　　　　options:0
　　　　　　　　　　　　　　　　　　　　　　　　　metrics:nil
　　　　　　　　　　　　　　　　　　　　　　　　　views:NSDictionaryOfVariableBindings(button)];
```
说明
H:"是表示这是水平方向上的约束，

"|"是表示superView，

"-"表示一个间隔空间，这个间隔如果是如superView之间的，那么就是20px,如果是两个同级别的view，比如@"[button]-[button1]"，那么这里表示的是8px.

```
NSArray *constraints2=[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-20-[button(==30)]"
　　　　　　　　　　　　　　　　　　　　　　　　　options:0
　　　　　　　　　　　　　　　　　　　　　　　　　metrics:nil
　　　　　　　　　　　　　　　　　　　　　　　　　views:NSDictionaryOfVariableBindings(button)];
```
说明
V:"中代表这是垂直方向上的约束,

"|-20-"这里的意思就是距离头部为20px，相当于y坐标为20。

后面的"[button(==30)]"，是指定这个button的高度为30px.y坐标固定

### 3.总结
三：最后对格式的字符串作一个总结介绍

功能　　　　　　　　表达式

水平方向  　　　　　　  H:

垂直方向  　　　　　　  V:

Views　　　　　　　　 [view]

SuperView　　　　　　|

关系　　　　　　　　　>=,==,<=

空间,间隙　　　　　　　-

优先级　　　　　　　　@value

[参考地址](http://www.cnblogs.com/wupei/p/4150626.html)