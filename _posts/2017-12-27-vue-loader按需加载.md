---
layout: post
title:  vue-router路由懒加载
date:   2017-12-27
---

``` js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)

export default new Router({
  routes: [
    {
        path: '/',
        component: resolve => require(['components/Hello.vue'], resolve)
    },
    {
        path: '/about',
        component: resolve => require(['components/About.vue'], resolve)
    }
  ]
})
```


``` js
const Home = (resolve) => {
    import('@/views/home').then(module => {
        resolve(module);
    });
};
```
