---
title: "Python线程安全"
date: 2022-07-08T09:32:29+08:00
draft: true
categories:
  - python
tags:
  - 线程安全
---
<!--more-->

- 线程不安全的主要原因是我们的代码不是原子操作导致的
- 原子操作(atomic operation),指不会被线程调度机制打断的操作，这种操作一旦开始，就一直运行到结束，中间不会切换，它类似与数据库的事务操作。
- 为确保线程安全，我们需要人工实现原子操作，因为我们不能保证我们在多线程的情况下代码都具有原子性
- 因此我们需要使用线程锁来使代码具有原子性
- 代码实例

```python
from threading import Thread, Lock

number = 0
lock = Lock()

def target():
    global number
    for _ in range(1000000):
        with lock:
            number += 1

# 开启两个线程
threads = [Thread(target=target) for _ in range(2)]
for t in threads:
    t.start()
for t in threads:
    t.join()

print(number)

```
- 现在，不论你执行多少次，输出都是2000000
