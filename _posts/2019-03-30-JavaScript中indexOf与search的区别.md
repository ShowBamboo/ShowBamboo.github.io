---
layout:     post                    # 使用的布局（不需要改）
title:      indexOf方法与search方法              # 标题 
subtitle:   JavaScript中indexOf与search的区别    #副标题
date:       2019-03-30              # 时间
author:     BY Bamboo                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - JavaScript
---
### 1.indexOf方法
定义和用法：
>indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。
如果要检索的字符串值没有出现，则该方法返回 -1。 
indexOf() 方法对大小写敏感！ 

语法如下：
>stringObject.indexOf(searchvalue,fromindex)

说明：
>该方法将从头到尾地检索字符串 stringObject，看它是否含有子串 searchvalue。开始检索的位置在字符串的 fromindex 处或字符串的开头（没有指定 fromindex 时）。如果找到一个 searchvalue，则返回 searchvalue 的第一次出现的位置。stringObject 中的字符位置是从 0 开始的。

实例：
```
var str = "hello world";
console.log(str.indexOf("hello")); ====>0
console.log(str.indexOf("World")); ====>-1
console.log(str.indexOf("world")); ====>6
```
---
### 2.search方法
定义和用法：
>search() 方法用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。
如果没有找到任何匹配的子串，则返回 -1。
search() 方法对大小写敏感！
要执行忽略大小写的检索，请追加标志 i。

语法如下：
>stringObject.search(regexp)

说明：
>search() 方法不执行全局匹配，它将忽略标志 g。它同时忽略 regexp 的 lastIndex 属性，并且总是从字符串的开始进行检索，这意味着它总是返回 stringObject 的第一个匹配的位置。

实例：
```
var str="hello World";
console.log(str.search(/World/)); ====>6
console.log(str.search(/world/)); ====>-1
console.log(str.search(/world/i); ====>6
```
---
### 3.indexOf与search的区别
>IndexOf()方法是用来判断一个字符串是否存在于一个更长的字符串中。从长字符串左端到右端来搜索，如果存在该子字符串就返回它所处的位置（即索引）。如果在被搜索的字符串没有找到要查找的字符串返回-1。
search()方法也是同样返回目标自字符串索引值的。indexOf()和search()有什么区别呢？为什么时候该使用它，什么时候该使用search()这个方法呢？

>首先要明确search()的参数必须是正则表达式，而indexOf()的参数只是普通字符串。indexOf()是比search()更加底层的方法。

>如果只是对一个具体字符串来查找，那么使用indexOf()的系统资源消耗更小，效率更高；如果是查找具有某些特征的字符串（比如查找以a开头，后面是数字的字符串），那么indexOf()就无能为力，必须要使用正则表达式和search()方法了。

>很多时候用indexOf()不是为了真的想知道子字符串的位置，而是想知道长字符串中没有包含这个子字符串。如果返回索引值是-1，那么说明没有：不等于-1，那么就是有。

>所以一般情况下indexOf比search更省资源。
