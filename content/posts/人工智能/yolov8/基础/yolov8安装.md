---
title: "yolov8安装"
date: 2023-05-10T10:52:21+08:00
draft: false
categories:
  - 人工智能
tags:
  - yolov8
---

<!--more-->

*   首先安装conda 使用conda3.8的python虚拟环境创建
*   安装cuda\`<https://developer.nvidia.com/cuda-toolkit-archive>\`推荐安装稳定版本
*   安装cudnn[`https://developer.nvidia.com/rdp/cudnn-archive`](https://developer.nvidia.com/rdp/cudnn-archive)
*   cudnn教程 \`<https://blog.csdn.net/jhsignal/article/details/111401628>\`
*   安装pytorch \`<https://pytorch.org/get-started/locally/>\`
*   clone yolov8项目 \`git clone --depth=1 <https://gitclone.com/github.com/ultralytics/ultralytics.git>\`
*   安装 requirements  \`pip install -r requirements.txt -i <https://mirrors.bfsu.edu.cn/pypi/web/simple/`>
*   安装`ultralytics 进入此文件夹执行` python setup.py install&#x20;
*   下载权重 <https://github.com/ultralytics/assets/releases>