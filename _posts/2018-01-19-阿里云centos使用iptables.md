---
layout: post
title:  阿里云centos使用iptables
date:   2018-01-19
---

* Centos 7 默认的防火墙是 firewall ，鉴于 iptables 使用的比较广，所有关掉 firewall ，使用 iptables .

#### 检测并关闭firewall
* 使用 systemctl status firewalld 查看服务状态，active/inactive表明服务是运行/关闭状态
* `systemctl status firewalld` #检测是否开启了firewall
* `systemctl stop firewalld` #关闭firewall
* `systemctl disable firewalld` #禁用firewall

#### 安装 iptables
* `yum install -y iptables-services`
-
#### 设置 iptables
* `systemctl start iptables` #启动iptables
* `iptables -L -n` #查看 iptables 默认规则，默认规则配置文件`/etc/sysconfig/iptables`
* `cp -a /etc/sysconfig/iptables /etc/sysconfig/iptables.bak` #清空规则前可先备份
* `iptables -F` #清空服务器上所有的规则
* `iptables -P INPUT DROP` #设置 INPUT 方向所有的请求都拒绝，这条策略加上以后所有访问服务器的请求全都会被拒绝掉，ssh登录将会断掉，小心操作。
* 前面设置好后，只是临时的，重启服务器还是会恢复原来没有设置的状态，还要使用 `service iptables save` 进行保存，这样`/etc/sysconfig/iptables`文件里才会改变
* 此时ssh及80端口都不能访问，我们需要放行常用端口。
* 执行命令`iptables -A INPUT -p tcp --dport 22 -j ACCEPT` 然后执行`service iptables save` 保存进`/etc/sysconfig/iptables`文件里。
* 不能直接修改`/etc/sysconfig/iptables`配置文件，想要添加规则，或删除规则，用命令。
* `systemctl enable iptables.service` 设置 iptables 开机启动



参考:
>[阿里云Centos配置iptables防火墙](https://www.cnblogs.com/suihui/p/4334224.html)
>[centos 7 配置iptables](https://www.cnblogs.com/qbyyqhcz/p/6007053.html)
>[iptables规则的查看、添加、插入、删除和修改](http://blog.csdn.net/l241002209/article/details/43987933)