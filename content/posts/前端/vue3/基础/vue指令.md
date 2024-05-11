---
title: "vue指令"
date: 2023-04-19T10:52:21+08:00
draft: false
categories:
  - 前端
tags:
  - vue
---

<!--more-->

*   使用工具初始化vue项目
*   npm

```sh
# npm 6.+
npm init vite@latest demoprojectname --template vue

# npm 7.+
- npm init vite@latest demoprojectname -- --template vue

```

*   yarn

```sh
yarn create vite project_name --template vue

cd project_name

yarn 

yarn dev

```

*   `v-bind` 将这个元素节点的`title`attribute和当前活跃实例的`message`property保持一致
*   to对象的点击

```typescript
# template

<div><button @click="change"></button></div>

<div>{{ state}} </div>

# script

import {toRef reactive} from 'vue'

const data = reactive({
    count: 1,
})

const state = toRef(data, 'count')

const change = () => {
    state.value++
}

```

*   上面的代码代表响应式刷新

*   `computed` 计算属性就是当依赖的属性的值发生变化的时候，才会触发它的更改，如果依赖的值不变，则使用缓存中的属性值

*   `reduce`与`reduceRight` 数组归并方法， 这两个方法都会迭代数组中的所有项，并在此基础上构建一个返回值。reduce从第一到最后，reduceRight从最后到第一

*   reduce接受四个参数`reduce((prev,next) => {return prev + (netx)}, 0)` prev代表当前计算所得的值，next代表下一个值, 默认返回0

*   `watch`监听函数可以获取改变后的值与改变前的值

*   `watchEffect` 立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更的时候重新运行该函数，非惰性，会默认执行一次

*   `watchEffect` 清除副作用，可以处理你的逻辑例如防抖动

#### 父子组件传参

*   父组件通过`v-bind`绑定一个数据，然后子组件通过`defineProps`接受过来的值
*   父组件绑定值后面跟随的参数`:xx`一定要与子组件`defineProps`中定义的值一致
*   父组件向子组件使用bind一类的函数进行传参
*   子组件向父组件传参使用defindxxx一类的默认函数

#### 动态组件

*   vue 中style中的`scoped` 是为了避免css样式之间的污染，当一个style标签拥有`scoped`这个属性的时候，他的css样式只作用于当前组件，通过设置该属性，使组件之间的样式不互相污染
*   在一个style中书写样式我们可以使用`@xxx`来了表示公有属性
*   在同一组类型样式中`&`代表当前类型样式名称

```css
<style lang="less" scoped>
    @border: #ccc
    
    .card{
        border: 1px solid @border;
        &:hover {
            box-shadow: 0 0 10px @border;
        }
        &-content {
            padding: 10 px;
        }
    }
</style>

```

*   普通函数与箭头函数：普通函数中的this指向是动态的，箭头函数中的this是静态的
*   css 中组件不能铺满全屏的原因是因为`margin`边框数据太大我们改成`-8px -8px auto`就可以了
