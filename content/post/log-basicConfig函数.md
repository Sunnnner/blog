---
title: "Log BasicConfig函数"
date: 2019-12-05T15:40:17+08:00
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

# logging.basicConfig函数

- logging模块是Python内置标准模块，主要用于输出运行日志，可以设置输出日志的等级、日志保存路径，日志文件回滚等

##相比Print优点：

- 可以通过设置不同的日志等级，在release版本中只输出重要信息，而不必显示大量的调试信息；
- print将所有信息都输出到标准输出中，严重影响开发者从标准输出中查看其它数据；logging则可以由开发者决定将信息输出到什么地方，以及怎么输出；
- 在python中，logging由logger，handler，filter，formater四个部分组成：
- logger是提供我们记录日志的方法；handler是让我们选择日志的输出地方，如：控制台，文件，邮件发送等，一个logger添加多个handler；filter是给用户提供更加细粒度的控制日志的输出内容；formater用户格式化输出日志的信息。

## python中配置logging有三种方式

### 第一种：基础配置，

```python
logging.basicConfig(
    filename="config.log",
    filemode="w",
    format="%(asctime)s-%(name)s-%(levelname)s-%(message)s",
    level=logging.INFO)

第二种：使用配置文件的方式配置logging,使用`fileConfig函数来读取配置文件

fileConfig(
    filename,
    defaults=None,
    disable_existing_loggers=Ture )`
第三种：使用一个字典方式来写配置信息，然后使用dictConfig

dictConfig(
    dict,
    defaults=None, 
    disable_existing_loggers=Ture )
```

## 日志Level等级

- 日志一共分成5个等级，从低到高分别是：DEBUG ,INFO ,WARNING ,ERROR, CRITICAL。
- DEBUG：详细的信息,通常只出现在诊断问题上
- INFO：确认一切按预期运行
- WARNING：一个迹象表明,一些意想不到的事情发生了,或表明一些问题在不久的将来(例如。磁盘空间低”)。这个软件还能按预期工作。
- ERROR：更严重的问题,软件没能执行一些功能
- CRITICAL：一个严重的错误,这表明程序本身可能无法继续运行
- 这5个等级，也分别对应5种打日志的方法： debug 、info 、warning 、error、critical。默认的是WARNING，当在WARNING或之上时才被跟踪。

## 二、日志输出：可以输出在控制台和文件，我选择的是输出在文件

```python
StreamHandler：logging.StreamHandler；日志输出到流，可以是sys.stderr，sys.stdout或者文件

FileHandler：logging.FileHandler；日志输出到文件
BaseRotatingHandler：logging.handlers.BaseRotatingHandler；基本的日志回滚方式

RotatingHandler：logging.handlers.RotatingHandler；日志回滚方式，支持日志文件最大数量和日志文件回滚

日志回滚的意思为：比如日志文件是chat.log，当chat.log达到指定的大小之后，RotatingFileHandler自动把文件改名为chat.log.1。不过，如果chat.log.1已经存在，会先把chat.log.1重命名为chat.log.2。最后重新创建 chat.log，继续输出日志信息。【这样保证了chat.log里面是最新的日志】

TimeRotatingHandler：logging.handlers.TimeRotatingHandler；日志回滚方式，在一定时间区域内回滚日志文件

SocketHandler：logging.handlers.SocketHandler；远程输出日志到TCP/IP sockets

DatagramHandler：logging.handlers.DatagramHandler；远程输出日志到UDP sockets

SMTPHandler：logging.handlers.SMTPHandler；远程输出日志到邮件地址

SysLogHandler：logging.handlers.SysLogHandler；日志输出到syslog

NTEventLogHandler：logging.handlers.NTEventLogHandler；远程输出日志到Windows NT/2000/XP的事件日志

MemoryHandler：logging.handlers.MemoryHandler；日志输出到内存中的指定buffer

HTTPHandler：logging.handlers.HTTPHandler；通过”GET”或者”POST”远程输出到HTTP服务器
```

## 三、日志格式说明

```python
logging.basicConfig函数中，可以指定日志的输出格式format，这个参数可以输出很多有用的信息
logging.basicConfig函数各参数:
filename: 指定日志文件名
filemode: 和file函数意义相同，指定日志文件的打开模式，'w'或'a'
format: 指定输出的格式和内容，format可以输出很多有用信息，如上例所示:
 %(levelno)s: 打印日志级别的数值
 %(levelname)s: 打印日志级别名称
 %(pathname)s: 打印当前执行程序的路径，其实就是sys.argv[0]
 %(filename)s: 打印当前执行程序名
 %(funcName)s: 打印日志的当前函数
 %(lineno)d: 打印日志的当前行号
 %(asctime)s: 打印日志的时间
 %(thread)d: 打印线程ID
 %(threadName)s: 打印线程名称
 %(process)d: 打印进程ID
 %(message)s: 打印日志信息
datefmt: 指定时间格式，同time.strftime()
level: 设置日志级别，默认为logging.WARNING
stream: 指定将日志的输出流，可以指定输出到sys.stderr,sys.stdout或者文件，默认输出到sys.stderr，当stream和filename同时指定时，stream被忽略
logging打印信息函数：
logging.debug('This is debug message')
logging.info('This is info message')
logging.warning('This is warning message')
```

## 初始化日志对象

```python
logging.basicConfig(
    # 日志级别
    level = logging.INFO,
    # 日志格式
    # 时间、代码所在文件名、代码行号、日志级别名字、日志信息
    format = '%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
    # 打印日志的时间
    datefmt = '%a, %d %b %Y %H:%M:%S',
    # 日志文件存放的目录（目录必须存在）及日志文件名
    filename = 'd:/report.log',
    # 打开日志文件的方式
    filemode = 'w'
)
```