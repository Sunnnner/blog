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