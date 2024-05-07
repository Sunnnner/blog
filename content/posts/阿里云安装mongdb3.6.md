---
title: "阿里云安装mongodb"
description: 
date: 2022-07-12T14:37:29+08:00
draft: true
categories:
  - aliyun
tags:
  - mongodb
---
- 第1步：导入公钥
- sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5 
- 第2步：创建源文件
- ubuntu 14.0
- echo "deb [ arch=amd64 ] http://mirrors.aliyun.com/mongodb/apt/ubuntu trusty/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list  
- ubuntu 16
- echo "deb [ arch=amd64,arm64 ] http://mirrors.aliyun.com/mongodb/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list  
- 第3步：
sudo apt-get update  
- 第4步：

- >安装最新版本
- sudo apt-get install -y mongodb-org  
- >安装指定版本3.6.2
- sudo apt-get install -y mongodb-org=3.6.2 mongodb-org-server=3.6.2 mongodb-org-shell=3.6.2 mongodb-org-mongos=3.6.2 mongodb-org-tools=3.6.2  