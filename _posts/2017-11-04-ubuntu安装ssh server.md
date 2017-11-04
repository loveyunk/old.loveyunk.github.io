---
layout: post                      
title:  ubuntu安装ssh server
date:   2017-11-04      
---

### SSH介绍
* SSH是Secure Shell的缩写，SSH 为建立在应用层和传输层基础上的安全协议。
* SSH是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。
* SSH是一种可以保证用户远程登录到系统的协议。
* 利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。
* SSH客户端适用于多种平台，UNIX，Linux，Windows等。

### OpenSSH
* SSH分为客户端openssh-client和服务端openssh-server。
* OpenSSH是SSH的开源实现，因此用户可以免费使用到这种安全服务。
* ssh是一种协议，openssh是一种实现。
* 一句话概括OpenSSH：使用加密的远程登录实现，可以有效保护登录及数据的安全。
* openssh-client用于本机去连接其他机器。
* openssh-server让别的机器可以连接本机。

### SSH安装及使用
* 如果只是要连接其他机器，安装openssh-client客户端即可，Ubuntu一般是默认安装好的。安装命令如下：
```
sudo apt-get install openssh-client 
```
* ubuntu自带的有openssh-client,所以可以通过如下命令来远程连接linux
```
ssh username@IP // username为远程机器上的用户名,IP为远程电脑的IP地址。
```
* 可是要想通过ssh被连接,ubuntu系统需要有openssh-server,可以通过如下命令来查看,如果没有显示sshd则说明没有安装openssh-server,如果有```sshd```则说明SSH服务端已经启动，可以使用其他电脑连接了。
```
ps -e | grep ssh
```
* 可通过如下命令来安装openssh-server
```
sudo apt-get install openssh-server
```
* 还可用如下命令来判断是否安装ssh服务，如果出现让输入密码，则表示安装成功。
```
ssh localhost
```
* 启动SSH：
```
sudo service sshd start
```
* 关闭SSH：
```
sudo service sshd stop
```
* 重启SSH：
```
sudo service sshd restart
```
* 检查SSH连接状态：
```
service sshd status
```
* 修改配置文件：打开配置文件，配置文件是```etc/ssh/sshd_config```使用文本编辑器打开，可修改其配置








