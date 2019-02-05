---
title: SSH免密码登录服务器设置
date: 2019-02-04 23:36:08
tags:
- ssh
---
# 什么是ssh

{% blockquote 维基- https://zh.wikipedia.org/wiki/Secure_Shell ssh %}
Secure Shell（安全外壳协议，简称SSH）是一种加密的网络传输协议，可在不安全的网络中为网络服务提供安全的传输环境[1]。SSH通过在网络中创建安全隧道来实现SSH客户端与服务器之间的连接[2]。虽然任何网络服务都可以通过SSH实现安全传输，SSH最常见的用途是远程登录系统，人们通常利用SSH来传输命令行界面和远程执行命令。
{% endblockquote %}

ssh 登录时有两种验证方式：

1.基于密码的安全验证

2.基于密钥的安全验证

# 基于密码登录的配置

1.先在本地终端生成密钥对

{% codeblock lang:shell %}
:~$ ssh-keygen //加密方式默认使用RSA，如果加参数-t，选择加密方式
{% endcodeblock %}

按Enter全部选择默认就好，此时会在.ssh/目录下生成id_rsa和id_rsa.pub的私钥文件和公钥文件

{% codeblock %}
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/user/.ssh/id_rsa.
Your public key has been saved in /home/user/.ssh/id_rsa.pub.
The key fingerprint is:
...
{% endcodeblock %}

2.把生成的公钥文件拷贝到服务器端对应帐号的.ssh/目录下，并改名为authorized_keys
{% codeblock %}
:~/.ssh$ scp id_rsa.pub user@server-ip:/home/user/
:~$ mv id_rsa.pub ./.ssh/authorized_keys
{% endcodeblock %}

3.并修改.ssh/和authorized_keys两个的权限
{% codeblock %}
:~$ chmod 700 ~/.ssh/
:~$ chmod 600 ~/.ssh/authorized_keys
{% endcodeblock %}

4.验证是否成功
{% codeblock %}
:~$ ssh user@server-ip
{% endcodeblock %}
