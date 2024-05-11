---
title: "新版docker Compose文件编写"
description: 
date: 2024-05-11T16:09:03+08:00
draft: false
categories:
  - docker
tags:
  - docker-compose
---
<!--more-->

## 新版docker Compose文件编写

- 顶部声明版本`version`更改为`name: myapp`
- 顶级属性由 Compose 规范定义为未显式设置的项目名称。 Compose 提供了一种覆盖此名称的方法，并设置了 如果未设置顶级元素，则要使用的默认项目名称。
- 项目名称默认为当前目录的基本名称，但可以通过设置`name`属性来覆盖。
- 项目名称用于创建网络和卷名称，以便在多个项目之间进行隔离。
- 项目名称还用于创建容器名称，以便在多个项目之间进行隔离。

```yaml
name: myapp

services:
  foo:
    image: busybox
    command: xxx
```

- volume
  - `volume`属性已更改为`volumes`。
  
```yaml
services:
  foo:
    image: busybox
    volumes:
      - /path/to/data:/data
```
or
```yaml
services:
  foo:
    image: busybox
    volumes:
      - db-data:/data
volumes:
  db-data:
    driver: foobar
```

## 参考
- [version and name](https://docs.docker.com/compose/compose-file/04-version-and-name/)
- [volumes](https://github.com/compose-spec/compose-spec/blob/master/07-volumes.md)