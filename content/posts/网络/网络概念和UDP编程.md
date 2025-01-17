---
title: "网络概念与UDP编程"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - python
tags:
  - socket
---

## 1. 网络基础概念

### 1.1 网络定义
- 电路网络：由电子元件组成的信号传输系统
- 三大网络：
  1. 电信网络
  2. 有线电视网络
  3. 计算机网络（互联网）

### 1.2 网络层次
```

网络体系结构：
- 应用层
- 传输层
- 网际层（网络层）
- 网络接口层（链路层）
```

## 2. 本地服务器配置

### 2.1 快速启动HTTP服务
```

# Python 2
python -m SimpleHTTPServer 8080

# Python 3
python -m http.server 8080

# 访问地址
http://127.0.0.1:8080  # 本机回环地址
http://localhost:8080   # 本机域名
```

## 3. Socket编程基础

### 3.1 Socket类型
```

import socket

# 创建Socket对象
# 本地进程通信
unix_socket = socket.socket(socket.AF_UNIX)

# 网络通信
inet_socket = socket.socket(socket.AF_INET)

# 协议类型
tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  # TCP协议
udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)   # UDP协议
```

### 3.2 Socket地址族
| 地址族 | 说明 | 用途 |
|--------|------|------|
| AF_UNIX | 本地通信 | 同一台计算机进程间通信 |
| AF_INET | IPv4网络 | 互联网通信 |
| AF_INET6 | IPv6网络 | 下一代互联网通信 |

## 4. UDP通信

### 4.1 UDP特点
1. 无连接通信协议
2. 支持广播发送
3. 数据包大小限制（64KB）
4. 不保证可靠传输
5. 不保证数据顺序

### 4.2 基本UDP通信示例
```

import socket

# 创建UDP Socket
udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# 绑定本地地址和端口
local_addr = ('', 8888)  # 空字符串表示本机所有IP
udp_socket.bind(local_addr)

# 发送数据
target_addr = ('192.168.1.100', 8888)
message = "Hello, UDP!"
udp_socket.sendto(message.encode('utf-8'), target_addr)

# 接收数据
while True:
    data, addr = udp_socket.recvfrom(1024)  # 缓冲区大小1024字节
    print(f"从{addr}接收到: {data.decode('utf-8')}")

# 关闭Socket
udp_socket.close()
```

### 4.3 端口绑定
```

# 服务端绑定固定端口
server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server_socket.bind(('', 80))  # 绑定80端口

# 客户端使用随机端口
client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# 系统自动分配端口
```

## 5. 通信模式

### 5.1 通信方式对比
| 模式 | 特点 | 类比 |
|------|------|------|
| 单工 | 单向传输 | 广播 |
| 半双工 | 双向交替传输 | 对讲机 |
| 全双工 | 双向同时传输 | 电话 |

### 5.2 数据编解码
```

# 发送数据编码
message = "你好"
encoded_data = message.encode('utf-8')

# 接收数据解码
decoded_data = received_data.decode('utf-8')

# 支持的编码
encodings = ['utf-8', 'gb2312', 'ascii']
```

## 6. 最佳实践

### 6.1 Socket编程建议
1. 始终使用 with 语句管理socket
2. 设置适当的超时时间
3. 正确处理异常
4. 及时关闭不用的socket

### 6.2 示例代码
```

import socket

def create_udp_server(host='', port=8888):
    with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as server:
        server.bind((host, port))
        server.settimeout(60)  # 60秒超时
        try:
            while True:
                data, addr = server.recvfrom(1024)
                if not data:
                    break
                # 处理数据
                process_data(data, addr)
        except socket.timeout:
            print("服务器超时")
        except Exception as e:
            print(f"发生错误: {e}")
```

### 6.3 安全建议
1. 验证数据来源
2. 限制数据包大小
3. 实现超时机制
4. 做好错误处理
5. 考虑加密传输