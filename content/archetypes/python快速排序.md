---
title: "Python快速排序"
date: 2018-11-01T10:38:06+08:00
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