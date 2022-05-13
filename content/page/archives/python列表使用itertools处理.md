---
title: "使用itertools处理python嵌套列表问题"
description: 
date: 2022-05-13T13:39:13+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---


- 使用itertools处理python嵌套列表问题

- 当我们想要把一串字符分割成列表的时候

```python

import itertools

a = "1111"

>>>print(list(itertools.chain(a)))


output:  ['1', '1', '1', '1']

```

- 嵌套列表组合成一个列表

```python

import itertools

>>> a = [1, [2], [3], 4, 5]

>>> print(itertools.chain.from_iterable(a))

output: [1, 2, 3, 4, 5]

```