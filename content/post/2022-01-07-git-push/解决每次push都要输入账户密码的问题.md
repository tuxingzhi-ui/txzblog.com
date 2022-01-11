---
title: 解决git push每次都输入账号密码的问题
author: txz
date: '2022-01-07'
slug: git-push
categories:
  - Example
tags:
  - Markdown
---
#### 解决每次都要输入账户密码的问题

1.  将本地[SSH](https://so.csdn.net/so/search?q=SSH)添加到远程github 中 

2. 若是出现以下问题

   ` fatal: Not a git repository (or any of the parent directories): .git `

    在命令行 输入` git init `然后回车就好了 

    

3.输入账户密码，在本地重新生成一个``.ssh``文件,然后打开将其拷贝到GitHub上的设置中如下图：

​	[![1.png](https://i.postimg.cc/j5vfq8sJ/1.png)](https://postimg.cc/R66hXLJM)

​	[![2.png](https://i.postimg.cc/RZ4Lmbx4/2.png)](https://postimg.cc/8jX6B4C0)

​	[![3.png](https://i.postimg.cc/jScQSQRN/3.png)](https://postimg.cc/JsyBTXD4)

#### 解决啦！！！

