---
title: "分析FastApi中三种状态存储机制"
description: 
date: 2025-01-08T15:06:15+08:00
draft: false
categories:
  - fastapi
tags:
  - fastapi
---
<!--more-->

# 分析 FastAPI 中的三种状态存储机制

### 1. 生命周期和作用域分析:
- app.state: 应用级别，整个应用生命周期
- request.scope['app'].state: 同 app.state，是通过请求获取的应用状态引用
- request.state: 请求级别，单个请求生命周期

### 2. 数据持久性:

- app.state: 持久存储，应用启动到关闭
- request.scope['app'].state: 与 app.state 共享同一存储空间
- request.state: 临时存储，请求结束即销毁

### 3. 数据共享范围:

- app.state: 所有请求共享
- request.scope['app'].state: 所有请求共享
- request.state: 仅当前请求可访问

### 4. 使用场景分析:

- app.state: 适合存储全局配置、连接池等
- request.scope['app'].state: 在中间件中访问应用状态
- request.state: 适合存储请求特定的临时数据

## 详细介绍

### 1. app.state

- 范围: 应用全局范围
- 生命周期: 整个应用程序的生命周期(从启动到关闭)
- 适用场景
  - 数据库连接
  - 缓存
  - 全局配置
  - 共享资源

- 示例:

```python
app.state.db = database
app.state.redis = redis_client
app.state.config = config

async def some_func(request: Request)
  db = request.app.state.db
```

### 2. request.scope["app"].state

- 范围: 与app.state 相同
- 生命周期: 与app.state相同
- 特点:
  - 实际上就是app.state的另一种访问方式
  - 主要在中间件使用

- 示例:

```python

async def middleware(request: Reqeust, call_next):
  # 通过request.scope["app"] 访问应用实例
  db = request.scope["app"].state.db
  return await call_next(request)

```

### 3. request.state

- 范围: 单个请求范围
- 生命周期: 仅在当前请求的生命周期内
- 适用场景:
  - 请求级别的临时数据
  - 中间件传递数据给路由处理器
  - 用户认证信息

- 示例:

```python

async def auth_middleware(request: Request, call_next):
    # 在中间件中设置请求状态
    request.state.user = current_user
    return await call_next(request)

@app.get("/api/profile")
async def profile(request: Request):
    # 在路由处理器中访问请求状态
    user = request.state.user

```

## 代码示例:

### 1. 应用级别全局状态

```python

# 使用 app.state 存储全局资源
app.state.db_pool = db_pool
app.state.cache = cache_client

```

### 2. 中间件中的状态访问

``` python

async def middleware(request: Request, call_next):
    # 访问全局资源
    db = request.scope['app'].state.db_pool
    # 设置请求级别状态
    request.state.user = current_user
    return await call_next(request)

```

### 3. 请求级别状态

```python

@app.get("/api/data")
async def get_data(request: Request):
    # 访问请求状态
    user = request.state.user
    # 访问全局状态
    db = request.app.state.db_pool

```