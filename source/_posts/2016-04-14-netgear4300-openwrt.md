---
title: Netgear WND4300刷OpenWrt
categories:
- 折腾
description: 玩转路由器
tags:
- openwrt
- netgear
---
OpenWrt是适合于嵌入式设备的一个Linux发行版。相对原厂固件而言，OpenWrt不是一个单一、静态的固件，而是提供了一个可添加软件包的可写的文件系统。（摘自维基）也是说他提供了一个最小的满足功能的linux路由系统。而后期用户可通过安装软件包来增加它的功能，实现可定制化。

最近在淘宝入了个二手Netgear 4300，198RMB。主要想解决一下家里原先路由经常断网的问题，还有想折腾下OpenWrt，据说美帝的网件不但质量好，还能：单号多拨榨取运营商带宽、绑定域名远程控制、挂载大容量硬盘、搭建BT下载机、搭建网络摄像头、Samba/DLNA家庭NAS共享、私有云同步、FTP、个人网站/服务器…（留待以后慢慢研究，先说下刷入OpenWrt的过程）

* 路由器型号：Netgear WND4300
* OpenWrt版本：15.05.1
* 刷机使用操作系统：Ubuntu14.04

## 首先，固件下载

不同的路由根据CPU型号的不同，所选择的固件也不同，需要在[官网](http://downloads.openwrt.org)选择相对应的固件。 

4300所对应的固件是[openwrt-ar71xx-nand-wndr4300-ubi-factory.img](https://downloads.openwrt.org/chaos_calmer/15.05.1/ar71xx/nand/openwrt-15.05.1-ar71xx-nand-wndr4300-ubi-factory.img)

以及升级包[openwrt-ar71xx-nand-wndr4300-squashfs-sysupgrade.tar](https://downloads.openwrt.org/chaos_calmer/15.05.1/ar71xx/nand/openwrt-15.05.1-ar71xx-nand-wndr4300-squashfs-sysupgrade.tar)

下载完放在~/Download 目录

## 进入tftp模式刷入固件

> 据说4300支持通过网页终端直接刷入固件的，但这样实在没意思，所以没去试

网件Netgear WNDR4300路由器进入恢复模式的方法

* 关闭路由器电源
* 用 牙签，或其他尖物 按住设备背面的机身背面的红色小圆孔(Restore Factory Settings button)
* 开启电源开关
* 观察电源灯（此时保持按住Restore Factory Settings按钮不要松手），直到电源灯由**橙色闪烁**状态变到**绿色闪烁**状态（说明设备已经进入到了 TFTP修复模式 ）

电脑网线连上路由的lan接口，手工设置本地地址为192.168.1.2/24，接着测试连通性：

	$ ping 192.168.1.1

安装tftp
	
	$ sudo apt-get install tftp

开始通过tftp进入路由器刷入固件
	
	$ tftp 192.168.1.1
	tftp> trace
	Packet tracing on.
	tftp> binary
	tftp> put openwrt-ar71xx-nand-wndr4300-ubi-factory.img
	sent WRQ <file=openwrt-ar71xx-nand-wndr4300-ubi-factory.img, mode=octet>
	received ACK <block=0>
	sent DATA <block=1, 512 bytes>
	...
	received ACK <block=4745>
	Sent 2428928 bytes in 6.2 seconds
	tftp> quit
	$

刷机完毕后，请重启，以规避首次启动，无线初始化有问题的问题（好绕口），才能够启用5G性号。

## 首次进入路由设置

电脑终端重新把IP改为DHCP模式，web端输192.168.1.1进入，初始用户名root，初始密码空，先设置web终端管理密码
升级安装包openwrt-ar71xx-nand-wndr4300-squashfs-sysupgrade.tar通过web端进行安装

接着可以通过web终端配置wlan口的互联网接入了，看具体接入方式：PPPoE，DHCP，静态IP等

此时还没法通过ssh进入路由，需通过telnet进入设置密码方能使用

	$ telnet 192.168.1.1
	# passwd

passwd设置密码后，ssh 功能启用

	$ ssh root@192.168.1.1

跟新软件源列表

	root@OpenWrt:/tmp# opkg update

至此基本操作完成，可以自由冲浪了，再安装shadowsock、usb、离线下载.......

> 参考

* [网件Netgear WNDR4300路由器怎样刷OpenWrt自动翻墙固件](https://github.com/softwaredownload/openwrt-fanqiang/blob/master/ebook/wndr4300/5.wndr4300-flash-fanqiang-img.md)
* [WNDR4300 折腾 openwrt 记](http://dlmao.com/wndr4300-%E6%8A%98%E8%85%BE-openwrt-%E8%AE%B0.html)
* [OpenWRT安装Shadowsocks和ChinaDNS](https://www.ifshow.com/openwrt-install-shadowsocks-and-chinadns/)
* [OpenWrt智能、自动、透明翻墙路由器教程](https://softwaredownload.gitbooks.io/openwrt-fanqiang/content/ebook/03.1.html)
* [WNDR4300刷OpenWrt手记](http://blog.csdn.net/zhiyuan411/article/details/41399273)
