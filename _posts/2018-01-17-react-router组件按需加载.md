---
layout: post
title:  react-router组件按需加载
date:   2018-01-17
---

1.配置webpack，项目使用create-react-app生成，在webpack.config.dev.js加入如下代码：

``` js
output: {
    chunkFilename: 'static/js/[name].chunk.js',
    ...
}

plugins: [
    // 提取公共代码
    new webpack.optimize.CommonsChunkPlugin({
        name: 'common',
        filename: 'static/js/common.js'
    }),
    ...
]
```

2.在webpack.config.prod.js加入如下代码：

``` js
output: {
    chunkFilename: 'static/js/[name].[chunkhash:8].chunk.js',
    ...
}

plugins: [
    // 提取公共代码
    new webpack.optimize.CommonsChunkPlugin({
        name: 'common',
        filename: 'static/js/common.[chunkhash:8].js'
    })
    ...
]
```

3.如果使用的是webpack1.x版本，则plugins里需要写成：
`new webpack.optimize.CommonsChunkPlugin('common', 'static/js/common.js'）` 或
`new webpack.optimize.CommonsChunkPlugin('common', 'static/js/[name].[chunkhash:8].chunk.js'）`

4.在路由组件中：

``` js
const App = (nextState, callback) => {
    require.ensure([], function (require) {
        callback(null, require('../containers/App').default);
       }, 'app');
};

<Route path="/" getComponent={App} >
```











