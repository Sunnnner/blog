---
title: "git基础"
description: 
date: 2022-07-12T14:37:29+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---


# Linux的发行版
- ubtnutu
- redhat
- gebtoo
- gentoo



# linux最最基本的命令
- `ls`: 列出所在目录的文件
- `cd`：进入根目录
- `cd 目录名`：进入目录名/
-  `mkdir 文件夹的名字`: 新建文件夹
  

# vi基本命令
-`i`进入编辑模式
-`esc`退出编辑模式
-`：`shift+:进入控制模式
-`wq`:保存退出
-`w`:保存
-`q`:退出
-`dd`:删除一行

# git基本命令
-`git init`初始话一个git仓库
- `git clone项目地址`
- `cd项目地址`
- `vim notes.md`编辑note.md文档
- `git add *`告诉git把文件添加到仓库
- `git commit -m"注释"`告诉git把文件提交到仓库
- `git push`
- `git diff`：查看提交了些什么
- `git log`:查看提交历史
- `git pull`：拉下来最新的代码
- `git log --pretty=oneline`git log参数简洁显示最近提交的信息
 
 #  git 时光机总总结
 
- `HEAD`指向当前版本
- `HEAD^`指向前一个版本^^前一个的前一个版本
- `id`git log 前面的psh
- `git log`查看当前提交的历史
- `git log --pretty=oneline`常看当前提交的历史简洁版
- `git reset --hard commit_id`commit_id代表指向的HEAD^
- `git reflog`查看命令历史进行回到未来
- # git 修改总结
- `git add`第一次修改提交只是储存在暂存区没有进行commit
- `git add`第二次修改后不进行提交存放在工作区
- `git add`第三次提交第二次的修改合并第一次的提交
- `git commit`第四次进行commit
- # git 的撤销操作
- `git checkout -- file`回到最后一次编辑位置
- 
- `git reset HEAD file`如果你不小心add进入了暂存区你就要用这个回滚到head的地方然后在执行checkout
- `git rm`用于删除仓库文件
- # 仓库分布式部署流程
- `$ ssh-keygen -t rsa -C "youremail@example.com"`创建SSH Key
- `Create a new repo`创建一个新的仓库
- `根据页面提示在终端执行一边代码`
- `$ git remote add origin git@github.com:自己的git用户民/learngit.git`以后推送设置
- `$ git push -u origin master`推送到git第一次推送使用-u
- `$ git push origin master`
- 以后直接推送
- `git remote add origin git@server-name:path/repo-name.git`要关联一个远程库
- ``