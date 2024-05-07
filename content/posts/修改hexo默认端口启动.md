---
title: "修改hexo默认端口启动"
date: 2018-06-04T10:25:30+08:00
draft: false
categories:
  - hexo
---
<!--more-->
- 默认使用4000端口，用`hexo s -p 80`，可以暂时修改启动端口。

- 但是每次启动都要写”-p 80”才行，过于繁琐。

- 修改方法：
`找到node_modules\hexo-server\index.js文件，可以修改默认的port值！`
