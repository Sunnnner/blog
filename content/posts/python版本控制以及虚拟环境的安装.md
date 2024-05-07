---
title: "Python版本控制以及虚拟环境的安装"
date: 2019-09-01T11:22:47+08:00
draft: true
categories:
  - python
tags:
  - python虚拟环境
---
<!--more-->
## 虚拟环境安装

    当然首先你先去官网下载Python3.6 注意不是3.7 它现在还不兼容
    下载好了之后安装这是Mac的路径包
    随后配置下面的语句
    pip3 install virtualenv
    当然这里你要建立一个文件夹来存放你的虚拟环境
    我这里是workspace
    mkdir workspace

虚拟环境管理包

    pip3 install virtualenvwrapper

## 虚拟环境文件夹

export WORKON_HOME='~/workspace'

## 虚拟环境Python需要Python版本进行安装

VIRTUALENVWRAPPER_PYTHON="/Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6"

## 使用哪个Python环境的虚拟环境安装包

source  /Library/Frameworks/Python.framework/Versions/3.6/bin/virtualenvwrapper.sh

Python环境配置

    因为TensorFlow库的学习我安装虚拟环境可是我并不怎么会安装虚拟环境
    就擅自删除了Mac自带的Python版本使用网上的安装默认的版本Python3.6
    可是这是错误的决定安装了默认版本的3。6之后pip各种报错
    到最后我总结了一句话
    在.zshrc（如果你安装了oh_my_zsh）就加入这一条shell语句
    这条语句代表了你的默认Python变量的地址
## Python环境变量

export PATH="/Library/Frameworks/Python.framework/Versions/3.6/bin:${PATH}"