---
title: "Docker操作"
date: 2019-10-08T14:19:00+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["docker"]
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


`docker build` 打包docker 项目

`docker-compose up` 启动整体项目(docker-compose.yml文件)

`docker-compose down` 强制停止docker运行的所有项目

1、删除所有容器 docker rm `docker ps -a -q`


2、删除所有镜像d ocker rmi `docker images -q`

3、按条件删除镜像 没有打标签docker rmi `docker images -q | awk '/^<none>/ { print $3 }'`

镜像名包含关键字docker rmi --force `docker images | grep doss-api | awk '{print $3}'`    //其中doss-api为关键字

　

`docker-compose.yml`

`service` 项目

`image docker`镜像名字，若本地没有会尝试在docker服务器拉取

`restart` 是否stop后重启

`command` 启动路径

`volumes` 将docker容器文件夹与本地文件夹映射挂载 [本地:docker文件夹]

`environment` 运行携带的参数

`ports`运行端口

`links` 关联项目，关联之后内部访问