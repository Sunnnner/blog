---
title: "使用minikube创建集群"
date: 2019-11-11T15:38:29+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["kubernete"]
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

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_1.5.2.deb \ && sudo dpkg -i minikube_1.5.2.deb

系统管理程序设置验证系统是否启用虚拟化 egrep -q 'vmx|svm' /proc/cpuinfo && echo yes || echo no 如果启用则需要关闭虚拟化

minikube servion查看版本信息

minikube start启动

查看集群信息kubectl cluster-info
