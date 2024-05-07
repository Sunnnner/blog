---
title: "Python上楼梯问题"
date: 2018-12-01T10:39:04+08:00
draft: true
categories:
  - python
tags:
  - 算法
---
<!--more-->
```python

 def demo(n):
        a = 1排序
        b = 2
        c = 3
        for i in range(n-3):
            c,b,a = a+b+c, c, b
        return c
其实就是斐波那契数列
def demo(n):                  
    if n == 1:                
        return 1              
    if n == 2:                
        return 2              
    a,b = 1, 2                
    result = 0                
    for i in range(3, n+1):   
        result = a + b        
        a = b                 
        b = result            
    return result             
                              
print(demo(10))               

```