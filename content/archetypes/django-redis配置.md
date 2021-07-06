---
title: "Django Redis配置"
date: 2018-06-01T10:20:47+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["redis"]
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

# Django-setting配置Redis储存session


```python
# redis配置
CACHES= {
    'default':{
        "BACKEND": 'django_redis.cache.RedisCache',
        "LOCATION": "redis://127.0.0.1:6379/2",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
            "PASSWORD": "",
        }
    }
}

# 储存session设置
SESSION_ENGING = "django.contrib.session.backends.cache"
SESSION_CACHE_ALIAS = "default"

```