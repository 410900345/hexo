---
title: ReactNative错误收集问题
categories: 'BFE'
date: 2016-12-15 10:47:26
tags:
---

## 错误一:Unable to resolve module image!
方法:	在 Xcode 下 Images.xcassets 里面明确的有这个图片。

## 错误二:低版本兼容,Log类接口修改, 添加 RCTLogSource source 即可.
	
	RCTSetLogFunction(^(RCTLogLevel level, RCTLogSource source, NSString *fileName, NSNumber *lineNumber, NSString *message)

## 错误三:RCTSRWebSocket.m报错,代码在下面

	SecRandomCopyBytes(kSecRandomDefault, sizeof(uint32_t), (uint8_t *)mask_key);
修改为:
	
	(void)SecRandomCopyBytes(kSecRandomDefault, sizeof(uint32_t), (uint8_t *)mask_key);	

## 错误四: Seem you're trying to access 'ReactNative.createClass' from the 'react-native package;

	var React = require('react');
	var component = React.createClass();

RN升级导致的问题,官方[解决](http://bbs.reactnative.cn/topic/1857/seems-you-re-trying-to-access-reactnative-createclass/7)
##错误五:重新安装sdk,react@15.3.1是sdk版本

```	
watchman watch-del-all
rm -rf node_modules
npm install react@15.3.1 --save
npm install
rm -fr $TMPDIR/react-*
npm start -- --reset-cache	
```		
##错误六:错误是下面提示
方法:other flag 添加标识 -lc++ 

```
Undefined symbols for architecture x86_64:
  "std::__1::__next_prime(unsigned long)", referenced from:
      std::__1::__hash_table<std::__1::__hash_value_type<unsigned long, unsigned long>, std::__1::__unordered_map_hasher<unsigned long, std::__1::__hash_value_type<unsigned long, unsigned long>, std::__1::hash<unsigned long>, true>, std::__1::__unordered_map_equal<unsigned long, std::__1::__hash_value_type<unsigned long, unsigned long>, std::__1::equal_to<unsigned long>, true>, std::__1::allocator<std::__1::__hash_value_type<unsigned long, unsigned long> > >::rehash(unsigned long) in libReact.a(RCTJSCExecutor.o)
  "std::__1::mutex::lock()", referenced from:
      -[RCTModuleData setUpInstanceAndBridge] in libReact.a(RCTModuleData.o)
  "std::__1::mutex::unlock()", referenced from:
      -[RCTModuleData setUpInstanceAndBridge] in libReact.a(RCTModuleData.o)
  "std::__1::mutex::~mutex()", referenced from:
      -[RCTModuleData .cxx_destruct] in libReact.a(RCTModuleData.o)
  "std::terminate()", referenced from:
      ___clang_call_terminate in libReact.a(RCTJSCExecutor.o)
  "operator delete[](void*)", referenced from:
      -[RCTJSCExecutor dealloc] in libReact.a(RCTJSCExecutor.o)
      executeRandomAccessModule(RCTJSCExecutor*, unsigned int, unsigned long, unsigned long) in libReact.a(RCTJSCExecutor.o)
      readRAMBundle(std::__1::unique_ptr<__sFILE, int (*)(__sFILE*)>, RandomAccessBundleData&) in libReact.a(RCTJSCExecutor.o)
.....
.....
  "___cxa_begin_catch", referenced from:
      ___clang_call_terminate in libReact.a(RCTJSCExecutor.o)
  "___gxx_personality_v0", referenced from:
      -[RCTJavaScriptContext initWithJSContext:onThread:] in libReact.a(RCTJSCExecutor.o)
      -[RCTJavaScriptContext init] in libReact.a(RCTJSCExecutor.o)
      -[RCTJavaScriptContext invalidate] in libReact.a(RCTJSCExecutor.o)
      +[RCTJSCExecutor runRunLoopThread] in libReact.a(RCTJSCExecutor.o)
      -[RCTJSCExecutor setBridge:] in libReact.a(RCTJSCExecutor.o)
      -[RCTJSCExecutor init] in libReact.a(RCTJSCExecutor.o)
      -[RCTJSCExecutor initWithUseCustomJSCLibrary:] in libReact.a(RCTJSCExecutor.o)
      ...
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```
##错误七: React Native cant find RCTEventEmitter after cocoapods integration 

解决方法:

* cleaning xcode under Product menu cmd + K 
* clearing rm ios/build/* 
* react-native unlink 
* src/ios $ pod clean && pod deintegrate && pod install