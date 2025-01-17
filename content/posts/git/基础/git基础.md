---
title: "Git 使用指南"
description: 
date: 2021-07-12T14:37:29+08:00
draft: false
categories:
  - github
tags:
  - git
---
<!--more-->
## 1. 基础命令

### 1.1 仓库初始化与克隆
```bash
# 初始化Git仓库
git init

# 克隆远程仓库
git clone <repository_url>
```

### 1.2 基本操作
```bash
# 查看仓库状态
git status

# 添加文件到暂存区
git add <file>     # 添加指定文件
git add .          # 添加所有文件

# 提交更改
git commit -m "提交说明"

# 推送到远程仓库
git push

# 拉取最新代码
git pull

# 查看差异
git diff          # 查看未暂存的更改
git diff --staged # 查看已暂存的更改
```

### 1.3 查看历史
```bash
# 查看提交历史
git log
git log --pretty=oneline  # 简洁模式
git log --graph          # 图形化显示
git reflog              # 查看命令历史
```

## 2. 版本控制

### 2.1 版本回退
```bash
# HEAD说明
HEAD      # 当前版本
HEAD^     # 上一个版本
HEAD^^    # 上上个版本
HEAD~n    # 前n个版本

# 回退版本
git reset --hard HEAD^
git reset --hard <commit_id>
```

### 2.2 工作区和暂存区
```bash
# 查看工作区状态
git status

# 撤销工作区修改
git checkout -- <file>

# 撤销暂存区修改
git reset HEAD <file>

# 删除文件
git rm <file>
git commit -m "删除文件"
```

## 3. 远程仓库操作

### 3.1 配置SSH密钥
```bash
# 生成SSH密钥
ssh-keygen -t rsa -C "your_email@example.com"

# 密钥位置
# Windows: C:\Users\用户名\.ssh\id_rsa.pub
# Linux/Mac: ~/.ssh/id_rsa.pub
```

### 3.2 远程仓库管理
```bash
# 添加远程仓库
git remote add origin <repository_url>

# 首次推送
git push -u origin master

# 后续推送
git push origin master

# 查看远程仓库信息
git remote -v

# 删除远程仓库链接
git remote rm origin
```

## 4. 分支管理

### 4.1 基本操作
```bash
# 创建分支
git branch <branch_name>

# 切换分支
git checkout <branch_name>
# 或使用新命令
git switch <branch_name>

# 创建并切换分支
git checkout -b <branch_name>
# 或使用新命令
git switch -c <branch_name>

# 查看分支
git branch

# 合并分支
git merge <branch_name>

# 删除分支
git branch -d <branch_name>
```

### 4.2 冲突解决
```bash
# 查看冲突文件
git status

# 解决冲突后提交
git add <conflict_file>
git commit -m "解决冲突"
```

## 5. 最佳实践

### 5.1 提交规范
- 使用清晰的提交信息
- 每次提交专注于一个改动
- 定期提交代码
- 避免提交临时文件

### 5.2 分支策略
- master/main: 主分支，保持稳定
- develop: 开发分支
- feature/*: 功能分支
- hotfix/*: 紧急修复分支

### 5.3 安全建议
1. 定期备份仓库
2. 保护好SSH密钥
3. 谨慎使用force push
4. 及时更新Git客户端

## 6. 常见问题解决

### 6.1 撤销操作
```bash
# 撤销最后一次提交
git reset --soft HEAD^

# 撤销所有本地改动
git reset --hard HEAD
git clean -fd

# 撤销某次提交
git revert <commit_id>
```

### 6.2 临时保存
```bash
# 保存当前工作进度
git stash

# 查看保存的进度
git stash list

# 恢复进度
git stash pop
```