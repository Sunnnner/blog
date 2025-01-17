---
title: "MySQL数据库管理指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mysql
---

----
<!--more-->
## 1. 安装与基本配置

### 1.1 安装MySQL
```bash
# 安装服务器
sudo apt-get update
sudo apt-get install mysql-server

# 安装客户端
sudo apt-get install mysql-client

# 检查安装状态
sudo netstat -tap | grep mysql
```

### 1.2 服务管理
```bash
# 启动服务
sudo service mysql start
# 或
sudo /etc/init.d/mysql start

# 停止服务
sudo service mysql stop
# 或
sudo mysqladmin -u root -p shutdown

# 重启服务
sudo service mysql restart
```

### 1.3 登录与退出
```bash
# 登录（交互式输入密码）
mysql -u root -p

# 登录（命令行直接提供密码，不推荐）
mysql -u root -p12345

# 退出
quit;
# 或
exit;
```

## 2. 用户管理

### 2.1 用户操作
```sql
-- 查看用户列表
SELECT user, host FROM mysql.user;

-- 创建用户并授权
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' 
IDENTIFIED BY 'password' 
WITH GRANT OPTION;

-- 刷新权限
FLUSH PRIVILEGES;

-- 删除用户
DELETE FROM mysql.user 
WHERE user = 'username' AND host = 'hostname';
```

### 2.2 修改密码
```bash
# 命令行修改密码
mysqladmin -u username -p'oldpassword' password 'newpassword'
```

## 3. 数据库操作

### 3.1 基本操作
```sql
-- 显示所有数据库
SHOW DATABASES;

-- 创建数据库
CREATE DATABASE dbname CHARACTER SET utf8;

-- 选择数据库
USE dbname;

-- 显示当前数据库
SELECT DATABASE();

-- 删除数据库
DROP DATABASE dbname;
```

### 3.2 表操作
```sql
-- 创建表
CREATE TABLE tablename (
    id INT(11) AUTO_INCREMENT PRIMARY KEY NOT NULL,
    name VARCHAR(40) DEFAULT NULL,
    is_deleted BIT(1) DEFAULT 0
) CHARSET=utf8;

-- 显示所有表
SHOW TABLES;

-- 显示表结构
DESC tablename;
-- 或
DESCRIBE tablename;

-- 删除表
DROP TABLE tablename;
```

### 3.3 数据操作
```sql
-- 插入数据
INSERT INTO tablename (column1, column2) 
VALUES (value1, value2);

-- 查询数据
SELECT * FROM tablename;
SELECT column1, column2 FROM tablename WHERE condition;

-- 更新数据
UPDATE tablename 
SET column1 = value1 
WHERE condition;

-- 删除数据
DELETE FROM tablename WHERE condition;
```

### 3.4 表结构修改
```sql
-- 添加字段
ALTER TABLE tablename 
ADD COLUMN columnname VARCHAR(20);

-- 删除字段
ALTER TABLE tablename 
DROP COLUMN columnname;

-- 修改主键
ALTER TABLE tablename 
ADD PRIMARY KEY (columnname);
```

## 4. 数据备份与恢复

### 4.1 备份数据库
```bash
# 备份整个数据库
mysqldump -u root -p dbname > backup.sql

# 备份特定表
mysqldump -u root -p dbname tablename > backup.sql
```

### 4.2 恢复数据库
```bash
# 恢复数据库
mysql -u root -p dbname < backup.sql
```

## 5. 最佳实践

### 5.1 安全建议
1. 不要在命令行中直接输入密码
2. 定期更改密码
3. 及时删除不用的用户
4. 最小权限原则授权

### 5.2 性能优化
1. 合理使用索引
2. 定期备份数据
3. 及时清理不需要的数据
4. 优化查询语句

### 5.3 编码注意事项
1. 始终指定字符集为UTF-8
2. 使用预处理语句防止SQL注入
3. 使用事务确保数据一致性
4. 正确处理NULL值