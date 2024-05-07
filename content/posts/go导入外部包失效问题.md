---
title: "Go导入外部包失效问题"
date: 2021-08-26T10:48:36+08:00
draft: true
categories:
  - go

---


- 小记在mac上使用vscode导入redis包失效问题

- 解决办法

```shell
vim .bash_profile
# 环境变量导入当前工作目录
export GOPATH=/Users/xxx/Desktop/go-project

cd /Users/xxx/Desktop/go-project

go mod init example.com/m/v2
# 自动下载所需的包
go mod tidy
# 项目源代码放置处
mkdir src
cd src
# 可以开始编写了
```