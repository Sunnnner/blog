---
title: "Python字典按值排序"
date: 2018-12-02T10:39:55+08:00
draft: false
categories:
  - python
tags:
  - 字典
---
<!--more-->

```python

# 方法1
f = zip(x.values(),x.keys())
sorted(f)
# 方法2
sorted(x.items(), key = lambda x:x[1], reverse = True)
# 字典key value互换
# 使用zip压缩器
# 使用字典推导式
{v: k for k ,v in x.items()}

```