---
title: "Django Redis配置"
date: 2018-06-01T10:20:47+08:00
draft: true
categories:
  - django
tags:
  - redis
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