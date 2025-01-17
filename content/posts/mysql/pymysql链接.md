---
title: "PyMySQL 数据库操作指南"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - python
tags:
  - pymysql
---
<!--more-->

## 1. 基础连接

### 1.1 安装PyMySQL
```python
pip install pymysql
```

### 1.2 建立数据库连接
```python
import pymysql

# 创建连接
conn = pymysql.connect(
    host='localhost',      # MySQL主机地址
    port=3306,            # 端口号（默认3306）
    user='root',          # 用户名
    password='password',   # 密码
    database='mydb',      # 数据库名
    charset='utf8'        # 字符编码
)

try:
    # 使用连接进行操作
    pass
finally:
    # 关闭连接
    conn.close()
```

## 2. Connection对象

### 2.1 主要方法
```python
# 关闭连接
conn.close()

# 提交事务
conn.commit()

# 回滚事务
conn.rollback()

# 创建游标
cursor = conn.cursor()
```

### 2.2 使用上下文管理器
```python
with pymysql.connect(
    host='localhost',
    user='root',
    password='password',
    database='mydb',
    charset='utf8'
) as conn:
    with conn.cursor() as cursor:
        # 执行操作
        pass
```

## 3. Cursor对象

### 3.1 基本操作
```python
# 创建游标
cursor = conn.cursor()

try:
    # 执行SQL语句
    affected_rows = cursor.execute('SELECT * FROM users')
    
    # 获取单行数据
    row = cursor.fetchone()
    
    # 获取所有数据
    rows = cursor.fetchall()
finally:
    # 关闭游标
    cursor.close()
```

### 3.2 游标方法详解
```python
# 执行SQL语句
cursor.execute('SELECT * FROM users WHERE age > %s', (18,))

# 执行多条SQL语句
cursor.executemany(
    'INSERT INTO users (name, age) VALUES (%s, %s)',
    [('Alice', 20), ('Bob', 22)]
)

# 获取下一行数据
row = cursor.fetchone()

# 获取指定数量的行
rows = cursor.fetchmany(size=2)

# 获取所有行
all_rows = cursor.fetchall()

# 移动游标位置
cursor.scroll(2, mode='relative')    # 相对当前位置移动
cursor.scroll(0, mode='absolute')    # 移动到开始位置
```

### 3.3 游标属性
```python
# 获取影响的行数
affected_rows = cursor.rowcount

# 获取当前连接对象
current_conn = cursor.connection
```

## 4. 实践示例

### 4.1 基本CRUD操作
```python
import pymysql
from pymysql.cursors import DictCursor

def get_database_connection():
    return pymysql.connect(
        host='localhost',
        user='root',
        password='password',
        database='mydb',
        charset='utf8',
        cursorclass=DictCursor  # 返回字典格式的结果
    )

# 查询操作
def select_users():
    with get_database_connection() as conn:
        with conn.cursor() as cursor:
            sql = "SELECT * FROM users WHERE age > %s"
            cursor.execute(sql, (18,))
            return cursor.fetchall()

# 插入操作
def insert_user(name, age):
    with get_database_connection() as conn:
        with conn.cursor() as cursor:
            sql = "INSERT INTO users (name, age) VALUES (%s, %s)"
            cursor.execute(sql, (name, age))
        conn.commit()

# 更新操作
def update_user(user_id, new_age):
    with get_database_connection() as conn:
        with conn.cursor() as cursor:
            sql = "UPDATE users SET age = %s WHERE id = %s"
            cursor.execute(sql, (new_age, user_id))
        conn.commit()

# 删除操作
def delete_user(user_id):
    with get_database_connection() as conn:
        with conn.cursor() as cursor:
            sql = "DELETE FROM users WHERE id = %s"
            cursor.execute(sql, (user_id,))
        conn.commit()
```

### 4.2 事务处理
```python
def transfer_money(from_id, to_id, amount):
    conn = get_database_connection()
    try:
        with conn.cursor() as cursor:
            # 检查余额
            cursor.execute(
                "SELECT balance FROM accounts WHERE id = %s",
                (from_id,)
            )
            if cursor.fetchone()['balance'] < amount:
                raise ValueError("余额不足")
            
            # 扣款
            cursor.execute(
                "UPDATE accounts SET balance = balance - %s WHERE id = %s",
                (amount, from_id)
            )
            
            # 入账
            cursor.execute(
                "UPDATE accounts SET balance = balance + %s WHERE id = %s",
                (amount, to_id)
            )
            
        # 提交事务
        conn.commit()
    except Exception as e:
        # 发生错误时回滚
        conn.rollback()
        raise e
    finally:
        conn.close()
```

## 5. 安全性考虑

### 5.1 防止SQL注入
```python
# 错误示例 - 容易遭受SQL注入
cursor.execute(f"SELECT * FROM users WHERE name = '{name}'")

# 正确示例 - 使用参数化查询
cursor.execute("SELECT * FROM users WHERE name = %s", (name,))
```

### 5.2 最佳实践
1. 始终使用参数化查询
2. 妥善保管数据库凭证
3. 使用最小权限原则
4. 及时关闭连接和游标
5. 正确处理异常
6. 使用连接池管理连接