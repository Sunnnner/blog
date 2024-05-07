---
title: "Redis配置"
date: 2018-05-31T18:53:17+08:00
draft: true
categories:
  - redis

---

```yml
1) 绑定IP地址,看业务开放
bind 0.0.0.0

2)Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程，设置为no

daemonize no

3)保护模式

protected-mode no 
# 检查启动状态命令
ps -ef|grep redis |grep 6379
mac以配置文件启动
sudo redis-server /usr/local/etc/redis.conf
Ubuntu以配置文件启动
 sudo redis-server /etc/redis/redis.conf
```