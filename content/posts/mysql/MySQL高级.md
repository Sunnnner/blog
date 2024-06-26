---
title: "Mysql高级"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - mysql
---

----
<!--more-->
# 关系
- 在创建scores表时可以直接创建约束
- creat table socres ( id int() primary key auto_increament notnull,
- score decimal(5,2) default 0,
- stuid int,
- subid int,
- foreign key (stuid) references students(id),
- foreign key (subid) references subjetes(id))charset=utf8;
- 插入数据到成绩表
- insert into scores(id,score,stuid,sunid) values(1,90,1,2)
- 被引用的数据不能够删除
-  外键的级联操作
-  creat table socres ( id int() primary key auto_increament notnull,
- score decimal(5,2) default 0,
- stuid int,
- subid int,
- foreign key (stuid) references students(id) on delete cascade,
- foreign key (subid) references subjetes(id) on delete cascade
- )charset=utf8;
- ---
# 连接查询
- 内连接 (inner join)
- 姓名(name)  标题(title)  分数（score）
- 1.这三个字段来自三张表,students.name,subjects.title,scores.score
- 2.这三张表有什么关系
- a,scores和学生表scores.stuid = students.id
- b,scores 和subjects 的关系 scores.subid  = subjects.id
- 第一种写法
- select students.name,subjects.title,scores.score from
- scores inner join students on scores.stuid = students.id
- inner join subjects on scores.subid = subjects.id;
- 第二种写法：
- select students.name,subjects.title,scores.score from students 
- inner join scores on scores.stuid = students.id
- inner join subjects on scores.subid = subjects.id;
- 第三种写法
- select students.name,subjects.title,scores.score from subjects 
- inner join scores on scores.subid = subjects.id
- inner join students on scores.stuid = students.id;
- 左链接 (left join)
- select * from students left join scores on students.id =scores.stuid;
- select * from scores left join students on students.id = scores.subid;
- 右链接 (rigth join)
-  select * from students right join scores on students.id =scores.stuid;
-  select * from scores right join students on students.id = scores.subid;
-  •	如果多个表中列名不重复可以省略“表名.”部分
-  select name,title,score from scores
-  inner join students on scores.stuid=students.id
-  inner join subjects on scores.subid=subjects.id;
-  •	如果表的名称太长，可以在表名后面使用' as 简写名'或' 简写名'，为表起个临时的简写名称
-  select name ,score  from scores as sco 
-  right join students as stu on stu.id = sco.stuid;
-  •	查询学生的姓名、平均分
-  select students.name as 姓名,avg(scores.score) as 平均分 from scores inner join students on scores.stuid = students.id group by students.name;
-  •	查询男生的姓名、总分
-  select students.name,sum(scores.score) from scores inner join students on students on scores.stuid = students.id where students.gender=1  group by students.name;
-  •	查询科目的名称、平均分
-  select subjects.title,avg(scores.score) from scores inner join subjects on 
-  scores.stuid = sunjects.id where group by subjects.title;
-  •	查询未删除科目的名称、平均分、最高分
-  select subjects.title,avg(scores.score),max(scores.score) from scores inner join subjects on 
-  scores.stuid = sunjects.id where subjects.isdelete=0 group by subjects.title;
-  

----
# 自关联
- 1.引入自关联
- 创建areas地区表 ：
- create table areas (
- id int primary key auto_ increment not mull,
- atitle varchar(40),
- pid int(11),
- foreign key(pid) references areas(id)
- );
- 
- 导入数据 
- 1.把areas.sql文件拷贝到liunx 上，
- 2.在当前目录进入到Mysql 选择数据库，执行命令:source areas.sql
- 自关联表的数据的查询：
- 查询一共有多少个省级单位
- select * from areas where pid is null;
- select id,atitle from areas where pid is null;
- 查询省的名字为""山西省"所有城市
- 1.列出的城市的inxi:city.*
- 2.隐含条件，city.pid=province.id 要取别名
- 3.where provice.atitle = "山西省"
- 4.总共一张表，有两中数据类型，模拟两张表
- select city.* from areas as city inner join areas as province on city.pid=province.id where province.atitle = "山西省";
- 查询市的名称为广州市的所有区县
- 1.虚拟三张表，provice,city,dis  select dis.*
- 2.隐含条件，city.pid=province.id ,dis.pid=city.id 要取别名
- where city.atitle="广州市"
- select dis*  from areas as dis inner join areas as city on city.id = dis.pid inner join areas as province on procince.id = city.pid where provice.atitle = "广州市";
- 

----
# 视图
- creat view as select...
- 如果说两张表里面的==字段相同==就不能进行创建视图
- 删除视图drop view xxx
- ---
# 事务
- 事务的四大特性：（ACID）
- 原子性（Atomicity）  要么全部完成，要么都不成功
- 一致性(Consistency)  几个并行执行的事务，其执行结果必须与按照某一舒徐串执行的结果相一致
- 隔离性(Isolation)   事务的执行不受其他事务的干扰，事务执行的中间结果对其他事务必须市透明的
- 持久性(Durability)  对于任意已提交事务，系统必须保证该事务对数据库的改变不被丢失，即使数据库出现故障；
- 要求：表的类型必须市innodb 或bdb类型，才可以对此表使用事务；
- 数据库引擎是用于存储、处理和保护数据的核心服务，利用数据库引擎可以控制访问权限并快速处理事务，从而满足企业内大多数需要处理大量数据的应用程序的要求。
- 查看引擎：show engines;
- 查看表的创建语句： show create table students/xxx;
- 修改表的字段：alert table "表明" engine=innodb;
### 使用事务的情况；
- 开启 begin;
- 提交： commit
- 回滚： rollbaack;
- ----
# 索引
- 越小的数据通常更好
- 简单的数据类型更好
- 尽量避免null
- 相关操作
- show index from xxxx;
- 创建索引 
- create index 索引名 on 表(哪一列);
- 删除索引
- drop index  索引名 on 表；
- 开启运行时间检测；
- set profiling =1;
- 执行查询语句：
- 
- 查看执行时间：
- show profiles;
- 为表areas 的atitle创建索引
- create index 索引名 on areas(atitle(20))
- 执行查询语句
- 在看执行时间
- show profiles;
- 字符串函数select ascii('a');
- 拼接字符串select concat(12,34,'ab')
- 查看字符串长度select length('abbc')
- 截取字符串select substring("abc123",2,3);
- select left('1234',2)
- select right()
- 去除空格：select trim("  barr  ")