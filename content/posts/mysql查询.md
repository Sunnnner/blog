---
title: "mysql查询"
description: 
date: 2022-07-12T14:37:29+08:00
draft: true
categories:
  - mysql
---
<!--more-->
----
# 查询
- 1.准备数据创建新的数据库
- 2.创建表
- 创建学生表：
- create table students(
      -> id int(11) primary key auto_increment not null,
      -> name varchar(40) default null,
      -> birthday datetime default null,
      -> gender bit(1) default 0,
      -> isDelete bit(1
      -> ) default 0)charset=utf8;

- 3.插入数据
- 创建学科表
-         create table subject(
-     id int(11) primary key auto_increment not null,
-           title varchar(10),
-           isDelete bit(1) default 0)charset=utf8;
-           

- 查询记本语法
- select * from studengs;查询所有信息
- 显示多个信息 select id,name,birthday from students;
- 取别名显示： select id as 编号,name as 姓名,birthday as 生日 from students;
- 某i额消除重复行：消除性别的重复列：
- select distinct gender from students;
- 0-----
- ### 条件where；
- select * from students where id =1;
- 比较运算符： =,>,>=,<,<=,!=或者<>
- 逻辑运算：and,or,not;
- 模糊查询:like  %表示任意多个字符  _表示任意一个字符
- select * from students where name like "郭%";

- 查询范围：•	in表示在一个非连续的范围内
- •	between ... and ...表示在一个连续的范围内
- 空判断--is null,is not null
- •	判空is null
- •	判非空is not null
- #### 优先级
- •	小括号，not，比较运算符，逻辑运算符
- •	and比or先运算，如果同时出现并希望先算or，需要结合()使用
- ---
- # 聚合
- 5个聚合函数`count(*),max(列),min(列),sum(列),avg(列)`
- `count`计算表中的记录（行数）
- `sum`计算表中数值列的数据合计值
- `avg`计算表中数值列的数据平均值
- `max `求出表中任意列中数据的最大值
- `min`求出表中任意列中数据的最小值
- •	查询学生总数  select count(*) from students;
- •	查询女生的编号最大值 select max(id) from students where gender=0;
- select max(id) as 女生的最大标号 from students where gender=0;
- •	查询未删除的学生最小编号 select min(id) from students where isdelete=0;
- •	查询男生的编号之和select sum(id) from students where gender=1;
- •	查询未删除女生的编号平均值select avg(id) from students where isdelete=0 and gender=0;
- ---
- # 分组
- ### 分组语法：
- select 列1,列2,聚合... from 表名 group by 列1,列2,列3...
- •	查询男女生总数：select gender as 性别,count(*)from students group by gender;
- •	查询删除和未删除的人数
- select isdelete as 是否删除, count(*)  from students group by isdelete；
- ###  分组后的数据筛选
- select 列1,列2,聚合... from 表名
- select 列1,列2,聚合... from 表名
- having 列1,...聚合...
- •	查询男生总人数数用where:
- select count(*)
from students
where gender=1;
- select gender,count(*) from students where gender=1;
- 使用分组和having
- select count(*) from students group by genser;
- select gender as 男生,count(*) from students group by gender having gender=1;
- ----
- # 排序
- select * from 表名order by 列1 asc|desc,列2 asc|desc,...
- •	将行数据按照列1进行排序，如果某些行列1的值相同时，则按照列2排序，以此类推
- •	默认按照列值从小到大排列
- •	asc从小到大排列，即升序
- •	desc从大到小排序，即降序
- 查询未删除的男生的信息降序
- select * from students where isdelete=0 and gender = 1 order by id desc;
- 查询未删除科目信息，按名称升序
- select * from subjects where isdelete = 0 order by title;
- ----
- # 分页
- select * from 表名limit start,count
- •	从start开始，获取count条数据
- •	start索引从0开始
- 查询数据：
- 假设页为n,每页的数据多少条m
- 第一页数据
- n=1,m=3
- select * from student limit 0,3;--->(n-1)*m,m
- 第二页数据
- n=2,m=3
- select * from students limit 3,3;--->(n-1)*m,m
- 第三页数据
- n=3,m=3
- select * from students limit 6,3;--->(n-1)*m,m
- n代表第一页，m要查询多少条数据
- (n-1)*m,m
- select * from 表名 ==limit== (n-1)*m,m;