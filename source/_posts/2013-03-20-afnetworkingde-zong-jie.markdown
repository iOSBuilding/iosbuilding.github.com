---
layout: post
title: "AFNetworking的总结"
date: 2013-03-20 16:02
comments: true
categories: 
---
一直想写一篇关于AFNetworking学习总结的文章便于自己记忆，迟迟没有动手，今天终于开始动笔啦。自从ASIH的作者停止更新之后，我们不免有点小失望，直到AFNetworking的出现让我们重新燃起激情。AFnetworking稳定的更新维护及其良好的可扩展性，不得不佩服[@matt](https://github.com/mattt)确实是个geek.  
**AFnetwokring的OverView**
![](https://github.com/AFNetworking/AFNetworking/raw/gh-pages/afnetworking-architecture-diagram.png)

AFnetworking的构成

* `AFURLConnectionOperation` NSOperation的子类主要实现NSURLConnection协议的方法
* `AFHTTPRequsetOperation` AFURLConnectionOpration的子类封装一些http相关的协议
* `AFJSONRequsetOperation` AFHTTPRequsetOperation的子类，用于JSON的解析（默认使用的是系统自带JSON解析NSJSONSerialization）
* `AFXMLRequsetOperation`  AFHTTPRequsetOperation的子类，用于XML的解析
* `AFPropertyListRequestOperation` AFHTTPRequsetOperation的子类，用于Plist文件的解析
* `AFImageRequestOperation` AFHTTPRequsetOperation的子类，用于图片的下载
* `UIImageView+AFnetworking` UIImageView的扩展，异步加载图片
* `AFHTTPClient` NSObeject的子类，实现基于base URL的网络请求

**注意以上所有的网络请求都是异步**
##AFNetworking类的使用
###AFHTTPRequsetOperation的使用

	AFHTTPRequsetOperation *requsetOpeation = [[AFHTTPRequsetOperation 	alloc]initWithRequest:urlRequest];
	[requsetOperation setCompletionBlockWithSuccess:^(AFHTTPRequestOperation 	*operation, id responseObject) {
   	 	self.data = responseObject;
	} failure:^(AFHTTPRequestOperation *operation, NSError *error){
   		 NSLog(@"%@", [error localizedDescription]);
	}];
	[requsetOpeation start];
###AFJSONRequsetOtion的使用
	AFJSONRequestOperation *requsetOpeation = [AFJSONRequestOperation 	JSONRequestOperationWithRequest:urlResquest 
	success:^(NSURLRequest *request, NSHTTPURLResponse *response, id JSON) { 
         if ([JSON isKindOfClass:[NSData class]]) {
              self.data = JSON;
         } else if([JSON isKindOfClass:[NSDictionary class]]){
              self.dictionary = JSON;
         } 
 	} failure:^(NSURLRequest *request, NSHTTPURLResponse *response, NSError 	*error, id JSON) { 
       NSLog(@"%@", [error localizedDescription]); 
 	}];
	[requsetOpeation start];
###AFXMLRequsetOperation的使用
	AFXMLRequestOperation *requsetOpeation = [AFXMLRequestOperation 	XMLParserRequestOperationWithRequest:urlResquest 
	success:^(NSURLRequest *request, NSHTTPURLResponse *response, NSXMLParser 	*XMLParser) {
  		XMLParser.delegate = self;
  		[XMLParser parse];
	} failure:^(NSURLRequest *request, NSHTTPURLResponse *response, NSError 	*error, NSXMLParser *XMLParser) {
  		 NSLog(@"%@", [error localizedDescription]);
	}];
	[requsetOpeation start];
###AFPropertyListRequestOperation的使用
	AFPropertyListRequestOperation *requsetOpeation = [AFPropertyListRequestOperation propertyListRequestOperationWithRequest:urlResquest 
	success:^(NSURLRequest *request, NSHTTPURLResponse *response, id propertyList) {   
     	self.dictionary = propertyList;
	} failure:^(NSURLRequest *request, NSHTTPURLResponse *response, NSError *error, id propertyList) {
     	NSLog(@"%@", [error localizedDescription]); 
 	}];
	[requsetOpeation start];
###AFImageRequestOperation的使用
###UIImageView+AFnetworking的使用
###AFHTTPClien的使用
##***AFnetworking extension***
待续。。。。。。
