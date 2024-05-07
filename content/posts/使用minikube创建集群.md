---
title: "使用minikube创建集群"
date: 2019-11-11T15:38:29+08:00
draft: true
categories:
  - k8s
tags:
  - minikube
---
<!--more-->
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_1.5.2.deb \ && sudo dpkg -i minikube_1.5.2.deb

系统管理程序设置验证系统是否启用虚拟化 egrep -q 'vmx|svm' /proc/cpuinfo && echo yes || echo no 如果启用则需要关闭虚拟化

minikube servion查看版本信息

minikube start启动

查看集群信息kubectl cluster-info
