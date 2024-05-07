---
title: "Ubuntu20.04 LTS编译python3.7"
date: 2021-08-06T19:29:05+08:00
draft: true
categories:
  - python
---

# ubuntu20.04 LTS编译 [python3.7.1](https://www.python.org/downloads/release/python-371/)


## 安装编译前依赖包

- `sudo apt-get install -y build-essential libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev zlib1g-dev gcc make
  `

## 编译前配置

- `sudo ./configure --enable-optimizations --prefix=/usr/local/bin/python3.7`

- --prefix指定安装位置

## 编译安装

- `make`

- `sudo make install`

## 安装virtualenv虚拟环境来管理python版本

- `sudo apt install python3-pip`
- `pip install virtualenv`
- `pip install virtualenvwrapper`
- `mkdir .virtualenvs`

## vim .zhsrc

```shell
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=~/.local/bin/virtualenv
source ~/.local/bin/virtualenvwrapper.sh
```

- `source .zshrc`

## 创建python3.7虚拟环境

- `mkvirtualenv -p mkvirtualenv -p /usr/local/bin/python3.7/bin/python3.7 py3.7`