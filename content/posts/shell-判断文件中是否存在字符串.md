---
title: "Shell 判断文件中是否存在字符串"
date: 2020-01-01T15:45:01+08:00
draft: true
categories:
  - shell
---
<!--more-->
```shell

if cat xxx.yml | grep "content">/dev/null

then

    return 1

else

    return 0

fi

```