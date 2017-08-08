---
title: andriod打包相关
categories: 'ios,技巧,tools,js,原理,iphone,小技巧<!--选一个-->'
date: 2017-08-08 11:34:21
tags:
---

### 简介
http://localhost:8081/index.android.bundle?platform=android；当应用启动运行的时候，会自动拉取这个bundle文件，该文件里存放的是应用的全部逻辑代码，在目录中并不存在这个文件，事实上，这个地址只是一个请求地址，而非真正的静态资源文件，是通过包服务器packager通过动态分析index.android.js中的依赖，并对其进行合并得到的，而且该服务允许代码实时渲染。

### 具体步骤
- 1.生成一个签名密钥

```
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```
最后它会生成一个叫做my-release-key.keystore的密钥库文件

- 2.找到路径/android/app/src/main，并在该目录下新建assets文件夹

- 3.在工程目录下将index.android.bundle下载并保存到assets资源文件夹中

```
curl -k "http://localhost:8081/index.android.bundle" > android/app/src/main/assets/index.android.bundle
```

这句命令是重点，如果assets目录中不存在该文件，则打包的apk在执行时显示空白。

`注意`
Protocol 'http not supported or disabled in libcurl
Windows下安装使用curl命令:http://jingyan.baidu.com/article/a681b0dec4c67a3b1943467c.html

- 4.添加gradle的android keystore配置

打包的apk在未签名的情况下,在手机中（非root）是不允许安装的

在build.gradle文件中

//签名
 
```
signingConfigs{ release { storeFile file("/my-release-key.keystore") storePassword "密码" keyAlias "keyAlias的名字" keyPassword "密码" } } buildTypes { release { minifyEnabled false proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro' signingConfig signingConfigs.release //添加这句话引用签名配置 } }
```

- 5.启用Proguard代码混淆来缩小APK文件的大小

Proguard是一个Java字节码混淆压缩工具，它可以移除掉React Native Java（和它的依赖库中）中没有被使用到的部分，最终有效的减少APK的大小。

重要：启用Proguard之后，你必须再次全面地测试你的应用。Proguard有时候需要为你引入的每个原生库做一些额外的配置。参见app/proguard-rules.pro文件。

```
def enableProguardInReleaseBuilds = true
```

- 6.在/android/目录中执行`gradle assembleRelease`命令，打包后的文件在 android/app/build/outputs/apk目录中，例如app-release.apk。如果打包碰到问题可以先执行 gradle clean 清理一下。

- 7.将apk发布到各大应用市场（BUILD SUCCESSFUL）
 
- 8.mac环境变量配置path
找到 `~/.bash_profile`添加,检查一下对应的gradle信息保证存在

```
export GRADLE_HOME=/Applications/Android\ Studio.app/Contents/gradle/gradle-3.3
export PATH=${PATH}:${GRADLE_HOME}/bin
```

![相应图片](http://img.blog.csdn.net/20160411123958780)

退出编辑,执行下面命名生效

```
source .bash_profile
```
配置完成之后，运行gradle -v，检查一下是否安装无误

如果权限不够

```
chmod  gradle.bat
```

[参考地址](http://blog.csdn.net/u013424496/article/details/52684213)