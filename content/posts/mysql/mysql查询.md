---
title: "MySQL查询语句指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mysql
---
<!--more-->
----

## 1. 数据准备

### 1.1 创建数据库
```sql
CREATE DATABASE db_example;
USE db_example;
```

### 1.2 创建表
```sql
CREATE TABLE students (
    id INT(11) PRIMARY KEY AUTO_INCREMENT NOT NULL,
    name VARCHAR(40) DEFAULT NULL,
    birthday DATETIME DEFAULT NULL,
    gender BIT(1) DEFAULT 0,
    is_deleted BIT(1) DEFAULT 0
) CHARSET=utf8;

CREATE TABLE subjects (
    id INT(11) PRIMARY KEY AUTO_INCREMENT NOT NULL,
    title VARCHAR(10),
    is_deleted BIT(1) DEFAULT 0
) CHARSET=utf8;
```

### 1.3 插入数据
略

## 2. 基础查询

### 2.1 查询所有列
```sql
SELECT * FROM students;
```

### 2.2 查询指定列
```sql
SELECT id, name, birthday FROM students;
```

### 2.3 列别名
```sql
SELECT id AS 编号, name AS 姓名, birthday AS 生日 FROM students;
```

### 2.4 去重查询
```sql
SELECT DISTINCT gender FROM students;
```

## 3. 条件查询

### 3.1 等值查询
```sql
SELECT * FROM students WHERE id = 1;
```

### 3.2 比较运算符
```sql
SELECT * FROM students WHERE id > 1;
SELECT * FROM students WHERE id >= 1;
SELECT * FROM students WHERE id < 1;
SELECT * FROM students WHERE id <= 1;
SELECT * FROM students WHERE id != 1;
SELECT * FROM students WHERE id <> 1;
```

### 3.3 逻辑运算符
```sql
SELECT * FROM students WHERE id > 1 AND gender = 1;
SELECT * FROM students WHERE id > 1 OR gender = 1;
SELECT * FROM students WHERE NOT gender = 1;
```

### 3.4 模糊查询
```sql
SELECT * FROM students WHERE name LIKE '郭%';
SELECT * FROM students WHERE name LIKE '_王';
```

### 3.5 范围查询
```sql
SELECT * FROM students WHERE id IN (1, 3, 5);
SELECT * FROM students WHERE id BETWEEN 1 AND 10;
```

### 3.6 空值判断
```sql
SELECT * FROM students WHERE birthday IS NULL;
SELECT * FROM students WHERE birthday IS NOT NULL;
```

## 4. 聚合函数

```sql
SELECT COUNT(*) FROM students;
SELECT MAX(id) FROM students WHERE gender = 0;
SELECT MIN(id) FROM students WHERE is_deleted = 0;
SELECT SUM(id) FROM students WHERE gender = 1;
SELECT AVG(id) FROM students WHERE is_deleted = 0 AND gender = 0;
```

## 5. 分组查询

### 5.1 基本语法
```sql
SELECT gender AS 性别, COUNT(*) FROM students GROUP BY gender;
SELECT is_deleted AS 是否删除, COUNT(*) FROM students GROUP BY is_deleted;
```

### 5.2 分组后筛选
```sql
SELECT gender AS 性别, COUNT(*) 
FROM students
GROUP BY gender
HAVING gender = 1;
```

## 6. 排序查询

```sql
SELECT * FROM students 
WHERE is_deleted = 0 AND gender = 1
ORDER BY id DESC;

SELECT * FROM subjects
WHERE is_deleted = 0
ORDER BY title ASC;
```

## 7. 分页查询

```sql
-- 第1页，每页3条
SELECT * FROM students LIMIT 0, 3;

-- 第2页，每页3条 
SELECT * FROM students LIMIT 3, 3;

-- 第3页，每页3条
SELECT * FROM students LIMIT 6, 3;
```

## 8. 最佳实践

1. 合理使用索引优化查询性能
2. 尽量减少使用通配符`%`进行模糊查询
3. 优先使用`IN`而不是`OR`进行范围查询
4. 合理设置查询缓存
5. 定期优化和重构SQL语句
6. 监控慢查询并进行优化