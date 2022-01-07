---
title: vue的基础学习
author: txz
date: '2022-01-07'
slug: vue
categories:
  - Example
tags:
  - Markdown
---

### vue的基础学习

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <h2>当前计数:{{counter}}</h2>
  <!--  <button v-on:click="counter++">+</button>-->
  <!--  <button v-on:click="counter&#45;&#45;">-</button>-->
```

```

<button v-on:click="add">+</button>
<button v-on:click="sub">-</button>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      counter:0
    },
    methods:{
      add:function (){
        console.log('add被执行');
        this.counter++
      },
      sub:function (){
        console.log('sub被执行');
        this.counter--
      }
    }
  })
  //拿button元素，添加监听事件(命令式) 通常使用声明是
  //methods用来定义对象中的属性方法
</script>
</body>
</html>
```


- vue里面的MVVM。MVVM是Model-View-ViewModel的简写，看视频讲解

- 创建vue实例的传入的options
+ el :
类型：string|HTMLelement  决定之后会管理哪一个dom

+ data：
类型：object|function(组件中data必须是一个函数)
作用：vue实例对应的数据

+ methods：
类型：{[key:string]:function}
作用：定义一些方法，可以在其他地方使用或者再指令中调用。

- 什么时候吧是称之为方法，什么时候称之为函数。
名称不同。方法和实例对象挂钩的。

- 什么是生命周期，事物诞生到消亡的过程
vue的生命周期：

+ new function()option（内部做了许多事情）  源码的代码，自己写的调用到function。
希望内部做一个回调（如发送一个网络请求）执行对应的函数（）callhook，挂载之后去操作

- init初始化当前的

模板相关的语法
mustache（也就是双大括号）语法


```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
```
```
<div id="app">
  <ul>
    <li v-for="item in movies">{{item}}</li>
  </ul>
</div>
```


```
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      massage: '你好啊',
      movies: ['海贼王', 'dahuaxiyou', 'shaonianpai','嘟嘟嘟']
    }
  })
</script>



</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2>{{message}}</h2>
  <h2>{{a+' '+b}}</h2>
  <h1>{{a*b}}</h1>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el:"#app",
    data:{
      message:'nihaoa',
      a:'123',
      b:'567',
    }
  })
    //解析的代码的时候就是从上往下的解析的
</script>
</body>
</html>
```




+ v-once的使用：
后面不需要跟任何指令
+ v-html

`<h2 v-html="url"></h2>`
+ V-cloak,再vue解析之前。div中有此属性。解析之后，就没有了这个属性。
settimeout
```
<style>
    [v-clock]{
        display: none;
    }
</style>
```



```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
  <img v-bind:src="imgURL" alt="">
  <a v-bind:href="aHref">打开百度</a>
</div>
```

```
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'嘟嘟嘟',
      imgURL:'https://ts1.cn.mm.bing.net/th?id=OIP-C.xsA-3qUw6cqmd8nRfxk6TQHaEK&w=164' +
              '&h=100&c=8&rs=1&qlt=90&o=6&pid=3.1&rm=2',
      aHref:'www.baidu.com'
    }
  })
</script>


</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="components-demo">
  <button-counter></button-counter>
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
```

```
</div>
// 定义一个名为 button-counter 的新组件
Vue.component('button-counter', {
data: function () {
return {
count: 0
}
},
})
//data选项必须是一个函数
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
</body>
</html>
```
