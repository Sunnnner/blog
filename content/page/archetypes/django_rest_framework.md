---
title: "Django_rest_framework"
date: 2019-09-08T11:37:47+08:00
draft: true
# weight: 1
# aliases: ["/first"]
tags: ["drf"]
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

为什么要使用Django_rest_framework
    能自动生成restful规范的API

    代码简介 并且开发速度快

Django_rest_framework框架有什么组件
    序列化组件：serializers 对queryset序列化及对请求数据格式校验

    路由组件：routers 进行路由开发

    视图组件： ModelViewSet 帮助开发者提供了一些类。 并在类中提供了多个方法

    认证组件： 写一个类并注册到选线类（authentication_classes）， 再类的authticate方法中编写认证逻辑

    权限组件：写一个类并注册到权限类（permission_classes）, 在类中的has_permission方法中编写认证逻辑

    频率限制： 写一个类并注册到频率类（throttle_classes）, 在类中的allow_request/wait方法中编写认证逻辑

    解析器 选择对数据解析的类， 在解析类中注册(parser_classes)

    渲染器 定义数据如何渲染到页面上， 在渲染器类中注册(render_classes)

    分页 对获取到的数据进行分页处理 pagination_class

    版本 版本控制用来在不同的客户端使用不同的行为

    在URL中设置version参数， 用户请求时候传入参数， 在request.version中获取版本, 根据版本不同，做不同处理

django rest framework框架的认证流程
    用户请求走进来进入APIView， 初始化了默认的认证方式

    进入APIView.dispatch()方法， initial方法调用了request.user

    如果我们配置了认证类， 走我们自己认证类中的authentication方法

django rest framework如何实现的用户访问频率控制
    使用ip/用户账户作为建， 每次访问时间作为值， 构造一个字典数据， 存起来， 每次访问对时间列表进行判断

    把没有访问的超时的删掉。 在计算列表剩余的元素就能做到频率限制了

    匿名账户， 使用IP控制， 但是无法完全控制， 因为用户可以更换代理IP

    登陆用户使用账号控制，但是如果有很多账号，也无法限制

如何实现用户登陆认证
    cookice session

    token 登陆成功后生成的加密字符串

    JWT： json wed token 缩写， 他讲用户信息加密到token中 服务器不保存任何用户信息， 服务器通过使用保存的密匙来验证token的正确性

rest_framework序列化组件的作用,以及一些外键关系的钩子方法

    作用：帮助我们序列化数据
    ```python
    1.choices  get_字段名_display
    2.ForeignKey source=orm 操作
    3.ManyToManyFiled  SerializerMethodField()
                        def get_字段名():
                        return 自定义
    ```

PV 和 UV

    pv :页面访问量打开一次算一次刷新也算

    uv ： 独立访问数， 一台电脑算一个访客

