---
title: "Mysql查询结果输出到文件"
date: 2019-10-03T14:13:04+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["mysql"]
author: "whitek"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Desc Text."
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/Sunnnner/Sunnnner.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

# 方法一：

    直接执行命令：
    `mysql> select count(1) from table into outfile '/tmp/test.xls';`

    Query OK, 31 rows affected (0.00 sec)
    在目录/tmp/下会产生文件test.xls
    遇到的问题：
    mysql> select count(1) from table into outfile '/data/test.xls';
    报错：
    ERROR 1 (HY000): Can’t create/write to file ‘/data/test.xls’ (Errcode: 13)
    可能原因：mysql没有向/data/下写的权限

# 方法二：

    查询都自动写入文件：
    mysql> pager cat > /tmp/test.txt ;
    PAGER set to 'cat > /tmp/test.txt'
    之后的所有查询结果都自动写入/tmp/test.txt’，并前后覆盖
    mysql> select * from table ;
    30 rows in set (0.59 sec)
    在框口不再显示查询结果


# 方法三：
    跳出mysql命令行
    `# mysql -h 127.0.0.1 -u root -p XXXX -P 3306 -e “select * from table” > /tmp/test/txt``

