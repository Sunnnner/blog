---
title: "Git加速"
date: 2019-10-12T15:29:07+08:00
draft: false
categories:
  - github
tags:
  - git
---
<!--more-->
## 全局代理，写入配置
    git config --global http.proxy 'socks5://127.0.0.1:1080'
    git config --global https.proxy 'socks5://127.0.0.1:1080'

## 清除配置
    git config --global --unset http.proxy
    git config --global --unset https.proxy

## 临时代理
    ALL_PROXY=socks5://127.0.0.1:1080 git clone xxx