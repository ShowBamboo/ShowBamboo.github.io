---
layout:     post                    # 使用的布局（不需要改）
title:      JavaScript中的字符串比较              # 标题 
subtitle:   字符串和数字大小比较    #副标题
date:       2019-08-05              # 时间
author:     BY Bamboo                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - JavaScript
---

>哇呀呀，今天一不小心就掉进了js类型比较的坑里。如果比较的类型不同，首先会进行隐式转换，就是将两边的类型自动转成一致再对比。查阅了不少资料，今天在这总结一下。  

比较首先分为以下几种情况：  
#### 1.纯数字和纯数字比较
直接依据数学运算，没啥说的。  
#### 2.纯数字和数字型字符串比较
```
(30 > '20'); //true  
```
数字型字符串会转成纯数字再与前面的纯数字比较，即20与30相比谁大？  
#### 3.纯数字和非数字字符串比较
```
('a' > 96); //false  
```
这种情况下，js会将字符串转成数字，js转数字的方法：parseInt('a')，如果解析不到数字，则将返回一个NaN的值。parseInt() 函数可解析一个字符串，并返回一个整数。具体用法[请戳我](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)。所以'a’转换的结果永远是NaN，所以结果永远是false（即 'a' < 96  //false）。  
#### 4.数字型字符串和数字型字符串比较
```
('5' >= '12'); //true  
('250' < '30');  //true  
```
这种比较为ASCII码比较，依次取每个字符，字符转为ASCII码进行比较，ASCII码先大的即为大；因为第一个字符5比1大，3比2大，所以后面就不用考虑了。  
#### 5.字符串和字符串比较
```
('d' > 'ab') //true  
```
大小比较是依次取字符，字符转ASCII码，ASCII码先大的即为大；d的ASCII码为100，而a的ascii码为97，所以为true。  
