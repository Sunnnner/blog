---
title: "Os模块"
date: 2019-10-10T14:20:46+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["system", "python"]
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

`os .path.dirname(path)` 获取路径名

`os.path.basename(path)` 获取文件名

`os.path.join(path1[,path2[,….]])` 将路径与文件名拼接成一个完整的路径

`os.path.split(path) `分割路径与文件名，返回元组(f_path, f_name), 如果完全使用目录，它也会将最后一个目录作为文件名分离，且不会判断文件或者目录是否存在

`os.path.splitext(path) `分割文件名与扩展名

`os.path.getsize(file)` 或得文件大小，单位是字节

`os.path.gettatime(file) `或得文件最近的访问时间，返回的是浮点型秒数

`os.path.getctime(file) `或得文件的创建时间，返回的是浮点型秒数

`os.path.getmtime(file)` 或得文件的修费时间，返回的是浮点型秒数

`os.path.exists(path)` 判断路径是否存在

`os.path.isabs(path)` 判断是否为绝对路径

`os.path.isdir(path)` 判断是否存在且是一个目录

`os.path.isfile(path)`

`os.path.islink(path)` 判断是否存在且是一个符号链接

`os.path.ismount(path) `判断是否存在且是一个挂载点

`os.path.samefile(path1, path2)` 判断两个路径是否指向同一个文件