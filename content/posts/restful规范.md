---
title: "Restful规范"
date: 2019-09-06T11:36:12+08:00
draft: false
categories:
  - python
tags:
  - api设计规范
---

restful 只是一种软件架构风格或者说是一种设计风格，它只是给我们提供了一个设计的原则和约束的条件，主要用于客户端与服务端的交互
<!--more-->
我们可以根据自己的需求做的更加简洁， 更有层次

它里面提供了一些规范，比如restful提倡面向资源编程， 在URL接口中尽量使用名词， 不要使用动词

在restful推荐使用HTTPS协议，更加安全

尽量在URL中体现版本号

restful的method <GET/ POST/ PUT/ DELETE/ PATCH>

响应应该设置状态码

有返回值，并且为json格式

返回结果中要提供帮助链接， 即API最好做好Hypermedia