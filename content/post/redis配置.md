---
title: "Redis配置"
date: 2018-05-31T18:53:17+08:00
tags: ["redis"]
author: "whitek"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
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