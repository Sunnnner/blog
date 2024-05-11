---
title: "Git Submodule更新主仓库"
description: 
date: 2023-12-13T11:44:52+08:00
draft: false
categories:
  - git
tags:
  - git
  - submodule
---
<!--more-->

## 步骤
- `git submodule update --init --recursive` 更新各子模块的代码
- 合并分支到`master`的时候进入到各子模块中进行合并也可以批量打tag `git submodule foreach git tag xx_tag`这个命令就会逐模块的打上tag,执行`git submodule foreach git tag`进行查看各tag
- 如果单独某一个子模块打`tag`打完之后再`submodule`仓库要执行`git submodule update --init --recursive`更新一下子模块的hash值,然后进入子模块执行`git status`,看一下`git head`的头部在哪里如果不在`master`上需要执行`git checkout master`,然后返回主仓库`git status`你就会看到子模块的hash值需要进行提交,这样方便我们进行项目管理.