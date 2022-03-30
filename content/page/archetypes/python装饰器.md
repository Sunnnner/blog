---
title: "Python装饰器"
date: 2018-09-07T10:35:21+08:00
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
装饰器
def demo(name):
    print('demo--name', name)
    def demo1(demo_name):
        print('demo1--demoname', demo_name.__name__)
        def demo2():
            print('demo--name', name)
            demo_name()
        return demo2
    return demo1
@demo('zhuangshiqi')
def test():
    print('test')
test()
```