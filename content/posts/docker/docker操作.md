---
title: "Docker & Docker Compose 使用指南"
date: 2019-10-08T14:19:00+08:00
draft: false
categories:
  - docker
---
<!--more-->

## 1. 基本命令

### 1.1 Docker 命令
```bash
# 构建镜像
docker build -t image_name:tag .

# 查看所有容器
docker ps -a

# 查看所有镜像
docker images

# 停止容器
docker stop container_id

# 启动容器
docker start container_id
```

### 1.2 Docker Compose 命令
```bash
# 启动服务
docker-compose up
docker-compose up -d  # 后台运行

# 停止服务
docker-compose down

# 查看服务日志
docker-compose logs
docker-compose logs -f  # 实时日志
```

## 2. 清理命令

### 2.1 删除容器
```bash
# 删除所有容器
docker rm $(docker ps -a -q)

# 删除指定容器
docker rm container_id
```

### 2.2 删除镜像
```bash
# 删除所有镜像
docker rmi $(docker images -q)

# 删除未标记镜像
docker rmi $(docker images -q | awk '/^<none>/ { print $3 }')

# 删除包含关键字的镜像
docker rmi --force $(docker images | grep keyword | awk '{print $3}')
```

## 3. Docker Compose 配置

### 3.1 基本结构
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    restart: always
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      - NODE_ENV=production
    links:
      - db
      - redis

  db:
    image: mysql:5.7
    restart: always
    volumes:
      - ./data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=secret
      - MYSQL_DATABASE=myapp

  redis:
    image: redis:latest
    restart: always
```

### 3.2 主要配置项说明

| 配置项 | 说明 | 示例 |
|--------|------|------|
| services | 定义服务 | web, db, redis |
| image | 指定镜像 | nginx:latest |
| restart | 重启策略 | always, no, on-failure |
| command | 启动命令 | python app.py |
| volumes | 挂载目录 | - ./local:/container |
| environment | 环境变量 | - KEY=value |
| ports | 端口映射 | - "8080:80" |
| links | 服务连接 | - db |

## 4. 最佳实践

### 4.1 镜像管理
1. 使用具体的标签版本，避免使用latest
2. 定期清理未使用的镜像
3. 使用多阶段构建减小镜像大小
4. 合理使用.dockerignore文件

### 4.2 容器管理
```bash
# 查看容器资源使用
docker stats

# 清理所有停止的容器
docker container prune

# 清理所有未使用的数据卷
docker volume prune
```

### 4.3 Docker Compose 使用建议
1. 将敏感信息存储在.env文件中
2. 使用docker-compose.override.yml进行本地开发
3. 合理设置重启策略
4. 使用健康检查确保服务可用

## 5. 常见问题解决

### 5.1 容器无法停止
```bash
# 强制停止容器
docker kill container_id

# 强制停止所有容器
docker kill $(docker ps -q)
```

### 5.2 磁盘空间问题
```bash
# 清理所有未使用的对象
docker system prune -a

# 查看Docker使用的磁盘空间
docker system df
```

## 6. 安全建议
1. 定期更新基础镜像
2. 使用非root用户运行容器
3. 限制容器资源使用
4. 使用私有镜像仓库
5. 实施容器安全扫描