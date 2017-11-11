---
layout: post                      
title:  Address already in use问题解决方法
date:   2017-11-07     
---

1. 表示端口被占用，有另一个进程也在监听此端口，可以使用以下命令来打到此进程：<br>
`lsof -i :8080(端口号)`

2. 然后杀掉进程，执行命令：<br>
`sudo kill -9 <process_id>`
