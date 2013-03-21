---
layout: post
title: "在OC中两个对象的交互"
date: 2013-03-21 08:51
comments: true
categories: 
---
当两个对象A对象B，比如两个ViewController他们需要传递数据，你能想到那些方法呢？
###NSNotificationCenter
一对多的传递方式。对象A发出一个消息到消息中心，消息中心随后分发消息给监听该消息的对象，对象与对象之间不需要彼此知道，有点太loose啦。
###KVO (Key-Value Observing)
对象A监听对象B的属性，当对象B被监听的属性改变，通知对象A执行想要执行的方法。
###Direct pointers
对象A有一个指针指向对象B，从而直接使用该指针操作对象B。
###Delegate
对象A是对象B的代理。在这种情况下对象A不知道任何关于对象B的事，他只知道对象作为他的代理可以传递消息。
###Blocks
Blocks和代理有些类似。对象B给对象A一个或多个blocks只有当特定消息的发生的时候才执行。可以看AFNetworking里面大量使用block。


此文大部分翻译自[@hollance](https://github.com/hollance)的[Communicate between objects using channels](http://www.hollance.com/2012/07/communicate-between-objects-using-channels/)
主要是为自己总结，不足之处，敬请谅解。

另奉上一大神关于NSNotificationCenter的Blog[Let's Build NSNotificationCenter](http://www.mikeash.com/pyblog/friday-qa-2011-07-08-lets-build-nsnotificationcenter.html)。
