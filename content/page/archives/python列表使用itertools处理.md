---
title: "使用itertools处理python嵌套列表问题"
date: 2022-05-13T13:39:13+08:00
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