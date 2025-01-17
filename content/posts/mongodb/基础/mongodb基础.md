---
title: " MongoDB 完全指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mongodb
---
<!--more-->

## 1. NoSQL概述

### 1.1 什么是NoSQL
- NoSQL (Not Only SQL) 是非关系型数据库的统称
- 适用于处理大规模数据、高并发读写、灵活的数据模型等场景

### 1.2 NoSQL优势
- 高扩展性和分布式友好
- 成本效益高
- 架构灵活,无需预定义模式
- 简化的数据关系

### 1.3 NoSQL局限
- 缺乏统一标准
- 查询功能相对受限
- 最终一致性模型可能带来复杂性

### 1.4 NoSQL数据库分类
1. 键值存储数据库 (如Redis)
2. 列族存储数据库 (如Cassandra)
3. 文档型数据库 (如MongoDB)
4. 图形数据库 (如Neo4j)

## 2. MongoDB基础

### 2.1 MongoDB简介
MongoDB是一个开源的文档型数据库,具有以下特点:
- 文档导向
- 高性能
- 高可用性
- 易扩展
- 丰富的查询语言

### 2.2 核心概念对比
| SQL概念 | MongoDB概念 | 说明 |
|---------|-------------|------|
| Database | Database | 数据库 |
| Table | Collection | 数据集合 |
| Row | Document | 数据文档 |
| Column | Field | 数据字段 |
| Index | Index | 索引 |
| Join | $lookup | 表关联 |

### 2.3 基本命令
```bash
# 数据库操作
mongo                    # 进入MongoDB Shell
show dbs                 # 显示所有数据库
use <database>          # 切换数据库
db                      # 查看当前数据库
db.dropDatabase()       # 删除当前数据库

# 集合操作
show collections        # 显示所有集合
db.createCollection("name") # 创建集合
db.<collection>.drop()  # 删除集合
```

## 3. 数据操作

### 3.1 数据类型
- ObjectId: 文档唯一标识符
- String: 字符串
- Number: 数字
- Boolean: 布尔值
- Array: 数组
- Object: 嵌入式文档
- Null: 空值
- Date: 日期时间
- Timestamp: 时间戳

### 3.2 CRUD操作

#### 创建(Create)
```javascript
// 插入单个文档
db.collection.insertOne({
    name: "张三",
    age: 25
})

// 插入多个文档
db.collection.insertMany([
    { name: "李四", age: 30 },
    { name: "王五", age: 35 }
])
```

#### 读取(Read)
```javascript
// 查询所有文档
db.collection.find({})

// 条件查询
db.collection.find({ age: { $gt: 30 }})

// 投影查询
db.collection.find({}, { name: 1, _id: 0 })
```

#### 更新(Update)
```javascript
// 更新单个文档
db.collection.updateOne(
    { name: "张三" },
    { $set: { age: 26 }}
)

// 更新多个文档
db.collection.updateMany(
    { age: { $gt: 30 }},
    { $set: { status: "senior" }}
)
```

#### 删除(Delete)
```javascript
// 删除单个文档
db.collection.deleteOne({ name: "张三" })

// 删除多个文档
db.collection.deleteMany({ age: { $lt: 25 }})
```

### 3.3 高级查询
```javascript
// 比较运算符
$eq  // 等于
$ne  // 不等于
$gt  // 大于
$gte // 大于等于
$lt  // 小于
$lte // 小于等于
$in  // 在指定数组中
$nin // 不在指定数组中

// 逻辑运算符
$and // 与
$or  // 或
$not // 非
$nor // 都不

// 分页
db.collection.find().limit(10)  // 限制返回数量
db.collection.find().skip(10)   // 跳过指定数量
```

## 4. 最佳实践

### 4.1 索引使用
- 为常用查询字段创建索引
- 避免过多索引
- 定期分析查询性能

### 4.2 数据模型设计
- 优先考虑嵌入式关系
- 适度冗余以提高查询效率
- 控制文档大小

### 4.3 性能优化
- 使用适当的数据类型
- 避免大规模的in查询
- 使用投影限制返回字段
- 批量操作代替单条操作