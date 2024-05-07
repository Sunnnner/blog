---
title: "Python链表"
date: 2018-10-02T10:37:28+08:00
draft: false
categories:
  - python
tags:
  - 算法
---
<!--more-->
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