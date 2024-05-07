---
title: "Python快速排序"
date: 2018-11-01T10:38:06+08:00
draft: true
categories:
  - python
tags:
  - 算法
---
<!--more-->
```python

def demo(A,p,r):
    x = A[r]
    i = p-1
    for j in range(p,r):
        if A[j] <= x:
            i = i+1
            A[i],A[j] = A[j],A[i]
    A[i+1], A[r] = A[r],A[i+1]
    return  i + 1
def demo2(A,p,r):
    if p< r:
        q = demo(A,p,r)
        demo(A,p,q-1)
        demo(A,q+1,r)
A = [23,54,6,5,7,8]
# 0,4代表列表的下标
demo2(A,0,4)
print(A)

```