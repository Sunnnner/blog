---
title: "Session+cookie和使用tocken有什么区别"
date: 2019-02-03T10:51:26+08:00
draft: true
categories:
  - python
tags:
  - web
---

cookie数据存放在客户的浏览器上，session数据放在服务器上。
<!--more-->
cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗

考虑到安全应当使用session。

考虑到减轻服务器性能方面，应当使用COOKIE。

将登陆信息等重要信息存放为SESSION

其他信息如果需要保留，可以放在COOKIE中

session 和 token并不矛盾，作为身份认证 token安全性比session好

token就是令牌，比如你授权（登录）一个程序时，他就是个依据，判断你是否已经授权该软件；cookie就是写在客户端的一个txt文件，里面包括你登录信息之类的，这样你下次在登录某个网站，就会自动调用cookie自动登录用户名；session和cookie差不多，只是session是写在服务器端的文件，也需要在客户端写入cookie文件，但是文件里是你的浏览器编号.Session的状态是存储在服务器端，客户端只有session id；而Token的状态是存储在客户端。