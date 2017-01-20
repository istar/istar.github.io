---
layout:     post
title:      "run pptp client on Centos"
date:       2017-01-19 12:00:00
author:     "Star"
catalog: true
tags:
    - Linux
    - CentOs
    - PPTP
---


安装:

`yum install pptp pptp-setup`

设置用户名和密码:

`pptpsetup --create vpn --server 127.0.0.1 --username yourname --password yourpwd`

运行:

`pppd call vpn`

如果连接上了可以查看网卡是否有ppp0了

`ifconfig`

这时候需要把ppp0设置为默认路由

`ip route replace default dev ppp0`

查看ip

`curl http://icanhazip.com`

关闭

`killall pppd `

重启网络恢复

`/etc/init.d/network restart`

