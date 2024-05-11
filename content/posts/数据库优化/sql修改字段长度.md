---
title: "Sql修改字段长度"
date: 2019-09-10T11:41:14+08:00
draft: false
categories:
  - sql
---
<!--more-->

sql修改字段长度的语法
    `alter table 表名 modify 字段名 字段类型;`

标准sql所有都适用
`alter table 数据库.表名 modify 字段名 字段类型;`

修改字段名名称
`alter table 数据库名 表名 column col1 to col2;`

添加字段
`alter table 数据库名.表名 add 字段名 类型;`

