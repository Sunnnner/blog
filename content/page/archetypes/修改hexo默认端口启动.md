---
title: "修改hexo默认端口启动"
date: 2018-06-04T10:25:30+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["hexo"]
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

- 默认使用4000端口，用`hexo s -p 80`，可以暂时修改启动端口。

- 但是每次启动都要写”-p 80”才行，过于繁琐。

- 修改方法：
`找到node_modules\hexo-server\index.js文件，可以修改默认的port值！`
