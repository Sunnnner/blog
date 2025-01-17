---
title: "Docker 用户权限配置指南"
date: 2019-11-01T15:35:30+08:00
draft: false
categories:
  - docker
---
<!--more-->

## 1. 前置条件
- 已安装 Docker
- 具有 root 或 sudo 权限
- Docker 服务正在运行

## 2. 配置步骤

### 2.1 检查现有 Docker 组
```

# 查看是否存在 docker 组
sudo cat /etc/group | grep docker
```

### 2.2 创建 Docker 组
```

# 创建 docker 组（指定组ID）
sudo groupadd -g 999 docker

# 创建 docker 组（自动分配组ID）
sudo groupadd docker
```

### 2.3 将用户添加到 Docker 组
```

# 添加当前用户到 docker 组
sudo usermod -aG docker $USER

# 添加指定用户到 docker 组
sudo usermod -aG docker username

# 添加用户到 docker root 组（如果需要）
sudo usermod -aG dockerroot username
```

### 2.4 验证配置
```

# 查看组配置
cat /etc/group | grep docker

# 查看当前用户所属组
groups
```

### 2.5 使配置生效
```

# 重启 Docker 服务
sudo systemctl restart docker

# 或者重新加载 Docker daemon
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 2.6 权限修复（如果需要）
```

# 修改 docker.sock 文件权限
sudo chmod a+rw /var/run/docker.sock
```

## 3. 验证配置

### 3.1 测试 Docker 权限
```

# 查看 Docker 信息
docker info

# 运行测试容器
docker run hello-world
```

## 4. 安全建议

### 4.1 最佳实践
1. 仅将必要的用户添加到 docker 组
2. 定期审查 docker 组成员
3. 避免使用 `chmod a+rw /var/run/docker.sock`（除非必要）
4. 使用更细粒度的权限控制

### 4.2 权限说明
- docker 组成员等同于 root 权限
- 需要谨慎管理 docker 组成员
- 建议使用最小权限原则

## 5. 故障排除

### 5.1 常见问题
```

# 权限不足错误
Got permission denied while trying to connect to the Docker daemon socket

# 解决方案
1. 确认用户在 docker 组中
2. 重新登录用户会话
3. 重启 Docker 服务
```

### 5.2 检查清单
- [ ] 用户已添加到 docker 组
- [ ] Docker 服务已重启
- [ ] 用户已重新登录
- [ ] docker.sock 权限正确
- [ ] SELinux 配置正确（如果启用）

## 6. 命令参考

### 6.1 用户和组管理
```

# 创建新组
sudo groupadd [options] groupname

# 修改用户组
sudo usermod [options] username

# 查看用户组
groups [username]
```

### 6.2 Docker 服务管理
```

# 查看服务状态
sudo systemctl status docker

# 启动服务
sudo systemctl start docker

# 停止服务
sudo systemctl stop docker

# 重启服务
sudo systemctl restart docker
```