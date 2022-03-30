---
title: "K8s基础操作"
date: 2019-11-02T15:36:16+08:00
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

k8s获取所有运行的podskubectl get pods --all-namespaces -o wide

获取当前集群名称kubectl get pods -o wide

当前etcd中的注册的宿主机的pod地址网段信息etcdctl ls /kube-centos/network/subnets

而每个node上的Pod子网是根据我们在安装flannel时配置来划分的，在etcd中查看该配置etcdctl get /kube-centos/network/config

