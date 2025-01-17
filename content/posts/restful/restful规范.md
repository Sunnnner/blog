---
title: "RESTful API 设计指南"
date: 2019-09-06T11:36:12+08:00
draft: false
categories:
  - python
tags:
  - api设计规范
---

## 1. 什么是RESTful

RESTful是一种软件架构风格，主要用于规范客户端与服务端的交互。它不是标准，而是一套设计原则和约束条件，帮助我们创建更优雅的API接口。

## 2. 核心原则

### 2.1 面向资源
- 使用名词表示资源
- URL中避免使用动词
- 资源应该是名词的复数形式

```

# 好的例子
GET /api/v1/users          # 获取用户列表
GET /api/v1/users/123      # 获取特定用户
POST /api/v1/users         # 创建用户

# 不好的例子
GET /api/v1/getUsers
POST /api/v1/createUser
PUT /api/v1/updateUser
```

### 2.2 HTTP方法
| 方法 | 用途 | 特点 |
|------|------|------|
| GET | 获取资源 | 安全且幂等 |
| POST | 创建资源 | 非幂等 |
| PUT | 更新资源（完整） | 幂等 |
| DELETE | 删除资源 | 幂等 |
| PATCH | 更新资源（部分） | 幂等 |

## 3. 设计规范

### 3.1 URL设计
```

# 版本号
/api/v1/resources

# 资源层级
/api/v1/users/{user_id}/orders/{order_id}

# 过滤、排序、分页
/api/v1/users?page=2&size=10
/api/v1/products?sort=price_desc
/api/v1/orders?status=pending
```

### 3.2 安全性
- 使用HTTPS协议
- 实现身份认证
- 使用OAuth2等授权机制
- 实施速率限制

### 3.3 状态码使用
```

# 常用状态码
200 OK              # 请求成功
201 Created         # 创建成功
204 No Content      # 删除成功
400 Bad Request     # 请求错误
401 Unauthorized    # 未授权
403 Forbidden       # 禁止访问
404 Not Found       # 资源不存在
500 Server Error    # 服务器错误
```

### 3.4 响应格式
```

# 成功响应
{
    "status": "success",
    "data": {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com"
    },
    "links": {
        "self": "/api/v1/users/1",
        "orders": "/api/v1/users/1/orders"
    }
}

# 错误响应
{
    "status": "error",
    "code": "USER_NOT_FOUND",
    "message": "User with id 1 not found",
    "documentation_url": "/api/docs#errors"
}
```

## 4. 最佳实践

### 4.1 版本控制
```

# URL中的版本号
/api/v1/users

# Header中的版本号
Accept: application/vnd.company.api+json;version=1
```

### 4.2 HATEOAS
```

{
    "data": {
        "id": 123,
        "status": "pending"
    },
    "_links": {
        "self": "/api/v1/orders/123",
        "cancel": "/api/v1/orders/123/cancel",
        "payment": "/api/v1/orders/123/payment"
    }
}
```

### 4.3 查询参数规范
```

# 分页
/api/v1/users?page=2&per_page=100

# 过滤
/api/v1/users?status=active&role=admin

# 排序
/api/v1/users?sort=created_at:desc

# 字段选择
/api/v1/users?fields=id,name,email
```

## 5. 文档和测试

### 5.1 API文档
- 使用OpenAPI/Swagger
- 提供详细的参数说明
- 包含请求和响应示例
- 说明错误处理机制

### 5.2 测试建议
- 编写完整的单元测试
- 进行集成测试
- 性能测试
- 安全性测试

## 6. 注意事项

1. 保持API的简单性和一致性
2. 正确处理错误情况
3. 实现适当的缓存机制
4. 考虑向后兼容性
5. 提供充分的文档说明
6. 实现合适的监控机制