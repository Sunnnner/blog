---
title: "Linux 命令速查手册"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - linux
---
<!--more-->

## 1. 基础终端操作

### 1.1 终端快捷键
| 快捷键 | 功能 |
|--------|------|
| `Ctrl + L` | 清屏 |
| `Ctrl + D` | 关闭终端 |
| `Ctrl + Alt + T` | 打开新终端 |
| `Ctrl + Shift + T` | 新建终端标签页 |
| `Alt + 1,2,3,4` | 切换终端窗口 |
| `Ctrl + -/+` | 调整字体大小 |
| `↑/↓` | 浏览历史命令 |

### 1.2 基本命令
| 命令 | 说明 | 常用选项 |
|------|------|----------|
| `pwd` | 显示当前目录 | - |
| `which` | 查看命令位置 | - |
| `ls` | 列出目录内容 | `-l`(列表) `-h`(人性化) `-a`(全部) |
| `tree` | 显示目录树结构 | - |

## 2. 文件和目录操作

### 2.1 目录操作
```bash
# 创建目录
mkdir dirname           # 创建单个目录
mkdir -p a/b/c         # 创建递归目录

# 删除目录
rmdir dirname          # 删除空目录
rm -r dirname          # 递归删除目录及内容
```

### 2.2 文件操作
```bash
# 创建文件
touch filename         # 创建空文件
gedit filename        # 使用编辑器创建/编辑

# 复制文件
cp source dest        # 复制文件
cp -r source dest     # 递归复制目录

# 移动/重命名
mv source dest        # 移动或重命名

# 删除文件
rm filename           # 删除文件
rm -f filename       # 强制删除
```

### 2.3 文件权限
```bash
# 权限说明
r (4) - 读权限
w (2) - 写权限
x (1) - 执行权限

# 修改权限
chmod 755 file       # 数字方式
chmod u+x file      # 符号方式
```

## 3. 文件查找和内容搜索

### 3.1 find命令
```bash
find / -name "*.py"          # 按名称查找
find / -size +2M            # 按大小查找
find / -perm 0777          # 按权限查找
```

### 3.2 grep命令
```bash
grep "pattern" file         # 基本搜索
grep -n "pattern" file     # 显示行号
grep -v "pattern" file     # 反向匹配
grep -i "pattern" file     # 忽略大小写
```

## 4. 文件压缩和解压

### 4.1 tar 命令
```bash
# .tar 文件
tar -cvf output.tar files    # 打包
tar -xvf file.tar           # 解包

# .tar.gz 文件
tar -zcvf output.tar.gz files    # 压缩
tar -zxvf file.tar.gz           # 解压

# .tar.bz2 文件
tar -jcvf output.tar.bz2 files   # 压缩
tar -jxvf file.tar.bz2          # 解压
```

### 4.2 zip/unzip
```bash
zip -r output.zip files     # 压缩
unzip file.zip             # 解压
```

## 5. 进程管理

### 5.1 进程查看
```bash
ps aux                     # 查看所有进程
top                       # 动态进程监控
htop                      # 增强版进程监控
```

### 5.2 进程控制
```bash
kill pid                  # 终止进程
kill -9 pid              # 强制终止
```

## 6. 用户和权限管理

### 6.1 用户管理
```bash
useradd username         # 创建用户
userdel username        # 删除用户
passwd username         # 设置密码
su username            # 切换用户
```

### 6.2 用户组管理
```bash
groupadd groupname      # 创建用户组
groupdel groupname     # 删除用户组
usermod -g group user  # 修改用户主组
usermod -aG group user # 添加附加组
```

## 7. 系统信息查看

### 7.1 系统资源
```bash
df -h                   # 磁盘使用情况
du -sh directory       # 目录大小
free -h               # 内存使用情况
```

### 7.2 网络信息
```bash
ifconfig               # 网卡信息
ip addr               # IP地址信息
netstat -tuln         # 端口监听情况
```

## 注意事项
1. 使用 `rm` 命令时要特别小心，建议使用 `-i` 选项
2. 重要操作建议先备份
3. 系统命令使用 `sudo` 需要管理员权限
4. 修改系统配置前先备份原文件

## 常用技巧
1. 使用 Tab 键自动补全命令和路径
2. 使用 `history` 查看命令历史
3. 使用 `man` 或 `--help` 查看命令帮助
4. 使用通配符 `*` 和 `?` 批量操作文件