---
title: "Install Postgresql"
date: 2019-11-04T15:37:26+08:00
draft: false
categories:
  - postgresql
---
<!--more-->
安装postgres sudo apt install postgresql postgresql-contrib

安装完成后，PostgreSQL服务将自动启动。 要验证安装，我们将使用psql实用程序连接到PostgreSQL数据库服务器并打印服务器版本：sudo -u postgres
 psql -c "SELECT version();"

安装完毕后，系统会创建一个数据库超级用户 postgres，密码为空。

切换到postgres用户sudo -i -u postgres

执行psql进入postgres shell 执行\password postgres修改默认密码

修改/etc/postgresql/9.6/main下 postgresql.conf里面listen address为*

修改pg_hba.conf all 地址为0.0.0.0/0

重启sudo /etc/init.d/postgresql restart
