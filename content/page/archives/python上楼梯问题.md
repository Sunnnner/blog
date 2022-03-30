---
title: "Python上楼梯问题"
date: 2018-12-01T10:39:04+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["python"]
author: "whitek"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/Sunnnner/Sunnnner.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

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