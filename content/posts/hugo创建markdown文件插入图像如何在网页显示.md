---
title: "Hugo创建markdown文件插入图像如何在网页显示"
description: 
date: 2023-11-10T11:09:54+08:00
draft: false
categories:
  - hugo
tags:
  - hugo
  - markdown
---
<!--more-->

- [摘要](#摘要)
  - [事实](##事实)
  - [步骤](##步骤)
  - [参考](##参考)

# 摘要
这篇文章介绍了在Hugo博客中如何引用本地图片，提供了两种选择：使用 图床 或使用 本地图片，并详细说明了使用本地图片的操作步骤。

## 事实
- 📁 Hugo博客的根目录包含一个static目录，用于存放静态文件，如图片、CSS和JS文件。
- 📦 执行hugo命令时，会将static目录下的子目录或文件复制到public目录，以供网站展示。
- 🖼️ 要在markdown文章中引用本地图片，需要将图片放置在static目录下的img子目录中。
- 📝 在markdown文件中，可以按照指定格式引用图片，例如：`![图片名称](/test/图片文件名.png)`
- 🚀 执行hugo命令并启动hugo server后，可以在本地预览文章中的图片。

## 步骤
1. 在Hugo博客的根目录下创建一个static目录。
2. 在static目录下创建一个test子目录，用于存放图片文件。
3. 将图片文件放置在test子目录中。
4. 在markdown文件中引用图片，例如：`![图片名称](/test/图片文件名.png)`
5. 执行hugo命令并启动hugo server，查看文章中的图片是否正常显示。

### 预览
---

![alt text]("/test/image.png")
![alt text]("/test/image-1.png")


### 引用

--- 
![alt text]("/test/image.png")

# 参考
- [Hugo中文文档](https://www.gohugo.org/)
- [Hugo如何在markdown里引用本地图片](https://jincheng9.github.io/post/hugo-add-img/)