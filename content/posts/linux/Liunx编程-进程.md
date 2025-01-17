---
title: "Python多进程编程指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - python
tags:
  - 进程
---
<!--more-->
## 1. 多任务基础概念

### 1.1 什么是多任务
- 同时执行多个任务的能力
- Linux是真正的多任务多用户系统
- Windows是多任务但非真正多用户系统

### 1.2 并发与并行
| 概念 | 说明 |
|------|------|
| 并发(Concurrent) | 多个任务交替执行 |
| 并行(Parallel) | 多个任务同时执行 |

### 1.3 时间片轮转调度
- 每个进程被分配一个时间片
- 分为两种优先级调度算法：
  - 非抢占式：进程执行完才释放CPU
  - 抢占式：高优先级进程可中断低优先级进程

## 2. 进程创建方式

### 2.1 使用os.fork()（Unix/Linux/Mac）
```python
import os

pid = os.fork()
if pid == 0:
    print('子进程')
elif pid > 0:
    print('父进程')
else:
    print('创建失败')
```

### 2.2 使用multiprocessing（跨平台）
```python
from multiprocessing import Process

def task(name):
    print(f'任务 {name} 正在运行')

if __name__ == '__main__':
    # 创建进程
    p = Process(target=task, args=('process1',))
    # 启动进程
    p.start()
    # 等待进程结束
    p.join()
```

## 3. Process类详解

### 3.1 主要参数
```python
Process(
    group=None,  # 进程组，通常为None
    target=None, # 目标函数
    name=None,   # 进程名称
    args=(),     # 位置参数
    kwargs={}    # 关键字参数
)
```

### 3.2 常用方法
| 方法 | 说明 |
|------|------|
| start() | 启动进程 |
| join([timeout]) | 等待进程结束 |
| terminate() | 终止进程 |
| is_alive() | 判断进程是否在运行 |

### 3.3 常用属性
- name: 进程名称
- pid: 进程ID
- daemon: 守护进程标志

## 4. 自定义Process子类
```python
class MyProcess(Process):
    def __init__(self, name):
        super().__init__()
        self.name = name
        
    def run(self):
        print(f'进程 {self.name} 正在运行')

if __name__ == '__main__':
    p = MyProcess('custom_process')
    p.start()
    p.join()
```

## 5. 进程池(Pool)

### 5.1 基本使用
```python
from multiprocessing import Pool

def task(n):
    return n * n

if __name__ == '__main__':
    with Pool(4) as p:
        # 非阻塞方式
        results = p.apply_async(task, args=(10,))
        print(results.get())
        
        # 阻塞方式
        result = p.apply(task, args=(10,))
        print(result)
```

### 5.2 Pool方法对比
| 方法 | 特点 | 适用场景 |
|------|------|----------|
| apply | 阻塞式 | 任务需要顺序执行 |
| apply_async | 非阻塞式 | 任务可并行执行 |

## 6. 进程间通信(IPC)

### 6.1 Queue
```python
from multiprocessing import Process, Queue

def producer(q):
    q.put('数据')

def consumer(q):
    data = q.get()
    print(f'收到数据: {data}')

if __name__ == '__main__':
    q = Queue()
    
    p1 = Process(target=producer, args=(q,))
    p2 = Process(target=consumer, args=(q,))
    
    p1.start()
    p2.start()
    
    p1.join()
    p2.join()
```

### 6.2 Queue方法
| 方法 | 说明 |
|------|------|
| put(item) | 放入数据 |
| get() | 获取数据 |
| empty() | 判断队列是否为空 |
| full() | 判断队列是否已满 |
| qsize() | 获取队列中元素数量 |

### 6.3 进程池中使用Queue
```python
from multiprocessing import Pool, Manager

def worker(q):
    q.put('数据')

if __name__ == '__main__':
    manager = Manager()
    q = manager.Queue()
    
    with Pool(4) as p:
        p.apply(worker, (q,))
```

## 7. 最佳实践

### 7.1 进程设计原则
1. 合理控制进程数量
2. 注意资源释放
3. 避免进程间频繁通信
4. 正确处理异常

### 7.2 性能优化
1. 使用进程池管理进程
2. 适当使用非阻塞操作
3. 减少进程创建销毁频率
4. 合理设置超时机制

### 7.3 调试技巧
1. 设置有意义的进程名
2. 使用日志记录关键信息
3. 合理使用join等待机制
4. 善用进程状态检查