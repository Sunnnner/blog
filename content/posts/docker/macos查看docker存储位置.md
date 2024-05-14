---
title: "Macos查看docker存储位置"
description: 
date: 2024-05-14T16:29:30+08:00
draft: false
categories:
  - docker
tags:
  - macos
---
<!--more-->

## 原因
- docker 在macos上是通过虚拟机运行的，所以docker的存储位置不是在macos上, 而是在虚拟机中。

## Macos查看docker存储位置
- 命令`stty -echo -icanon && nc -U ~/Library/Containers/com.docker.docker/Data/debug-shell.sock && stty sane`

## 参考
- [Getting a Shell in the Docker Desktop Mac VM](https://gist.github.com/BretFisher/5e1a0c7bcca4c735e716abf62afad389)