---
title: "Python虚拟环境pipenv使用"
date: 2022-07-07T10:08:33+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["python"]
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

- pipenv 是一个包的版本控制软件，与我之前用过的rust语言中的cargo类似，与go的包管理器也类似，它能够锁定当前包的依赖项

- Ubuntu中可以使用`sudo apt install pipenv`
- 也可以使用当前python环境中的pip进行安装`pip install pipenv`

- pipenv 命令

- 指定python版本 `pipenv --python 3.8.12`
- 使用当前requements文件生成Pipfile文件`pipenv install`
- 锁定当前Pipfile文件`pipenv lock`
- 详细信息请参阅`https://pipenv.pypa.io/en/latest/`