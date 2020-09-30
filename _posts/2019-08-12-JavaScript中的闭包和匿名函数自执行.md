---
layout: post # 使用的布局（不需要改）
title: JavaScript中的闭包和匿名函数自执行 # 标题
subtitle: 总结一下闭包和匿名函数自执行的一些问题 #副标题
date: 2019-08-12 # 时间
author: BY Bamboo # 作者
header-img: img/post-bg-2015.jpg #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
    - JavaScript
---

### 1.闭包

> 闭包就是能够读取其他函数内部变量的函数。例如在 javascript 中，只有函数内部的子函数才能读取局部变量，所以闭包可以理解成“定义在一个函数内部的函数“。在本质上，闭包是将函数内部和函数外部连接起来的桥梁。  
> 闭包通常用来创建内部变量，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作；闭包就是有权限访问另一个函数内部作用域的变量的函数。

举个栗子

```
function foo() {
    var a = 10;
    function bar() {   //这个函数叫做闭包
        console.log(a);
    }
}
```

```
var foo = function () {
    var a = 10;
    return function () {
        console.log(a);
    };

}();     //return出来的是一个函数表达式，可以在后面接小括号直接调用。
foo();   //10  利用闭包可以在函数外部进行调用。
```

闭包有什么好处呢？  
1.防止变量冲突。  
2.拥有自己独立的变量作用域，让局部变量保持一个，避免全局变量的污染。

再举一个实用的栗子

```
var foo = function () {
    var a = 10;
    a++;
    console.log(a);
};
foo();  //11
foo();  //11
foo();  //11  每调用一次函数，a都会被重新赋值为10
```

我想让 a 值累加，又是一个局部变量，该怎么做呢？对了，闭包可以做到。

```
var foo = function () {
    var a = 10;
    return function () {
        a++;
        console.log(a);
    };
}();  //此时foo是函数执行完的返回值，即return后的闭包
foo();  //11
foo();  //12
foo();  //13
```

### 2.匿名函数自执行

> 匿名函数，顾名思义指的是没有名字的函数。（没有函数名）

```
function () {   //错误写法，会报错！默认情况下，程序认为没有名字的函数是函数声明写法
    console.log(123);
}();
```

可以通过以下方法转化为函数表达式  
在 function 前面加！、+、-、~或者把函数用（）包起来都可以将函数声明转换成函数表达式，我们一般用（）把函数声明包起来。

```
(function () {
    console.log(123);
})();
```

可以配合闭包用来保存状态，下面是一道很经典的题。

```
for (var i = 0; i < 3; i++) {
    setTimeout(function () {
        console.log(i);  // 3 3 3
        //在执行到这一行时，发现匿名函数里没有i，然后向往外部作用域找，然后找到的其实是for循环执行完了的i，也就是2++，3
    }, 1000);
}
```

```
for (var i = 0; i < 3; i++) {
    (function (x) {
        setTimeout(function () {
            console.log(x);  // 0 1 2
        }, 1000);
    })(i)
    //i传给了x，并且锁在内存中，所以不会变
}
```

```
for (let i = 0; i < 3; i++) {    //let具有独立的块级作用域
    setTimeout(function () {
        console.log(i);  // 0 1 2
    }, 1000);
}
```
