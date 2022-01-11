---
title: 攻防学习
author: 搬运工，详情见末尾
date: '2021-11-11'
slug: 搬运工
categories:
  - Example
tags: []
---
网上相关资料

- [Kali Linux教程](https://www.it1352.com/OnLineTutorial/kali_linux/kali_linux_information_gathering_tools.html)
- [SQL手工注入方法](https://www.cnblogs.com/mutudou/p/11757182.html)
- [Web安全攻防笔记-SQL注入](https://www.cnblogs.com/zh2000/p/11778089.html)
- [子域名挖掘方法](https://blog.csdn.net/qq_43468607/article/details/97035484)
- [一次通过漏洞挖掘成功渗透某网站的过程](https://cloud.tencent.com/developer/article/1035284)
- [深入了解子域名挖掘tricks](https://www.cnblogs.com/linuxsec/articles/12019160.html)
- [Nmap扫描基础常用命令(包含进阶使用)](https://www.cnblogs.com/iAmSoScArEd/p/10585863.html)
- [VSFTP2.3.4（笑脸漏洞）渗透测试](https://www.cnblogs.com/Renqy/p/12660646.html)
- [简单的metasploit使用-vsftpd漏洞利用](https://blog.csdn.net/qq_24601451/article/details/82789719)
- [metasploit 渗透测试（ftp）](https://blog.csdn.net/xul2009/article/details/23596241?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight)
- [提权，代理，内网渗透（针对445端口）](https://www.cnblogs.com/G-Shadow/p/10965035.html)
- [内网渗透测试1](https://www.cnblogs.com/wjw-zm/p/11677051.html)
- [内网渗透测试2](https://recomm.cnblogs.com/blogpost/12597399?page=3)
- [内网渗透测试3](http://www.zhoulingjie.com/server)
- [用Metasploit破解ftp用户名和密码](https://blog.csdn.net/qq_28409193/article/details/71565305?utm_medium=distribute.pc_relevant_download.none-task-blog-blogcommendfrombaidu-3.nonecase&depth_1-utm_source=distribute.pc_relevant_download.none-task-blog-blogcommendfrombaidu-3.nonecas)
- [ftp弱口令爆破软件](https://download.csdn.net/detail/a199141929/2829996)
- [Metasploitable 2 渗透练习：利用telnet渗透](https://www.jianshu.com/p/d10cae641bb6)
- [端口扫描器与扫描方式](http://www.wadn8.com/html/wlgz/wxwljs/10918.html) -[如何快速进行常规端口渗透](https://www.freebuf.com/column/150205.html)
- masscan快速扫描语法

```shell
   masscan --rate=1000 -p21,22,23,25,U:69,110,143,U:161,80,81,82,83,88,443,445,512,513,514,1433,1521,2082,2083,2181,2601,2604,3128,3690,4848,8088,8086,8081,8080,3306,5432,3389,5984,6379,7001,7002,8069,9200,9300,11211,10000,27017,27018,50000,50070,50030 --banners  220.163.106.148 220.163.106.149 220.163.106.151 220.163.106.143 220.163.106.156 220.163.106.152 220.163.106.154 -oL port_hacking.txt 
```

- [vnc漏洞利用及vnc漏洞利用工具](https://blog.foolbird.net/453.html)
- [远程桌面RDP漏洞扫描](https://github.com/robertdavidgraham/rdpscan)
- [端口对应服务的相应漏洞](https://www.cnblogs.com/jiangyatao/p/12193430.html)
- [常见端口漏洞信息解析](https://blog.csdn.net/zhouwei1221q/article/details/47806919?utm_source=blogxgwz5)
- [端口渗透总结](https://www.cnblogs.com/zhencool/p/11142278.html)
- [按5次shift的粘滞键利用](http://429006.com/article/technology/528.htm)
- [微软3389远程漏洞CVE-2019-0708批量检测工具](https://www.cnblogs.com/17bdw/p/11484160.html)
- [windows RDP远程代码执行_CVE-2019-0708漏洞复现](https://www.cnblogs.com/yuzly/p/11197021.html)
- [微软RDP远程代码执行漏洞（CVE-2019-0708）分析集锦](https://www.freebuf.com/vuls/205380.html)
- [RDP远程桌面执行漏洞 CVE-2019-0708](https://www.jianshu.com/p/400fc54b447f)
- [CVE0708本地搭建，渗透提权](https://www.jianshu.com/p/c7859788ff43)
- [CVE-2019-0708远程桌面漏洞验证和利用](https://www.jianshu.com/p/eff45e54da38)
- [CVE-2019-0708漏洞复现](https://blog.csdn.net/Becktick/article/details/91138712)
- [CVE-2019-0708 RDP MSF漏洞利用](https://www.cnblogs.com/Oran9e/p/11479575.html)
- [网络安全的现状与重要性](https://www.sohu.com/a/353272675_653604)