---
layout: post
title: vue-cli项目引入jquery
---

1.`npm install jquery --save` <br>
2.打开文件 `build/webpack.base.conf.js` ，添加如下代码：<br>
``` js
var webpack = require("webpack")

module.exports = {
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jquery: 'jquery',
      'window.jQuery': 'jquery',
      jQuery: 'jquery'
    })
  ]
  ...
} 
```

3.打开 `.eslintrc.js` 添加如下代码：
``` js
module.exports = {
  globals: {
    "$": true,
    "jQuery": true
  },
  ...
```
4.现在可以在你的项目中使用 `$` 了