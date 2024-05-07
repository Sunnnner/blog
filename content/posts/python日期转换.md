---
title: "Python日期转换"
date: 2019-12-10T15:43:08+08:00
draft: true
categories:
  - python
tags:
  - 内置函数
---
<!--more-->

- 秒数是相对于1970.1.1号的秒数
- 日期的模块有time、datetime

```python
import datetime
t = datetime.datetime(2009, 10, 21, 0, 0, 10, 10)   # 分别是年份、月份、日、小时、分钟、秒、微妙(10-6秒)
print (t-datetime.datetime(1970,1,1)).total_seconds()  # 总共多少秒
import datetime, time
t = datetime.datetime(2011, 10, 21, 0, 0)
time.mktime(t.timetuple())
1319148000.0
string转datetime
str = '2012-11-19'
date_time = datetime.datetime.strptime(str,'%Y-%m-%d')
datetime.datetime(2012,11,19,0,0)
datetime转string
date_time.strftime('%Y-%m-%d')

'2012-11-19'
```

## datetime转时间戳

`time_time = time.mktime(date_time.timetuple())`

## 时间戳转string

- `time.strftime('%Y-%m-%d',time.localtime(time_time))`
- '2012-11-19'

## date转datetime

```python
date = datetime.date.today()

date

datetime.date(2012,11,19)

datetime.datetime.strptime(str(date),'%Y-%m-%d')    #将date转换为str，在由str转换为datetime

datetime.datetime(2012,11,19,0,0)
```