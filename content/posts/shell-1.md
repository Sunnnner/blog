---
title: "Shell 1"
date: 2019-08-15T11:18:47+08:00
draft: true
categories:
  - shell
---

什么是shell

    最早期运行在unix上的shell是Bourne shell（sh），其实shell我们都知道是一个内核，里面集成了很多命令，shell负责和底层硬件打交道。前面我们介绍的这些命令，可以说是shell命令。shell程序的入口一般是在终端输入一些相关命令，然后不需要编译，直接去解释和运行命令的结果，给出相关反馈到终端上面。所以，一句话来理解，shell是一个很多命令的集合，一个内核
<!--more-->
什么是bash

    bash 是一个为GNU计划编写的Unix shell。它的名字是一系列缩写：Bourne-Again SHell — 这是关于Bourne shell（sh）的一个双关语（Bourne again / born again）.Bash (GNU Bourne-Again Shell) 是许多Linux发行版的默认Shell。事实上，还有许多传统UNIX上用的Shell，例如tcsh、csh、ash、bsh、ksh等等，Shell Script大致都类同，当您学会一种Shell以后，其它的Shell会很快就上手，大多数的时候，一个Shell Script通常可以在很多种Shell上使用。所以，这就是我们为什么要使用bash脚本的原因。我们接下来的shell脚本都是基于bash。

什么是shell脚本

    前面我们写过了一个shell脚本，shell脚本就是通过一些相关shell命令的组合来达到完成一个任务的文件，文件一般是以,sh结尾。

写一个shell脚本，在终端打印hello shell

```shell
touch hello.sh
code hello.sh
#!  /bin/bash

echo 'Hello world'

提高权限 -rwxr-xr-x
chmod +x hellp.sh
```