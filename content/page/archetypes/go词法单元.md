---
title: "Go词法单元"
date: 2021-08-17T10:10:49+08:00
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


## 高级语言源程序内部的几个概念

- token、关键字、标识符、操作符、分隔符和字面量

### token

- token 是构成源程序的基本不可再分割的单元，编译器编译程序的第一步就是将源程序分割为一个个独立的token，这个过程就是词法分析

- go语言的token可以分为关键字、标识符、操作符、分隔符和字面常量等

