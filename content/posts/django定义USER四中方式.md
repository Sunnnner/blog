---
title: "Django定义USER四中方式"
date: 2018-09-03T10:30:05+08:00
draft: true
categories:
  - django
---

<!--more-->
- 设计user models

- django本身的auth_user 只包含了基本的信息包括用户名，密码，邮箱以及注册时间和最新的登录时间，但是这些字段很难满足我们的要求，有时我们想记录用户更多的信息，例如手机号等信息，这时就需要在auth_user 的基础上增加字段，django自定义User网上有四种方法。

- 是官网上推荐的方法，就是增加一个表auth_profile，其中以auth_user 表中的id作为Forgein Key将两个表过关联起来，这样可以在auth_profile 中增加多个用户的信息。
- 另外一种是修改django的源码，这种方法简单暴力直接，但是这种方法可移植性差，不利于多项目部署。
- 继承django auth/models 中的User继续增加字段，这种方法需要修改setting中的AUTH_USER_MODEL=‘app.User’ app为你自定义的app，INSTALLED_APP中要包含Contenttypes和auth两个app，class meta中 db_table 要指定为auth_user, 如果要在admin中管理用户的话，需要将app_label 进行指定。而且要在admin中重新定义UserAdmin 将新添加的字段写在list_display和add_fields中。详见django.contrib.auth.admin中。

- 重写User，也就是继承AbstractUser和Permissions两个类，其实django的User Model也是继承自这两个类，因此你可以做类似User的定义方法定义User。

- 记录是否执行了迁移文件靠的是django_migrations这表
