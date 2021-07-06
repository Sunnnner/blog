---
title: "Python Collections Duque函数演示"
date: 2019-10-15T15:33:37+08:00
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

- duque函数有一个maxlen参数，当append的时候，如果超过，那么最前面的就会被挤出队列

```python
from collections import duque
def search(lines, pattern, lens=5):
    previous_lines = deque(maxlen=lens)
    for li in lines:
        if pattern in li:
            yield li, previous_lines
        previous_lines.append(li)

if name == ‘main‘:
    with open(r’./xx.txt’) as f:
        for line, prevlines in search(f, ‘python’, 5):
            for pline in prevlines:
                print(pline, end=’’)
            print(line, end=’’)
        print(‘**’ * 20)
```