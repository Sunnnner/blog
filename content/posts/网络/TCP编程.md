---
title: "网络协议与抓包分析"
description: 
date: 2022-07-12T14:37:53+08:00
draft: false
categories:
  - network
tags:
  - tcp
---
<!--more-->

## 1. 网络抓包基础

### 1.1 Wireshark过滤器
```


# IP地址过滤
ip.addr == 192.168.1.1
ip.src == 192.168.1.1    # 源IP
ip.dst == 192.168.1.1    # 目标IP

# 端口过滤
udp.port == 53
tcp.port == 80
tcp.srcport == 80        # 源端口
tcp.dstport == 80        # 目标端口

# 组合过滤
ip.addr == 192.168.1.1 and tcp.port == 80
```

## 2. 网络架构模式

### 2.1 常见架构模式对比
| 模式 | 特点 | 应用场景 |
|------|------|----------|
| BS (Browser/Server) | 基于浏览器，跨平台，维护方便 | Web应用 |
| CS (Client/Server) | 性能好，体验佳，需要安装 | 桌面应用 |

### 2.2 数据传输方向
```


# 上传操作
本地(读取) -> 远程(写入)

# 下载操作
远程(读取) -> 本地(写入)
```

## 3. TCP vs UDP

### 3.1 基本特征对比
| 特性 | TCP | UDP |
|------|-----|-----|
| 连接方式 | 面向连接 | 无连接 |
| 首部大小 | 20字节 | 8字节 |
| 通信模式 | 点对点 | 一对一/一对多/多对多 |
| 传输方式 | 字节流 | 数据报 |
| 可靠性 | 高 | 低 |
| 传输速度 | 慢 | 快 |

### 3.2 TCP可靠传输机制
1. 三次握手
2. 数据确认
3. 重传机制
4. 拥塞控制

### 3.3 TCP服务器实现
```


import socket

def create_tcp_server(host='0.0.0.0', port=8888):
    # 1. 创建套接字
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # 2. 绑定地址
    server_socket.bind((host, port))
    
    # 3. 开启监听
    server_socket.listen(5)
    
    while True:
        try:
            # 4. 等待连接
            client_socket, client_addr = server_socket.accept()
            
            # 5. 数据收发
            while True:
                # 接收数据
                data = client_socket.recv(1024)
                if not data:
                    break
                    
                # 发送数据
                client_socket.send(data)
                
        except Exception as e:
            print(f"Error: {e}")
        finally:
            # 关闭客户端连接
            client_socket.close()
    
    # 关闭服务器
    server_socket.close()
```

## 4. TFTP (简单文件传输协议)

### 4.1 特点
1. 简单的文件传输协议
2. 基于UDP协议
3. 支持上传和下载
4. 无认证机制

### 4.2 基本操作
```


# TFTP客户端示例
from tftpy import TftpClient

def tftp_download(server, filename):
    client = TftpClient(server, 69)
    client.download(filename, filename)

def tftp_upload(server, filename):
    client = TftpClient(server, 69)
    client.upload(filename, filename)
```

## 5. 网络编程最佳实践

### 5.1 TCP服务器优化
1. 使用非阻塞IO
2. 实现超时机制
3. 错误处理
4. 资源管理

```


import socket
import select

def optimized_tcp_server(host='0.0.0.0', port=8888):
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.setblocking(False)
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind((host, port))
    server.listen(5)
    
    inputs = [server]
    outputs = []
    
    while inputs:
        readable, writable, exceptional = select.select(inputs, outputs, inputs)
        # 处理可读socket
        for sock in readable:
            if sock is server:
                client, addr = sock.accept()
                client.setblocking(False)
                inputs.append(client)
            else:
                try:
                    data = sock.recv(1024)
                    if data:
                        # 处理数据
                        pass
                    else:
                        inputs.remove(sock)
                        sock.close()
                except Exception:
                    inputs.remove(sock)
                    sock.close()
```

### 5.2 安全建议
1. 输入验证
2. 超时控制
3. 资源限制
4. 错误处理
5. 日志记录

### 5.3 性能优化
1. 使用连接池
2. 实现缓存机制
3. 合理的缓冲区大小
4. 异步处理