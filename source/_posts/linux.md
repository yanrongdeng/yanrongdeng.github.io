---
title: Linux中常用操作命令
date: 2018-08-11 09:47:37
tags: Linux
categories: 学习笔记
---

工作中Linux中常用操作命令

|执行操作| 命令1 | 命令2 | 备注(实例) |
|:--:|--|--|--|
|<b>查看目录| ls |  |  |
|<b>进入目录| cd 目录名称 |  |  |
|<b>开始服务| service tomcat start | | /usr/local/tomcatgroup2/tomcat203/bin/catalina.sh start |
|<b>结束服务| service tomcat stop | | /usr/local/tomcatgroup2/tomcat203/bin/catalina.sh stop |
|<b>复制文件| cp -r 要复制文件路径 将要复制到的路径 | | \cp -r /data/smbshare/insy/index.html /usr/longrise/insytest/WEB-INF/ResourceLib.TMP/insytest/LEAP/html |
|<b>打开文件| cat 要打开的文件路径 | | cat /usr/longrise/insytest/WEB-INF/ResourceLib.TMP/insytest/LEAP/html/insy.html |
|<b>删除文件| rm -rf 要删除的文件路径 | | rm -rf /usr/local/tomcatgroup2/tomcat203/logs/* |
|<b>编辑文件| vim 要编辑的文件路径 | |  vim /usr/longrise/insytest/WEB-INF/ResourceLib.TMP/insytest/LEAP/html/insy.html<br/>执行vim命令后，按字母i，即可开始编辑；编辑完成后按“Esc”键，然后输入“：wq” |
|<b>复制| Ctrl + insert |
|<b>粘贴| shift+ insert |
|<b>退出| ctrl+c |
|<b>获取权限| sudo rz -be | |
|<b>修改权限| chown -R tomcat:tomcat 文件路径 | | chown -R tomcat:tomcat /usr/longrise/insyi |
|<b>解压压缩包| sudo unzip -o 压缩包名 | | sudo unzip -o prd.zip |
|<b>查看进程| ps -ef&#124;grep tomcatA04 | ps -aux |
|<b>杀死进程| kill -9 n |  | n由查看进程查出来的 |
|<b>查看ip |ipconfig |
|<b>ip指向代理| vim /usr/local/nginx/conf/upstream.conf | vim /usr/local/nginx/conf/nginx.conf | location ^~ /COMMONPAYDYR/{<br>proxy_pass http://COMMONPAYDYR;<br>}<br>location ^~ /insyi/{<br> #root /usr/longrise/insyiTEST/WEB-INF/ResourceLib.TMP/insyiTEST/LEAP/html;<br>root /usr/longrise/insyi;<br>  proxy_pass http://insyi;<br>} |
|<b>启动nginx| /usr/local/nginx/sbin/nginx -s reload |
|<b>查看网关| netstat -rn |
|<b>查看DNS| cat /etc/resolv.conf |
|<b>查看主机名| hostname |
|<b>查看操作系统版本| cat /etc/issue| cat /proc/version|uname -a|
|<b>查看hosts| cat /etc/hosts |
|<b>查看cpu信息| cat /proc/cpuinfo |上图有几个比较重要的指标：<br/>processor ：逻辑处理器的id。<br/>physical id ：物理封装的处理器的id。<br/>core id ：每个核心的id。<br/>cpu cores ：位于相同物理封装的处理器中的内核数量。<br/>siblings ：位于相同物理封装的处理器中的逻辑处理器的数量。|physical id，有两项，说明物理硬件cpu有两个；<br/>cpu cores 的值为8，这也就说明了我的CPU是八核心的；<br/>processor的值有32个，这说明，逻辑cpu有32个；|
|<b>查看内存信息| cat /proc/meminfo| free -g|top|
|<b>查看磁盘信息| df -h |
|<b>查看端口占用| lsof -i:50070 |netstat -tunlp &#124; grep 50070|
|<b>查找异常| less 文件路径 &#124; grep 'message描述'  | | less /usr/local/tomcatgroup/tomcatA09/logs/catalina2019-03-21_16_12_10.out &#124; grep 'message描述' |
|<b>保易测试环境logs| | | tail -f /usr/local/tomcatgroup2/tomcat203/logs/catalina.out |
|<b>十二五测试环境logs| | |tail -f /usr/local/tomcatgroup2/tomcat210/logs/catalina.out |
|<b>国开219环境logs| | | 冒烟 /usr/local/tomcatgroup/tomcatA47/logs <br/> 测试 /usr/local/tomcatgroup/tomcatA40/logs/ |
