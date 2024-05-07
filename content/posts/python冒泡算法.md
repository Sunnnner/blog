---
title: "Python冒泡算法"
date: 2018-09-08T10:36:08+08:00
draft: true
categories:
  - python
tags:
  - 算法
---
<!--more-->
```python
冒泡
def damo(sun):
    for i in range(len(sun)-1):
        for j in range(len(sun)-i-1):
            if sun[j]> sun[j+1]:
                sun[j], sun[j+1] = sun[j+1], sun[j]
    return sun
```