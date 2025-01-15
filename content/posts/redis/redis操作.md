---
title: "Redis操作"
description: 
date: 2025-01-15T09:58:57+08:00
draft: false
categories:
  - redis
tags:
  - redis
---
<!--more-->

# Redis 完全指南

## 一、Redis概述

### 1.1 什么是Redis

Redis(Remote Dictionary Server)是一个开源的高性能键值对(key-value)数据库。主要特点:

*   基于内存运行,支持持久化
*   支持多种数据结构
*   支持主从复制
*   使用C语言编写,遵守BSD协议

### 1.2 主要特性

*   性能优秀,支持10万/秒读写
*   数据类型丰富(String、Hash、List、Set、Zset)
*   原子性操作,所有操作都是原子性
*   支持发布/订阅模型
*   支持持久化机制

### 1.3 应用场景

*   缓存系统
*   计数器/限流
*   消息队列
*   排行榜/计分板
*   Session共享
*   分布式锁

## 二、安装部署

### 2.1 Linux安装

```bash
# 更新源
sudo apt-get update

# 安装Redis服务器
sudo apt-get install redis-server

# 启动Redis服务
redis-server

# 测试连接
redis-cli
> ping  # 返回PONG表示成功
```

### 2.2 服务管理命令

```bash
# 启动服务
sudo service redis start 

# 停止服务  
sudo service redis stop

# 重启服务
sudo service redis restart

# 查看版本
redis-cli --version
redis-server -v
```

## 三、Redis基本命令

### 3.1 键(Key)操作

```redis
# 查看所有键
keys *  

# 判断键是否存在
exists key

# 查看键类型
type key

# 删除键
del key 

# 设置过期时间(秒)
expire key seconds

# 查看剩余时间
ttl key
```

### 3.2 数据库操作

```redis
# 切换数据库 
select index

# 查看当前数据库的key数量
dbsize

# 清空当前数据库
flushdb

# 清空所有数据库
flushall
```

## 四、Redis数据类型

### 4.1 String类型

最基本的数据类型,可以存储字符串、整数或浮点数。

```redis
# 设置值
set key value
setex key seconds value  # 设置过期时间

# 获取值
get key
mget key1 key2  # 获取多个

# 数值操作
incr key  # 值+1
decr key  # 值-1 
incrby key increment  # 增加指定值
decrby key decrement  # 减少指定值
```

### 4.2 Hash类型

适合存储对象,类似map结构。

```redis
# 设置
hset key field value
hmset key field1 value1 field2 value2

# 获取 
hget key field
hmget key field1 field2
hgetall key  # 获取所有字段和值

# 删除
hdel key field
```

### 4.3 List类型

有序字符串列表。

```redis
# 添加
lpush key value  # 左侧添加
rpush key value  # 右侧添加

# 查询
lrange key start stop  # 获取片段
llen key  # 获取长度 

# 删除
lpop key  # 左侧弹出
rpop key  # 右侧弹出
```

### 4.4 Set类型

无序字符串集合,元素不重复。

```redis
# 添加
sadd key member

# 查询
smembers key  # 获取所有成员
sismember key member  # 判断是否存在

# 集合运算
sinter key1 key2  # 交集
sunion key1 key2  # 并集
sdiff key1 key2   # 差集
```

### 4.5 Zset类型

有序集合,每个元素关联一个分数。

```redis
# 添加
zadd key score member

# 查询
zrange key start stop  # 按分数获取片段
zcard key  # 获取成员数
zscore key member  # 获取分数

# 删除  
zrem key member
```

## 五、性能优化建议

1.  合理设置maxmemory
2.  使用合适的淘汰策略
3.  设置键值对生命周期
4.  避免使用大key
5.  使用批量操作提高效率

## 六、安全建议

1.  设置访问密码
2.  禁用危险命令
3.  限制网络访问
4.  定期备份数据
5.  监控系统运行状态

