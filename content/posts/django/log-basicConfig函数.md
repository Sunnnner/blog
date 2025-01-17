---
title: "Python Logging 完整指南"
date: 2019-12-05T15:40:17+08:00
draft: false
categories:
  - python
tags:
  - 内置函数
---
<!--more-->

## 1. Logging 基础概念

### 1.1 为什么使用 Logging
| 特性 | Print | Logging |
|------|--------|----------|
| 输出控制 | 无法控制 | 可设置日志级别 |
| 输出目标 | 标准输出 | 多种输出方式 |
| 格式化 | 基础格式化 | 丰富的格式化选项 |
| 线程安全 | 否 | 是 |

### 1.2 核心组件
1. Logger: 日志记录器
2. Handler: 日志处理器
3. Filter: 日志过滤器
4. Formatter: 日志格式化器

## 2. 配置方法

### 2.1 基础配置
```python
import logging

logging.basicConfig(
    filename="app.log",
    filemode="w",
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO
)
```

### 2.2 文件配置
```python
import logging.config

# 使用配置文件
logging.config.fileConfig('logging.conf', 
    defaults=None,
    disable_existing_loggers=False
)
```

### 2.3 字典配置
```python
import logging.config

config_dict = {
    'version': 1,
    'formatters': {
        'standard': {
            'format': '%(asctime)s [%(levelname)s] %(name)s: %(message)s'
        },
    },
    'handlers': {
        'default': {
            'level': 'INFO',
            'formatter': 'standard',
            'class': 'logging.StreamHandler',
        },
    },
    'loggers': {
        '': {
            'handlers': ['default'],
            'level': 'INFO',
            'propagate': True
        }
    }
}

logging.config.dictConfig(config_dict)
```

## 3. 日志级别

### 3.1 级别定义
| 级别 | 数值 | 使用场景 |
|------|------|----------|
| DEBUG | 10 | 详细调试信息 |
| INFO | 20 | 确认程序按预期运行 |
| WARNING | 30 | 警告信息（默认级别）|
| ERROR | 40 | 错误信息 |
| CRITICAL | 50 | 严重错误信息 |

### 3.2 使用示例
```python
logging.debug('调试信息')
logging.info('正常信息')
logging.warning('警告信息')
logging.error('错误信息')
logging.critical('严重错误')
```

## 4. Handler 类型

### 4.1 常用Handler
```python
# 文件处理器
file_handler = logging.FileHandler('app.log')

# 流处理器
stream_handler = logging.StreamHandler()

# 轮转文件处理器
rotating_handler = logging.handlers.RotatingFileHandler(
    'app.log',
    maxBytes=1024*1024,  # 1MB
    backupCount=5
)

# 定时轮转处理器
time_handler = logging.handlers.TimedRotatingFileHandler(
    'app.log',
    when='midnight',
    interval=1,
    backupCount=7
)
```

### 4.2 高级Handler
- SocketHandler: TCP/IP输出
- SMTPHandler: 邮件输出
- HTTPHandler: HTTP输出
- SysLogHandler: 系统日志输出

## 5. 格式化配置

### 5.1 格式化字段
| 字段 | 说明 |
|------|------|
| %(asctime)s | 时间戳 |
| %(levelname)s | 日志级别名称 |
| %(filename)s | 文件名 |
| %(funcName)s | 函数名 |
| %(lineno)d | 行号 |
| %(message)s | 日志信息 |
| %(thread)d | 线程ID |
| %(threadName)s | 线程名称 |
| %(process)d | 进程ID |

### 5.2 完整配置示例
```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S',
    filename='app.log',
    filemode='a',
    encoding='utf-8'
)

# 添加控制台输出
console = logging.StreamHandler()
console.setLevel(logging.INFO)
formatter = logging.Formatter('%(name)-12s: %(levelname)-8s %(message)s')
console.setFormatter(formatter)
logging.getLogger('').addHandler(console)
```

## 6. 最佳实践

### 6.1 日志配置建议
1. 使用模块级别的logger
2. 合理设置日志级别
3. 实现日志轮转
4. 添加适当的上下文信息

### 6.2 性能考虑
1. 使用 lazy logging
2. 合理设置缓冲区大小
3. 避免频繁打开关闭文件
4. 使用异步日志处理

### 6.3 安全建议
1. 注意日志文件权限
2. 避免记录敏感信息
3. 实现日志备份策略
4. 监控日志大小