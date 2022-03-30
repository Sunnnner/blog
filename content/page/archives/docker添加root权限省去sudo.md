---
title: "Docker添加root权限省去sudo"
date: 2019-11-01T15:35:30+08:00
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

- 首先使用root权限账户登录系统
- 首先查看用户组中有没有docker组sudo cat /etc/group | grep docker

创建docker分组，并将相应的用户添加到这个分组里面

sudo groupadd -g 999 docker

-g 999为组ID 也可以不指定

sudo usermod -aG dockerroot username

sudo usermod -aG docker username

检查一下是否有效 cat /etc/group

用户退出登录或者重启docker-daemon使权限生效

sudo systemctl restart docker

运行docker info查看是否生效

如果提示get权限不足，修改/var/run/docker.sock权限即可

sudo chmod a+rw /var/run/docker.sock