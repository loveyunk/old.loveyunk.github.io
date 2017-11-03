---
layout: post
title: 当Promise遇上for循环
---

for循环中进行异步操作,此时在循环之后使用resolve()并不能获取到异步后的值,只能得到原始值或undefined
{% highlight ruby%}
new Promise(resolve => {
    let a = 0;
    for (let i = 0; i < 10; i++) {
        setTimeout(() => {
            a++;
        }, 10);
    }
    resolve(a);
}).then(res => {
    console.log(res); // 0
});
{% endhighlight %}
而将resolve()写入循环异步之中,也只能得到第一次循环的值,因为resolve之后状态改变,不会再变回来
{% highlight ruby%}
new Promise(resolve => {
    let a = 0;
    for (let i = 0; i < 10; i++) {
        setTimeout(() => {
            a++;
            resolve(a);
        }, 10);
    }
}).then(res => {
    console.log(res); // 1
});
{% endhighlight %}
解决方案1: 
初始化一个变量,每次在回调后加一,直至与循环数一致
{% highlight ruby%}
new Promise(resolve => {
    let a = 0;
    let flag = 0;
    for (let i = 0; i < 10; i++) {
        setTimeout(() => {
            a++;
            flag++;
            if (flag === 10) {
                resolve(a);
            }
        }, 10);
    }
}).then(res => {
    console.log(res); // 10
});
{% endhighlight %}
解决方案2:
{% highlight ruby%}

{% endhighlight %}

参考:
>[http://blog.csdn.net/canot/article/details/73505891](http://blog.csdn.net/canot/article/details/73505891)