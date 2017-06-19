---
title: ReactNative错误收集(Andriod)
categories: 'BFE'
date: 2017-05-15 10:47:26
tags:
---

## 错误一:小米5进行程序调试 出现下面的问题
问题描述:

```
* What went wrong:
Execution failed for task ':app:installDebug'.
> com.android.builder.testing.api.DeviceException: com.android.ddmlib.InstallException: Failed to establish session

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.

BUILD FAILED
```

1.执行了一下 `adb devices` 命令的时候看到设备是否经连接上了。
2.在小米手机里面点`miui版本`打开开发者调试 ,然后再去设置`小米手机设置->开发者选项->启用MIUI优化关闭。

## 错误二:
```
jax$  react-native run-android
Starting JS server...
Building and installing the app on the device (cd android && ./gradlew installDebug...

Could not install the app on the device, read the error above for details.
```
执行下面的命令
chmod 755 android/gradlew
[facebook/react-native](https://github.com/facebook/react-native/issues/8868#issuecomment-303320822)

## 错误三:zsh: command not found: adb

1.解决办法
在`~/.zshrc`文件里面添加找到.zshrc文件 中“# User configuration” 位置加入 “source ~/.bash_profile”(前提是bash_profile文件中的环境变量 你已经各种配置好了)
2.重启命令行



------
