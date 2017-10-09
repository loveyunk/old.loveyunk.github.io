---
layout: post
title: 原生js点击toggle方法
---

两次点击事件进行切换
{% highlight ruby%}
const toggle = (() => {
    let a = true;
    return (fn1, fn2) => {
        a = !a;
        let toggler = () => {
            return a ? fn1 : fn2;
        };
        return this.onclick = toggler();
    }
})();
{% endhighlight %}
使用
{% highlight ruby%}
let div = document.querySelector('div');
div.onclick = function () {
    toggle(function () {
        alert(1);
    }, function () {
        alert(2);
    });
};
{% endhighlight %}