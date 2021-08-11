---
title: nginx 设置本机域名
date: 2017-06-09 16:42:22
tags: Nginx
categories: 小知识
---

1. 打开 hosts 文件
方法一：
路径： C:\Windows\System32\drivers\etc\hosts ![设置代理](https://img-blog.csdnimg.cn/e97b7ff2e14642818ea128ff0e495786.png) 方法二：
安装 SwitchHosts! 可直接打开 hosts 文件编辑![在这里插入图片描述](https://img-blog.csdnimg.cn/6f80691ae2c64dd3a72aa5ba3a739034.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)添加到 hosts 文件中 `127.0.0.1 dengyr.com` （缺点：不能去掉端口） 
访问链接：http://dengyr.com:3000/html/truthlist.html

2. 微信 web 开发者工具
移动调试-》ios 设备调试-》本机地址-》在手机上设置代理 192.168.3.246 9973 -》开始调试

3. 启动 nginx
D:\nginx-1.11.13\conf\nginx.conf（下载 nginx 放在D盘）
添加到 nginx.conf 文件中  `proxy_pass http://192.168.3.246:3000;` （去掉端口）![设置代理](https://img-blog.csdnimg.cn/2e940488b4b248e4b39bfd80c2a0b793.png)在 D:\nginx-1.11.13 目录下，右键 `git bash Here`，输入命令 `start nginx`
>
>nginx 的命令
>**启动命令：** `start nginx`
>**关闭命令：** `./nginx.exe -s stop`
>**重启命令：** `./nginx.exe -s reload`

访问链接：http://dengyr.com/html/truthlist.html 