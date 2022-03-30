---
title: "Python链表"
date: 2018-10-02T10:37:28+08:00
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

1-->2-->3-->4-->5-->null
5-->4->3-->2-->1-->null
class Demo(object):
    def __init__(self,x):
        self.val = x
        self.next = None

class Demo1(object):
    def reverseList(self,head):
        dummy = head
        tmp = dummy

        while head and head.next != None:
            dummy = head.next
            head.next = dummy.next
            dummy.next = tmp
            tmp = dummy
        return dummy

head = Demo(1)
head.next = Demo(2)
head.next.next = Demo(3)
head.next.next.next = Demo(4)
head.next.next.next.next = Demo(5)

demo1 = Demo1()
reverse_head = demo1.reverseList(head)
tmp = reverse_head

while tmp:
    print(tmp.val)
    tmp = tmp.next
```