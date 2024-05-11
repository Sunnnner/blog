---
title: "vue-router路由"
date: 2023-04-19T10:52:21+08:00
draft: false
categories:
  - 前端
tags:
  - vue
---

<!--more-->

*   首先我们在`components`文件夹下创建`router`文件夹，然后创建`index.ts`,这是我们路由书写的文件

*   `index.ts`内容

```typescript
import {createRouter,createWebHistory, RouteRecordRaw} from 'vue-router'

const routes: Array<RouteRecordRaw> = [{
    path: '/',
    name: 'a',
    component: () => import('../xxx/xx.vue')
}]

const router = createRouter({
    history: createWebHistory,
    routes
})

```

*   随后我们在`main.ts`中导入router文件夹 `import router from './router'`,然后使用`use(router)`我们就搭建起了vue的路由环境

*   编程式导航

```typescript

<script setup lang='ts'>

import {useRouter} from 'vue-router'

const router = useRouter();

#字符串路由
const toPage = () => {
    router.push('/')
}

# 对象path路由

const toPage = () => {
    router.push({
        path: '/'
    })
}

# 对象名称路由
const toPage = () => {
    router.push({
        name: 'home'
    })
}

# 参数路由
const toPage = (url:string) => {
    router.replace(url)
}

# 路由历史-前进
const next = () => {
    router.go(1)
}

# 后退
const prev = () => {
    router.back()
}

# 路由传参

const toDetail = (item: Item) => {
    router.push({
        path: 'reg',
        query: item
    })
}

# params传参

const toDetail = (item: Item) => {
    router.push({
        name: 'Reg',
        params: item
    })
}


</script>

<template>
    # router-link 跳转方式
    <router-link replace to="/"> </router-link>
</template>


```

*   路径参数用冒号`:`表示，当一个路由被匹配时，它的params的值将在每个组件

```typescript

# router/index.ts

const router: Array<RouteRecordRaw> = [
    {
        path:'/',
        name: 'Login',
        component: () => import('../xxx/xx.vue')
    },
    {
        path: '/reg/:id',
        name: 'Reg',
        component: () => import ('../xxx/xxx.vue')
    }
]

# xx.vue script

const toDetail = (item: Item) =>{
    router.push({
        name: "Reg",
        params: {
            id: item.id
        }
    })
}

import {useRouter} from 'vue-router'
import {data} from './test.json'
const router = useRouter();
const item = data.find(v => v.id === Number(router.params.id))

```

*   区别
    *   query传参配置是path，而params传参配置的是name，在params中配置path无效
    *   query在路由配置不需要设置参数，而params必须设置
    *   query传递参数会显示在地址栏中
    *   params传参刷新会无效，但是query会保存传递过来的值，刷新不变
    *   路由配置

*   命名视图

*   在同一级展示更多的路由视图，而不是嵌套显示，命名视图可以让一个组件中具有多个路由渲染出口，这对于一些特定的布局组件非常有用，视图的默认名称是`default()`

*   视图使用多个组件时，确保components配置正确

```typescript

# router/index.ts
const router: Array<routerRecordRaw> => [
    {
        path: '/',
        components: {
            default: () => import('../../xx.vue')
            header: () => import('../../xx.vue')
            content: () => import('../../xx.vue')
        }
    }
]

const router = createRouter({
    history: createWebHistory(),
    router
})

export default router

```

*   对应的我们使用`router-view`组件进行渲染

```html

<div>
    <router-view></router-view>
    <router-view name='header'></router-view>
    <router-view name='content'></router-view>
</div>

```

*   重定向`redirect`

```typescript

# router/index.ts

const router: Array:<routerRecordRaw> => [
    {
        path: '/'
        name: 'home'
        components :() => import('../../xx.vue') 
    },{
        path: '/reg',
        name: 'reg',
        # 字符串
        redirect: '/',
        # 对象形式
        redirect: {path: '/'},
        # 函数形式(可以传参数)
        redirect: (to) => {
            return{
                path: '/',
                query: to.query
            }
        }，
        # 别名alias
        alias: ["/root", "/root2"]
        components: () => import('../../xx.vue')
    }
]

```