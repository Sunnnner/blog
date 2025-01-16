---
title: "Linux操作系统概述"
description: 
date: 2021-07-12T14:37:29+08:00
draft: false
categories:
  - liunx
---
<!--more-->


# Linux操作系统概述

## 发展历史
```markdown
1. UNIX诞生
- 1969年，Ken Thompson（肯·汤普逊）在贝尔实验室开发UNIX
- 最初用汇编语言编写
- 1973年，Dennis Ritchie（丹尼斯·里奇）开发C语言
- Thompson和Ritchie用C语言重写UNIX，奠定现代操作系统基础

2. UNIX分支
- BSD（Berkeley Software Distribution）
  * FreeBSD
  * OpenBSD
  * NetBSD
- System V
  * IBM AIX
  * Sun Solaris
  * HP-UX

3. MINIX诞生
- Andrew S. Tanenbaum开发
- 用于教学的类UNIX系统
- 启发了Linux的诞生

4. Linux诞生
- 1991年，Linus Torvalds（林纳斯·托瓦兹）开发
- 最初只支持386处理器
- 开源社区共同开发，支持多种硬件平台
```

## Linux发行版
```markdown
1. 主流发行版
- Debian系：
  * Ubuntu
  * Debian
  * Linux Mint
- Red Hat系：
  * Red Hat Enterprise Linux
  * CentOS
  * Fedora
- 其他：
  * SUSE Linux
  * Arch Linux
  * Gentoo

2. 特点比较
- Ubuntu：
  * 用户友好
  * 适合新手
  * 桌面环境优秀
- Red Hat：
  * 企业级应用
  * 稳定性好
  * 技术支持完善
- SUSE：
  * 企业应用
  * 系统管理工具完善
```

## 系统架构
```markdown
1. 核心组件
- 内核（Kernel）：
  * 系统核心程序
  * 硬件资源管理
  * 提供系统调用接口
  * 进程调度
  * 内存管理
  * 文件系统

2. 系统层次
- 硬件层
- 内核层
- Shell层
- 应用层

3. 重要概念
- 多用户
- 多任务
- 文件系统层次结构
```

## 基本命令语法
```markdown
1. 路径相关
- cd /     # 切换到根目录
- cd 或 cd ~  # 切换到用户家目录
- cd ..    # 切换到上级目录
- cd -     # 切换到上次访问的目录
- pwd      # 显示当前目录

2. 特殊符号
- /  # 根目录，目录分隔符
- \  # 转义字符
- -  # 命令选项标识符
- _  # 文件名中的连接符
- |  # 管道符，连接多个命令
- >  # 重定向输出符
- >>  # 追加重定向
- &  # 后台运行
- ;  # 命令分隔符

3. 目录结构
- /bin     # 基本命令目录
- /boot    # 启动文件目录
- /dev     # 设备文件目录
- /etc     # 配置文件目录
- /home    # 用户主目录
- /lib     # 系统库文件
- /root    # root用户主目录
- /usr     # 应用程序目录
- /var     # 变动文件目录
```

## 命令使用规范
```markdown
1. 基本格式
command [options] [arguments]

2. 命令类型
- 内部命令（Shell内置）
- 外部命令（独立的可执行文件）

3. 常用操作
- 命令自动补全（Tab键）
- 命令历史（上下箭头）
- 命令别名（alias）

4. 帮助获取
- man command    # 查看命令手册
- command --help # 查看命令帮助
- info command   # 查看命令信息
```

## 重要概念
```markdown
1. 权限控制
- 用户（User）
- 组（Group）
- 权限（Permission）：读、写、执行

2. 进程管理
- 前台进程
- 后台进程
- 守护进程

3. 文件系统
- 文件类型
- 挂载点
- 链接（软链接、硬链接）
```

## 安全性
```markdown
1. 基本安全措施
- 用户认证
- 访问控制
- 系统日志
- 防火墙配置

2. SELinux
- 强制访问控制
- 安全策略
- 运行模式
```
