---
title: "Python装饰器"
date: 2018-09-07T10:35:21+08:00
draft: true
categories:
  - python
tags:
  - 设计模式
---
<!--more-->
```python
装饰器
def demo(name):
    print('demo--name', name)
    def demo1(demo_name):
        print('demo1--demoname', demo_name.__name__)
        def demo2():
            print('demo--name', name)
            demo_name()
        return demo2
    return demo1
@demo('zhuangshiqi')
def test():
    print('test')
test()
```