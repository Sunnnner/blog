---
title: "Go导入外部包失效问题"
date: 2021-08-26T10:48:36+08:00
# weight: 1
# aliases: ["/first"]
tags: ["first"]
author: "whitek"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
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