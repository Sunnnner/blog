---
title: "Docker Frp内网穿透教程"
description: 
date: 2024-10-11T15:16:05+08:00
draft: false
categories:
  - docker
tags:
  - docker-compose
  - frp
---
<!--more-->

# frp 使用 Docker 容器进行内网穿透

## 提前准备

- 两台公网 IP 主机（轻量型服务器即可，一台备案主机可使用域名，另一台作为中转）
- 一个备案域名（无备案可使用国外主机）
- 一台内网主机

## frpc 客户端内网主机配置

### Docker Compose 文件

```yaml
version: '3'
services:
  app:
    image: snowdreamtech/frpc:alpine
    restart: always
    volumes:
      - ./frpc.toml:/etc/frp/frpc.toml
    network_mode: host
```

### frpc.toml 文件

```toml
serverAddr = "117.72.66.33"  # 连接服务端的地址（公网主机 IP 地址）
serverPort = 7000             # 连接服务端的端口，默认为 7000
auth.token = "xxx"            # 身份验证令牌，frpc 要与 frps 一致
log.to = "/usr/local/frp/frps.log"  # 日志相关
log.level = "info"
log.maxDays = 3

# 代理配置
[[proxies]]
name = "web01"  # 代理名称
type = "tcp"    # 代理类型
localIP = "127.0.0.1"  # 被代理的本地服务 IP
localPort = 8000       # 被代理的本地服务端口
remotePort = 8000      # 服务端绑定的端口
```

启动客户端：

```bash
docker-compose up -d
```

## frps 服务端公网主机配置

### Docker Compose 文件

```yaml
version: '3'
services:
  app:
    image: snowdreamtech/frps:alpine
    restart: always
    volumes:
      - ./frps.toml:/etc/frp/frps.toml
    network_mode: host
```

### frps.toml 文件

```toml
bindAddr = "0.0.0.0"         # 服务端监听地址
bindPort = 7000              # 服务端与客户端通信端口
kcpBindPort = 7000           # 服务端监听 KCP 协议端口
webServer.addr = "0.0.0.0"   # webServer 后台管理地址
webServer.port = 7002         # webServer 后台管理端口
webServer.user = "root"      # webServer 后台登录用户名
webServer.password = "root"   # webServer 后台登录密码
auth.token = "xxx"           # 身份验证令牌
log.to = "/usr/local/frp/frps.log"  # 日志相关
log.level = "info"
log.maxDays = 3
```

启动服务端：

```bash
docker-compose up -d
```

## 备案服务器配置

由于 frps 服务器没有备案，无法直接使用域名进行访问。我们可以使用另一台备案的机器来实现反向代理，并且使用 Docker 进行 HTTPS 证书的自动申请和续期。

### 所需镜像

- `alpine:latest`：占位镜像，用于提供域名供 acme 自动申请。
- `nginxproxy/nginx-proxy:alpine`：Nginx 反向代理。
- `nginxproxy/acme-companion:2.2`：自动申请和续签 HTTPS 证书。

### Docker Compose 文件

```yaml
version: '3'
services:
  dj-gpt:
    image: alpine:latest
    restart: always
    command: tail -f /dev/null
    environment:
      - VIRTUAL_HOST=xxx.com.cn
      - LETSENCRYPT_HOST=xxx.com.cn
      - LETSENCRYPT_EMAIL=xx@email.com

  nginx:
    image: nginxproxy/nginx-proxy:alpine
    restart: always
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
      - /srv/proxy/certs:/etc/nginx/certs:ro
      - /srv/proxy/vhost.d:/etc/nginx/vhost.d
      - /srv/proxy/html:/usr/share/nginx/html
    container_name: nginx-proxy
    ports:
      - 80:80
      - 443:443
    logging:
      driver: json-file
      options:
        max-size: "20m"
        max-file: "1"

  https:
    image: nginxproxy/acme-companion:2.2
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - /srv/proxy/certs:/etc/nginx/certs
      - /srv/proxy/vhost.d:/etc/nginx/vhost.d
      - /srv/proxy/html:/usr/share/nginx/html
      - /srv/proxy/acme:/etc/acme.sh
    container_name: nginx-proxy-acme
    environment:
      - DEFAULT_EMAIL=xx@email.com
      - NGINX_PROXY_CONTAINER=nginx-proxy
    logging:
      driver: json-file
      options:
        max-size: "20m"
        max-file: "1"
```

### 反向代理配置

在 Nginx 容器的 `/srv/proxy/vhost.d` 中创建一个文件，文件名为 `${VIRTUAL_HOST}_location_override`，例如 `xxx.com.cn_location_override`，文件内容如下：

```conf
location / {
    proxy_pass http://xxx:8000;  # frps 公网电脑可以访问内网服务的 IP 及端口号
}
```

### 完成配置

至此，启动容器后访问 `xxx.com.cn` 即可访问你的内网服务。虽然配置流程较繁琐，但通过该方案可以实现 证书 的自动申请与续期。