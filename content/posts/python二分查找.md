---
title: "Python二分查找"
date: 2018-10-01T10:36:53+08:00
draft: false
categories:
  - python
tags:
  - 算法
---
<!--more-->
```python
时间复杂度为o（logN）
    def demo(array, t):
        for i in range(len(array):
            if array[i] == t:
                return True
        return False
    
    def demo1(array, t):
        left = 0
        right = len(array) - 1
        while left <= right:
            mid = int((left+right)/2)
            if array[mid] < t:
                left = mid+1
            elif array[mid] > t:
                right = mid -1
            else:
                return True
        return False
    array = list(range(100000))
    import time 
    t1 = time.time()
    demo(array,100001)
    t2 = time.time()
    print('线性查找', t2-t1)

    t3 = time.time()
    demo1(array, 100001)
    t4 = time.time()
    print('二分查找', t4-t3)
```