---
title: iOS 9 - Keyboard 出现在 UIAlertView 不消失
date: 2016-10-01 17:56:13
tags:
categories: 'ios'
---
**今天遇见一个奇怪的bug,当我的UIAlertView 消失的时候键盘弹出来了,这个只出现在第一次安装的时候
万能的[stackoverflow](http://stackoverflow.com/questions/32744209/ios-9-keyboard-pops-up-after-uialertview-dismissed)上面有这个问题的一些解决方案:**

1.使用新的api,UIAlertController

```
UIAlertController *alertController = [UIAlertController alertControllerWithTitle:@"Alert Title!" message:@"This is an alert message." preferredStyle:UIAlertControllerStyleAlert]; 
UIAlertAction *ok = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault handler:nil]; 
[alertController addAction:ok];
[self presentViewController:alertController animated:NO completion:nil];
```

2.另外一个方法就是延迟调用一下alertView.

```	
@weakify(self);
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(0.6 *NSEC_PER_SEC)),dispatch_get_main_queue(), ^{
	@strongify(self);
	[self loadUpdateAPI]; 
});
```
    
3.另外一种注销键盘

{% codeblock lang:objc %}
[[UIApplication sharedApplication] sendAction:@selector(resignFirstResponder) to:nil from:nil forEvent:nil];
{% endcodeblock %}

** 出现的原因**
可能是键盘状态没有完全被收回,导致出现的

**如果有更好的方案可以告诉我**

