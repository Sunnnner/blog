---
title: "MySQL数据导出指南"
date: 2019-10-03T14:13:04+08:00
draft: false
categories:
  - mysql
---
<!--more-->

## 1. 直接导出文件方法

### 1.1 基本语法
```sql
-- 将查询结果导出到文件
SELECT count(1) FROM table 
INTO OUTFILE '/tmp/test.xls';
```

### 1.2 常见权限问题
```bash
# 检查MySQL数据目录权限
sudo ls -l /var/lib/mysql

# 修改目录权限
sudo chown -R mysql:mysql /data
```

### 1.3 完整导出示例
```sql
-- 导出完整数据
SELECT * FROM table 
INTO OUTFILE '/tmp/export.csv' 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\n';
```

## 2. 交互式导出方法

### 2.1 使用PAGER命令
```sql
-- 设置输出重定向
mysql> pager cat > /tmp/test.txt

-- 执行查询（结果将写入文件）
mysql> SELECT * FROM table;
```

### 2.2 PAGER常用技巧
```sql
-- 恢复默认输出
mysql> nopager

-- 使用less查看输出
mysql> pager less

-- 使用more查看输出
mysql> pager more
```

## 3. 命令行导出方法

### 3.1 基本导出命令
```bash
# 直接导出到文件
mysql -h 127.0.0.1 -u root -p \
    -e "SELECT * FROM table" > /tmp/export.txt

# 带密码的导出
mysql -h 127.0.0.1 -u root -pPASSWORD \
    database_name -e "SELECT * FROM table" > /tmp/export.txt
```

### 3.2 高级导出选项
```bash
# 指定分隔符
mysql -h host -u user -p \
    -B -N -e "SELECT * FROM table" \
    --silent \
    --skip-column-names \
    --raw > /tmp/export.txt
```

## 4. 大数据量导出建议

### 4.1 CSV格式导出
```bash
# 使用mysqldump导出CSV
mysqldump -u root -p \
    --fields-terminated-by=',' \
    --fields-enclosed-by='"' \
    --lines-terminated-by='\n' \
    database_name table_name > /tmp/export.csv
```

### 4.2 分批导出大表
```sql
-- 使用LIMIT分批导出
SELECT * FROM large_table 
WHERE id > last_exported_id 
LIMIT 10000 
INTO OUTFILE '/tmp/export_part.csv';
```

## 5. 安全和性能注意事项

### 5.1 权限控制
1. 使用专门的导出用户
2. 限制导出用户权限
3. 避免导出敏感数据

### 5.2 性能优化
1. 避免在生产高峰期导出大量数据
2. 使用索引优化导出查询
3. 考虑使用压缩格式
4. 对大表使用分批导出

### 5.3 常见错误处理
```bash
# 权限问题
ERROR 1 (HY000): Can't create/write to file

# 解决方案
sudo chown mysql:mysql /export/path
sudo chmod 755 /export/path
```

## 6. 实用导出脚本示例

```bash
#!/bin/bash

# 数据库导出脚本
DB_USER="root"
DB_PASS="password"
DB_NAME="mydb"
EXPORT_DIR="/backup/mysql"

# 创建时间戳目录
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
EXPORT_PATH="${EXPORT_DIR}/${TIMESTAMP}"

mkdir -p $EXPORT_PATH

# 导出所有表
mysqldump -u $DB_USER -p$DB_PASS \
    --single-transaction \
    --routines \
    --triggers \
    $DB_NAME > "${EXPORT_PATH}/full_backup.sql"

# 压缩备份
tar -czvf "${EXPORT_PATH}.tar.gz" $EXPORT_PATH

echo "数据库备份完成：${EXPORT_PATH}"
```

## 7. 推荐工具
1. Navicat
2. MySQL Workbench
3. phpMyAdmin
4. DBeaver