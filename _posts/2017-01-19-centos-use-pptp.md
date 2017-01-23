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

另外需要注意的是有的时候连上VPN了， 内网却链接不上了， 那是因为路由没有设置好的， 我在这里卡了好长时间， 我的数据库放在了内网， 而且是另外一个网段。具体如下：

应用服务器放在A段， IP是 10.0.0.151
数据库放在了B网段， IP是 10.0.2.211

使用命令 traceroute  10.0.1.211， 发现直接走到了ppp0那边去了， 所有解决方法很简单就是加一条路由

`ip route replace 10.0.1.211 via 10.0.0.1 dev eth0 src 10.0.0.151`

这里 10.0.0.1 是A网段的网关， 这样路由寻址的时候就会先走这条路由， 就可以内网外网都接上了.
