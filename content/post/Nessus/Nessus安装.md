---
title: Nessus的安装
author: 涂兴智
date: '2020-11-03'
slug: Nessus
categories:
  - Example
tags:
  - Markdown
---
> **Nessus的安装**  

1.点击<http://www.tenable.com/products/nessus-home>,注册并填写可用邮箱拿到激活码。  

![](http://img.wandouip.com/crawler/article/201963/d1611a85f2b1565bcf2caebc7597e3fe)

2.下载Nessus<https://www.tenable.com/downloads/nessus>,或者注册后邮件里面有下载链接🔗地址，直接点击即可。选择适合的版本进行下载安装。

![](http://img.wandouip.com/crawler/article/201963/0d33a712a863c5786a866c67534f909c)

![](http://img.wandouip.com/crawler/article/201963/1431605ce32f282157828474d4f73d39)
3.安装完成后到浏览器访问<https://localhost:8834/ >，会进入到Nessus的欢迎和配置界面，从而激活和创建管理员用户，紧接着会加载插件。期间我不小心断网了，所以没下载成功，重新来一遍，保持网络通畅，下载结束后会编译。

![](http://img.wandouip.com/crawler/article/201963/79923e79f56adc11c043c79d6156a3ce)

4.全部结束后重启，Nessus服务重启命令(Nessus服务安装后。默认是自己主动启动的。假设用户重新启动系统，获取进行其他操作时。将Nessus服务关闭的话。则再次訪问必需要先启动该服务。)
Mac下启动Nessus服务
```
主要是需要清楚命令所在路径
cd /Library/Nessus/run/sbin
sudo ./nessusd restart
```
>**初步使用**  
![Nessus（主机扫描）.png](http://ww1.sinaimg.cn/large/006HO6T7gy1gm6xco2cs1j31ww13uwko.jpg)
![](http://ww1.sinaimg.cn/large/006HO6T7gy1gm6xdi4ec1j31xi14g43n.jpg)

**从而进行漏洞扫描**
