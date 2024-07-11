---
title: "Tauri修复http跨域cors错误"
description: 
date: 2024-07-04T13:49:59+08:00
draft: false
categories:
  - rust
tags:
  - tauri
---
<!--more-->

- 修改`tauri.conf.json > tauri > security > dangerousUseHttpScheme = true`重新打包之后可以访问http任意链接
- csp设置: `default-src blob: data: filesystem: ws: wss: http: https: tauri: asset: 'unsafe-eval' 'unsafe-inline' 'self'; script-src blob: 'unsafe-inline' 'unsafe-hashes' 'self';` 每个命令之间使用`;`相隔.