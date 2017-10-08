---
layout: post
title: 通过jQuery Ajax上传文件
---

{% highlight ruby%}
let form = new FormData();
form.append("png_file", file);
$.ajax({
    type: 'POST',
    url: '',
    dataType: 'json',
    catch: false,
    "processData": false,
    "contentType": false,
    "mimeType": "multipart/form-data",
    "data": form
}).done(res => {
    console.log(res);
});
{% endhighlight %}

* processData设置为false。因为data值是FormData对象，不需要对数据做处理。
* cache设置为false，上传文件不需要缓存。
* mimeType为multipart/form-data
* contentType设置为false。不对表单内容进行编码。
* mimeType与contentType起到enctype="multipart/form-data"的作用

enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码(MIME type)。
默认地，表单数据会编码为 "application/x-www-form-urlencoded"。就是说，在发送到服务器之前，
所有字符都会进行编码（空格转换为 "+" 加号，特殊符号转换为 ASCII HEX 值）。
当 method 属性值为 post 时, enctype 是提交form给服务器的内容的 MIME 类型 。可能的取值有:
* application/x-www-form-urlencoded: 在发送前编码所有字符（默认）.
* multipart/form-data: 这个类型允许`<input type="file">`上传文件。在使用包含文件上传控件的表单时，必须使用该值,
它不会对字符进行编码，一般用于传输二进制文件（图片、视频、、、）.
* text/plain: 空格转换为 "+" 加号，但不对特殊字符编码.
以上是默认以form表单形式提交的时候，以ajax形式不通过form表单形式提交，则需自行指定MIME type，及进行自行编码。
ajax post方式则需将Content-type头信息设置为application/x-www-form-urlencoded，且需对表单进行序列化。
而能过jquery ajax形式，ContentType默认为application/x-www-form-urlencoded

参考：
> [通过jQuery Ajax使用FormData对象上传文件](http://blog.csdn.net/xllily_11/article/details/52330280)
> [HTMLFormElement.enctype](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/enctype)
