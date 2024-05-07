---
title: "Django Minio开发过程"
date: 2019-10-06T14:17:12+08:00
draft: true
categories:
  - django
tags:
  - minio
---

> 使用Django-minio-storage进行开发minio的静态文件存储功能，本来寻思用minio直接进行开发，既然django有这个包我们就拿来用一下

- 项目说明[django-minio-storage](https://django-minio-storage.readthedocs.io/en/latest/)


## 开发期间遇到的问题

- 千万不要忘了把minio-storage添加到app

        Add minio_storage to INSTALLED_APPS in your project settings.

        The last step is setting DEFAULT_FILE_STORAGE to "minio_storage.storage.MinioMediaStorage", and STATICFILES_STORAGE to "minio_storage.storage.MinioStaticStorage".

接下来的配置看官网配置就行了

因为我用docker写的所以minio_storage_endpoint可以使用docker项目名称:端口号或者外网域名（static.media.com）或者外网IP:端口号

浏览器复用minio静态服务器的media携带端口号怎么办？

解决办法 nginx 负载均衡：

```conf
upstream docker {
    server docker:9000;
}

server {
    listen 80;
    server_name static.media.com

    location / {
        proxy_set_header Host $host;
        proxy_pass http://docker;
        client_max_body_size 10m;
    }
}
```