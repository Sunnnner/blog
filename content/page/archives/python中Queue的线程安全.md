---
title: "Python中Queue的线程安全"
description: 
date: 2022-07-08T09:39:21+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---

- 为什么Queue是线程安全的

- python的threading模块里的消息通信机制主要有以下三种
    - Event
    - Condition
    - Queue

- 使用最多的是Queue
- 原因是Queue实现了锁原语
  > 原语： 指若干个机器指令构成的完成某种特定功能的一段程序，具有不可分割性，即原语的执行必须是连续的，在执行过程中不可中断.
