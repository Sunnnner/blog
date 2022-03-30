---
title: "Sql修改字段长度"
date: 2019-09-10T11:41:14+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["sql"]
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


sql修改字段长度的语法
    `alter table 表名 modify 字段名 字段类型;`

标准sql所有都适用
`alter table 数据库.表名 modify 字段名 字段类型;`

修改字段名名称
`alter table 数据库名 表名 column col1 to col2;`

添加字段
`alter table 数据库名.表名 add 字段名 类型;`

