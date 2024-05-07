---
title: "Python单例"
date: 2018-09-05T10:32:39+08:00
draft: true
categories:
  - python
tags:
  - 设计模式
---

- 举个常见的单例模式例子，我们日常使用的电脑上都有一个回收站，在整个操作系统中，回收站只能有一个实例，整个系统都使用这个唯一的实例，而且回收站自行提供自己的实例。因此回收站是单例模式的应用。

- 单例模式，是一种常用的软件设计模式。在它的核心结构中，只包含一个被称为单例的特殊类。

- 通过单例模式可以保证系统中，应用该模式的类一个类只有一个实例。即一个类只有一个对象实例。

```python
class A(object):
    # 定义类属性记录实例化对象
    __instance = None
    
    # 创建实例对象的方法
    def __new__(cls):
        # 如果没有创建实例对象就创建
        if cls.__instance == None: 
            cls.__instance = object.__new__(cls)
            return cls.__instance
        else:
            #如果存在就直接返回
            return cls.__instance
```

---

```python

# 创建单例时，只执行1次__init__方法
 class Singleton(object):
    # 定义雷属性记录实例化对象
    __instance = None
    #创建市里的方法
    def __new__(cls):
        if cls.__instance = None:
            cls.__instance = object.__new__(cls)
            return cls.__instance
        else:
            return cls.__instance
    
    def __init__(self, name):
        self.name = name

    怎么保证打印的名字是一个呢？

class Singleton(object):
    __instance = None
    # 标志语，false没有赋值 ture 已经赋值
    __init__flag = False
    重写new方法,创建对象记录下来
    下次创建对象的时候不去创建新的对象，而是返回已经创建的对象
    def __new__(cls):
    if cls.__instance = None:
        cls.__instance = object.__new__(cls)
        print('创建新对象的地址',id(cls.__instance)
        return cls.__instance
        return cls.__instance
    else:
        return cls.instance
    def __init__(self, name):
    if Singleton.__init__flag = False:
        self.name = name
        Singleton.__init__flag = True

```