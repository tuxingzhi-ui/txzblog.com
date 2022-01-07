---
title: vue.js基础学习
author: txz
date: '2022-01-07'
slug: vue-js
categories:
  - Hugo
tags:
  - Markdown
---


### JS<u>学习</u>

- [x] 使用hbuilderx新建一个网页

[![5.png](https://i.postimg.cc/xT8LpPts/5.png)](https://postimg.cc/Tp8ypn8m)

- [x] 学习Alert

  Document.write

  Console.log
  
  
[![1.png](https://i.postimg.cc/L8VWz13B/1.png)](https://postimg.cc/sMvKz18v)

[![2.png](https://i.postimg.cc/bvJmkFJp/2.png)](https://postimg.cc/rDBGLjxP)

  ### 小知识点

  - 可以将JS代码编写到标签``onclick``属性中，当我们点击按钮的时候，JS代码才会执行。

    `` <button onclick="alert(‘内容’);">点击按钮</button>``  <button onclick="alert(‘内容’);">点击按钮</button>

  -  可以将js代码写在超链接``href``属性中，这样点击超链接时候，会执行js代码

    写在标签的属性中，属于结构与``行为耦合``，不方便维护，不推荐使用

    一般可以将代码写到``script``标签。或者编写到外部文件通过``script``进行引用

```
<script type="text/javascript">
alert("傻狍子学前端呀")
</script>
```

- *Js*中严格区分大小写

- 每一条语句以分号结尾

- *Js*中会忽略多个空格和换行，可以利用空格和换行对代码进行格式化。。

  通常使用变量保存字面量 `` var a;（var声明变量之前）``

- 标识符（所有可以自己命名的（变量名，属性名，函数名等））和其他语言一样

  不能是ES中的关键字和保留字

- / 转义字符

- JS中所有数值都是`number`类型，包括整数和浮点数。可以使用`typeof`检查变量类型`Console.log(typeof a) `

- 值类型(基本类型)：字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol。

- 可以使用字符来定义和创建 JavaScript 对象、键值对在 JavaScript 对象通常称为 对象属性。


