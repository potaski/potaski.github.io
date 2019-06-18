---
layout: post
title:  "Vue.js学习笔记"
categories: 学习笔记
tags: 前端 vue 学习笔记
author: ZhangWei
---

* content
{:toc}

越来越觉得在web开发上消耗大量时间是非常错误的

所以下定决心学习一个通用的框架，那么就是 [Vue.js](https://cn.vuejs.org/v2/guide/) 了

## Date: 20190618

### 最小化vue示例

```html
<div id="app">{{ message }}</div>
<script>
    var app = new Vue({
        el: "#app",
        data: {
            message: "hello world"
        }
    })
</script>
```

基本用法

1. 元素绑定：el: "#app"
2. 数据模板（类似jinja）：{{ message }}实际为app.message
3. 数据绑定：打开console重新给app.message赋值，页面随之改变
4. 数据绑定解除：Object.freeze(app)，执行后不再追踪数据

其它用法
1. app.$data === data
2. app.$el === document.getElementById('example')

### 生命钩子

目前暂时用不上，实际开发时再用吧

[点我看图](https://cn.vuejs.org/images/lifecycle.png)

### vue构成单元

```html
<script>
    var appname = new Vue({
        el: "#html元素的ID",
        data: {
            message: "静态数据，可为字符串或列表或其它"
        },
        methods: {
            // <button v-on:click="editMessage">触发函数，重新赋值</button>
            editMessage: function() {
                this.message = "其它东东"
            }
        }
    })
</script>
```