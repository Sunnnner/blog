---
title: "Mysql安装"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mysql
---

----
<!--more-->
# 安装数据库
- `sudo apt-get install mysql-server `
- `show databases` 查看数据
- 安装mysql-client
- `sudo apt -get install mysql-client`

- 如无法下载
- `sudo apt-get install updata`

- 检查书否安装成功
- `dudo netstat -tap | grap mysql `
- 登陆
- `mysql -u root -p`
- 或者直接跟密码`mysql -u roo -p12345`
- 启动
- `service mysql start` 
- `sudo /etc/init.d/mysql start`
- 关闭
- `service mysql stop`或者  `mysqladmin -u root -p shutdown`
- `sudo netstat -tap | grep mysql `
- 重启
- `service mysql restart`或者 `sudo /etc/init.d/ mysql restart`
- 进入数据库
- `mysql -u root -p`
- 推出mysql 
- `quit;quit exit;exit ctrl+d`
- ----
- # 使用Navicat for Mysql连接mysql服务器
- 使用mysql这个数据库选择数据库`use+数据库名字`  `use mysql;`
- 查看mysql 的数据库  `show databases`
- 把当前数据库所有的标列出来`show tables`
- 查看某个表的结构`desc xx`
- 查看某个表的所有数据`select * from xxx`
- 查看某一天数据的信息 :`select * from xxx where id/name/xxx/=xx`
- 
- 在mysql这个数据库中查找user这个表中的user和host字段`select user,host from user;`
- 创建用户`grant all privileges on *.* to 用户名@"%" identified by "密码" with grant option`
- `grant all privileges on *.* to white@"%" identified by "12345" with grant option;
`
- grant是授权命令，其中afu是我们连接用的用户名、”123456″是连接密码，用户名后面的“%”通用符表示允许各host操作。
- 查询select user,host from user;
- 刷新数据库账户权限 `flush privileges;`
- 重新查询 `select user,host from user;`
- 删除id 为13的student的信息  `delent from student where id = 13`
- 删除用户：`delete from user where user = "用户名"and host = "xxx" `
- 修改id 为1的数据的名字为郭靖:`update student set name = '郭靖' where id = 1;`
- 增加一条数据`insert into student(id,name) values(0,王迪);`id=0默认最后
- 重新查询：`select user,host from user`
- 
- ----
- ### 表的操作
- 使用某个数据库 use xxx
- 列出所有标show tables
- 创建数据表create table tab_name(
id int(10)  auto_increment primary key not null,
name varchar(40),
pwd varchar(40)
) charset=utf8;
- 
- 删除数据表 drop table xxx
- 查看当前使用的数据库：select database();
- 显示数据表的结构   desc xxx或者 describe xxx  或者 show colu
- ---
- # 数据库操作
- 显示那些数据库  show databases;
- 切换数据库 use xxx;
- 显示数据库中所有的表 show tables 
- 列出表的结构 desc xxx
- 查看当前选择选中的数据库：select database();
- 删除数据库 drop database xxx
- 创建新的数据库 create database xxx  指定编码charset=utf8
- 修改密码mysqladmin -u 用户名 -p旧密码 password 新密码;
- 1.推出数据库
- 2.执行Linux命令：mysqladmin -u 用户名 -p旧密码 password 新密码
- ---
- # 表的操作
- 创建数据表
- create table student(
- id int(11) auto_increment primary key not null,
- name varchar(40) default null,
- idDelete bit(1) default 0
- )charset=utf8
- 删除表  drop table xxx
- 显示表的结构 desc xxx
- 查询表的里面所有的数据  select * from xxx
- 插入数据：insert into xxx() vslues(),(0,""),(0,"")
- 删除名字为“张三"delete from students where name = "张三"
- 删除所有数据 delete from students;
- 在表中添加一个字段 alter table tab_name add address varchar(20);
- 删除表中的字段: alter table tab_name drop address;
- (了解)把某一列设为主键：
- alter table tab_name change id id int(10);
- alter table tab_name drop primary key;
- ALTER TABLE tab_name ADD PRIMARY KEY (col_name) ;
- alter table tab_name add primary key(id);
- alter table tab_name change id id int(10) not null auto_increment~~~~~~;~~~~~~
- ----
- # 数据库备份
- cd / var/lib/
- sudo -s
- cd musql
- mysqldump -uroot -p 数据库名 > ~ /Desktop/备份文件.sql;
- 数据恢复：
- mysql -uroot -p xxx< xxx.sql;