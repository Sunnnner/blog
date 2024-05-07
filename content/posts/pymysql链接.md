---
title: "pymsql基础"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - python
tags:
  - pymysql
---
<!--more-->
# pymysql
- import pymysql
###  Connection对象
- •	用于建立与数据库的连接
- 创建对象:调用connect()
- conn = pymysql.connect(参数列表)
- 参数host：链接MySQL主机，如果本机是local host
- 参数port：链接的MySQL主机的端口，默认3306，可以不写
- 参数db数据库的名称
- 参数user链接的用户名
- 参数password链接的密码
- 参数charset通信采用的编码方式，建议是utf8要求与数据库创建时指定的编码一致
### 对象的方法
- 当链接成功后可以做如下操作：
- close（）关闭链接
- commit（）事务，所以需要提交时才会生效
- rollback（）事务，放弃之前的操作
- cursor（）返回cursor对象，用于执行sql语句并获得结果
### cursor对象
- 执行sql语句
- 创建对象：调用connection对象的cursor（）方法
- cursor = conn.cursor()
### 对象的方法
- close（）关闭
- execute（operation[,parametes]）执行语句，返回受影响的行数
- fetchone()执行查询语句时，获取查询及如果集的第一行数据，返回一个元组
- fetchall()执行查询语句时，获取结果集的所有行，一行构成一个元组，再将这些元组装入一个元组返回
- next()执行查询语句时，获取当前行的下一行
- scroll(value[,mode])将行指针移动到某个位置
- mode表示移动的方式
- mode的默认值为relative，标志基于当前行移动到value，
- value 为正则向下移动，value为负则向上移动
- mode的值为absolute，表示基于第一条数据的位置，第一条数据的位置为0
### 对象的属性
- rewcount只读属性，表示最近一次excute()执行后受影响的行数
- connection 获得当前链接对象
- 
---
# SQL 注入
- select * form students where name ='a' or 1=1 or '';
- 