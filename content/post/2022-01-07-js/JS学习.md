---
title: JS学习
author: txz
date: '2022-01-07'
slug: js
categories: []
tags: []
---


### JS<u>学习</u>

- [x] 使用hbuilderx新建一个网页

[![5.png](https://i.postimg.cc/xT8LpPts/5.png)](https://postimg.cc/Tp8ypn8m)

- [x] 学习Alert

  Document.write

  Console.log

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


#  0. 简介

- JavaScript 对网页行为进行编程

- javascript 是脚本语言，是一种轻量级的编程语言

- JavaScript 是动态类型语言，而 Java 是静态类型语言

- JavaScript 是弱类型的，Java 属于强类型

## 1. 命名规范

- 区分大小写
- 第一个字符必须是一个字母、下划线（_）或一个美元符号（$）;其他字符可以是字母、下划线、美元符号或数字
- 不能含有空格和其他标点符号。
- 不能以关键字或保留字命名

## 2.书写规范

1. 缩进的最小单位是4个空格
2. 所有的变量应该在使用前声明
3. 命名应该由26个大小写字母(A .. Z, a .. z)，10个数字(0 .. 9)和_(下划线)组成。不要在名字里使用$(美元符号)或(反斜线符号)。

## 3. 使用

1、JavaScript 代码必须位于 < script > 与 </ script > 标签之间。

```html
<script>
  document.getElementById("demo").innerHTML = "我的第一段 JavaScript";
</script>
```

 2、JavaScript 文件放置外部脚本引用。 

```html
<script src="myScript.js"></script>
```

> 外部 JavaScript 的优势:
>
> > 1、分离了 HTML 和代码
> > 2、使 HTML 和 JavaScript 更易于阅读和维护
> > 3、已缓存的 JavaScript 文件可加速页面加载



## 4. 注释

> // 单行注释
> /* */ 多行注释 



## 5. 输出

输出

| 代码             | 详解                     |
| ---------------- | ------------------------ |
| window.alert()   | 【弹出警告框】           |
| document.write() | 【将内容写到HTML文档中】 |
| innerHTML        | 【写入到HTML中】         |
| console.log()    | 【写入到浏览器控制台】   |

> 附（PS：console有很多有意思的玩法）
> console.log('文字信息');
> console.info('提示信息');
> console.warn('警告信息');
> console.error('错误信息');

语句标识符（关键词）

| 关键词       | 详解                                                         |
| ------------ | ------------------------------------------------------------ |
| break        | 用于跳出循环。                                               |
| catch        | 语句块，在 try 语句块执行出错时执行 catch 语句块。           |
| continue     | 跳过循环中的一个迭代。                                       |
| do ... while | 执行一个语句块，在条件语句为 true 时继续执行该语句块。       |
| for          | 在条件语句为 true 时，可以将代码块执行指定的次数。           |
| for ... in   | 用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。 |
| function     | 定义一个函数                                                 |
| if ... else  | 用于基于不同的条件来执行不同的动作。                         |
| return       | 退出函数                                                     |
| switch       | 用于基于不同的条件来执行不同的动作。                         |
| throw        | 抛出（生成）错误 。                                          |
| try          | 实现错误处理，与 catch 一同使用。                            |
| var          | 声明一个变量。                                               |
| while        | 当条件语句为 true 时，执行语句块。                           |

# 1. 变量

变量是用于存储某种/某些数值的存储器。

# 2. 命名方法

### 2.1 匈牙利命名法

变量名 = 类型 + 对象描述

| 命名类型       | 命名前缀 |
| -------------- | :------: |
| array 数组     |    a     |
| boolean 布尔值 |    b     |
| float 浮点数   |    l     |
| function 函数  |    fn    |
| int 整型       |    i     |
| object 对象    |    o     |
| regular 正则   |    r     |
| string 字符串  |    s     |

>  举例： 

```js
var s_webname = 'hello world'
```

### 2.2 驼峰式命名法

 当标识符由一个或多个单词连接在一起，第一个单词的首字母小写，后面的单词首字母大写，其它字母全部小写。 

> 举例： 

```js
var webName = 'hello world'
```

### 2.3 帕斯卡命名法

与骆驼式命名法类似，不过第一个单词首字母也大写

> 举例：

```js
var WebName = 'hello world'
```

## 3.变量声明

var - 声明全局变量

let - 声明块级变量，即局部变量。(即：所声明的变量，只在let命令所在的代码块内有效。)

const - 用于声明常量，也具有块级作用域 ，也可声明块级。(const声明的变量不得改变值， 这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。不可重复声明。)

## 4.变量类型

此处不作介绍，详情可看下面数据类型的结构

## 5.变量作用域

在 JavaScript 中, 作用域是可访问变量的集合。

JavaScript 函数作用域: 作用域在函数内修改。

一个变量的作用域（scope)是程序源代码中定义这个变量的区域。

> JavaScript 变量生命周期在它声明时初始化。
>
> > 局部变量在函数执行完毕后销毁。
> > 全局变量在页面关闭后销毁。

### 5.1 全局变量

变量在函数外定义，即为全局变量。

全局变量有 全局作用域: 网页中所有脚本和函数均可使用。

### 5.2 局部变量

变量在函数内声明，变量为局部作用域。

局部变量的优先级高于同名的全局变量

局部变量在函数开始执行时创建，函数执行完后局部变量会自动销毁。



参考：[点击](https://miluluyo.github.io/home/basics/b/b_datatype.html)
