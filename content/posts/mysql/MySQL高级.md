---
title: "MySQL关系查询与高级特性指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mysql
---

----
<!--more-->

## 1. 表关系与外键约束

### 1.1 创建外键约束
```sql
CREATE TABLE scores (
    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    score DECIMAL(5,2) DEFAULT 0,
    stu_id INT,
    sub_id INT,
    FOREIGN KEY (stu_id) REFERENCES students(id),
    FOREIGN KEY (sub_id) REFERENCES subjects(id)
) CHARSET=utf8;
```

### 1.2 插入关联数据
```sql
INSERT INTO scores (id, score, stu_id, sub_id) 
VALUES (1, 90, 1, 2);
```

### 1.3 外键级联操作
```sql
CREATE TABLE scores (
    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    score DECIMAL(5,2) DEFAULT 0,
    stu_id INT,
    sub_id INT,
    FOREIGN KEY (stu_id) REFERENCES students(id) ON DELETE CASCADE,
    FOREIGN KEY (sub_id) REFERENCES subjects(id) ON DELETE CASCADE
) CHARSET=utf8;
```

## 2. 连接查询

### 2.1 内连接（INNER JOIN）
```sql
-- 写法1
SELECT students.name, subjects.title, scores.score
FROM scores
INNER JOIN students ON scores.stu_id = students.id
INNER JOIN subjects ON scores.sub_id = subjects.id;

-- 写法2
SELECT students.name, subjects.title, scores.score
FROM students
INNER JOIN scores ON scores.stu_id = students.id
INNER JOIN subjects ON scores.sub_id = subjects.id;

-- 写法3
SELECT students.name, subjects.title, scores.score
FROM subjects
INNER JOIN scores ON scores.sub_id = subjects.id
INNER JOIN students ON scores.stu_id = students.id;
```

### 2.2 左连接（LEFT JOIN）
```sql
SELECT *
FROM students
LEFT JOIN scores ON students.id = scores.stu_id;

SELECT *
FROM scores
LEFT JOIN students ON students.id = scores.stu_id;
```

### 2.3 右连接（RIGHT JOIN）
```sql
SELECT *
FROM students
RIGHT JOIN scores ON students.id = scores.stu_id;

SELECT *
FROM scores
RIGHT JOIN students ON students.id = scores.sub_id;
```

### 2.4 连接查询技巧
```sql
-- 省略重复列名的表名前缀
SELECT name, title, score
FROM scores
INNER JOIN students ON scores.stu_id = students.id
INNER JOIN subjects ON scores.sub_id = subjects.id;

-- 使用表别名简化查询
SELECT name, score
FROM scores AS sco
RIGHT JOIN students AS stu ON stu.id = sco.stu_id;
```

### 2.5 常见查询示例
```sql
-- 查询学生的姓名、平均分
SELECT students.name AS 姓名, AVG(scores.score) AS 平均分
FROM scores
INNER JOIN students ON scores.stu_id = students.id
GROUP BY students.name;

-- 查询男生的姓名、总分  
SELECT students.name, SUM(scores.score)
FROM scores
INNER JOIN students ON scores.stu_id = students.id
WHERE students.gender = 1
GROUP BY students.name;

-- 查询科目的名称、平均分
SELECT subjects.title, AVG(scores.score)
FROM scores
INNER JOIN subjects ON scores.sub_id = subjects.id
GROUP BY subjects.title;

-- 查询未删除科目的名称、平均分、最高分
SELECT subjects.title, AVG(scores.score), MAX(scores.score)
FROM scores
INNER JOIN subjects ON scores.sub_id = subjects.id
WHERE subjects.is_deleted = 0
GROUP BY subjects.title;
```

## 3. 自关联查询

### 3.1 创建自关联表
```sql
CREATE TABLE areas (
    id INT PRIMARY KEY AUTO_INCREMENT NOT NULL,
    title VARCHAR(40),
    pid INT,
    FOREIGN KEY (pid) REFERENCES areas(id)
);
```

### 3.2 导入自关联数据
```bash
# 拷贝SQL文件到服务器
scp areas.sql user@server:/path/to/

# 登录MySQL，选择数据库
mysql -u root -p
USE mydb;

# 执行SQL文件
SOURCE /path/to/areas.sql;
```

### 3.3 自关联查询示例
```sql
-- 查询省级单位数量
SELECT COUNT(*) FROM areas WHERE pid IS NULL;

-- 查询名为"山西省"的所有城市
SELECT city.*
FROM areas AS city
INNER JOIN areas AS province ON city.pid = province.id
WHERE province.title = '山西省';

-- 查询名为"广州市"的所有区县
SELECT district.*
FROM areas AS district
INNER JOIN areas AS city ON city.id = district.pid
INNER JOIN areas AS province ON province.id = city.pid
WHERE city.title = '广州市';
```

## 4. 视图

### 4.1 创建视图
```sql
CREATE VIEW view_name AS
SELECT ...
```

### 4.2 删除视图
```sql
DROP VIEW view_name;
```

## 5. 事务

### 5.1 事务特性（ACID）
- 原子性（Atomicity）
- 一致性（Consistency）
- 隔离性（Isolation）
- 持久性（Durability）

### 5.2 事务使用
```sql
-- 开启事务
BEGIN;

-- 提交事务
COMMIT;

-- 回滚事务
ROLLBACK;
```

### 5.3 表引擎与事务
```sql
-- 查看数据库引擎
SHOW ENGINES;

-- 查看表的创建语句
SHOW CREATE TABLE table_name;

-- 修改表引擎为InnoDB  
ALTER TABLE table_name ENGINE = InnoDB;
```

## 6. 索引

### 6.1 索引设计原则
- 选择尽可能小的数据类型
- 选择简单的数据类型
- 尽量避免NULL值

### 6.2 索引操作
```sql
-- 查看索引
SHOW INDEX FROM table_name;

-- 创建索引
CREATE INDEX index_name ON table_name (column_name);

-- 删除索引
DROP INDEX index_name ON table_name;
```

### 6.3 性能分析
```sql
-- 开启查询分析
SET profiling = 1;

-- 执行查询语句
SELECT ...

-- 查看查询耗时
SHOW PROFILES;
```

### 6.4 索引使用示例
```sql
-- 为areas表的title列创建索引
CREATE INDEX idx_areas_title ON areas (title(20));

-- 执行查询语句
SELECT ...

-- 查看查询耗时
SHOW PROFILES;
```

## 7. 常用字符串函数
- `ASCII(str)`：返回字符串第一个字符的ASCII码值
- `CONCAT(str1, str2, ...)`：拼接多个字符串
- `LENGTH(str)`：返回字符串的长度
- `SUBSTRING(str, pos, len)`：截取字符串的子串
- `LEFT(str, len)`：返回字符串左边指定长度的子串
- `RIGHT(str, len)`：返回字符串右边指定长度的子串
- `TRIM(str)`：去除字符串两端的空格