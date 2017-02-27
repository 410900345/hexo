---
title: AFN实现原理分析(2.x版本)
categories: '原理'
date: 2017-02-27 11:49:29
tags:
---

1. 使用AFHTTPSessionManager进行网络请求,类继承于AFURLSessionManager

```
AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
[manager GET:URL parameters:nil progress:nil success:^(NSURLSessionDataTask *_Nonnulltask, id _NullableresponseObject) {
  dispatch_async(dispatch_get_main_queue(), ^{
  //将子线程从网络拉取的数据用于主线程刷新视图
    });
  }failure:^(NSURLSessionDataTask*_Nullabletask,NSError*_Nonnullerror) {

}];
```
通过查看manager方法代码可以看到其实现最终是调用了父类AFURLSessionManager的initWithSessionConfiguration：方法，

设置了默认的json解析方式;

最大的并发操作数为1是让所有请求的发起和等待网络响应均在同一条线程中执行，而不用为每一个请求都新建一条线程，这样节约了很多资源;

默认安全策略是AFSSLPinningModeNone,

该方法代码片段如下

```
self.sessionConfiguration = configuration;
self.operationQueue = [[NSOperationQueue alloc] init];
self.operationQueue.maxConcurrentOperationCount = 1;
self.session = [NSURLSession sessionWithConfiguration:self.sessionConfiguration delegate:self delegateQueue:self.operationQueue];
self.responseSerializer = [AFJSONResponseSerializer serializer];
```
在响应到达后会执行AFURLSessionManager的NSURLSessionDataDelegate协议的方法，[AFURLSessioinManager URLSession:dataTask:didReceiveData:]用于查找对应的响应代理，并将后续的数据处理如数据拼接转交给该代理。该方法的实现代码如下：

```
AFURLSessionManagerTaskDelegate *delegate = [self delegateForTask:dataTask];
[delegate URLSession:session dataTask:dataTask didReceiveData:data];

if (self.dataTaskDidReceiveData) {
    self.dataTaskDidReceiveData(session, dataTask, data);
}
```
在数据比较大时，改方法可能会多次执行。

当数据传输完成后会调用[AFURLSessioinManager URLSession:task:didCompleteWithError],该方法用于让对应的代理执行NSURLSessionTaskDelegate协议中的方法，并将该代理对象从字典中移除，源代码如下：

```
AFURLSessionManagerTaskDelegate *delegate = [self delegateForTask:task];

// delegate may be nil when completing a task in the background
if (delegate) {
    [delegate URLSession:session task:task didCompleteWithError:error];

    [self removeDelegateForTask:task];
}

if (self.taskDidComplete) {
    self.taskDidComplete(session, task, error);
}
```

随后代理执行URLSession:task:didCompleteWithError:，该方法把数据放到另一个由静态方法生成的url_session_manager_processing_queue操作队列中做数据解析，如json解析，并将解析后的数据回传到主线程或者你自己生成的操作队列里，通过通知中心将请求完成的消息传递到主线程去（后面会写一篇文章介绍通知中心的实现原理,并写一个类似的通知中心）。
该方法源码片段如下：

```
dispatch_async(url_session_manager_processing_queue(), ^{
            NSError *serializationError = nil;
            responseObject = [manager.responseSerializer responseObjectForResponse:task.response data:[NSData dataWithData:self.mutableData] error:&serializationError];

            dispatch_group_async(manager.completionGroup ?: url_session_manager_completion_group(), manager.completionQueue ?: dispatch_get_main_queue(), ^{
                if (self.completionHandler) {
                    self.completionHandler(task.response, responseObject, serializationError);
                }

            dispatch_async(dispatch_get_main_queue(), ^{
                [[NSNotificationCenter defaultCenter] postNotificationName:AFNetworkingTaskDidCompleteNotification object:task userInfo:userInfo];
                });
            });
        });
```
通知的作用是decrementActivityCount;

[self.refreshControl endRefreshing];等