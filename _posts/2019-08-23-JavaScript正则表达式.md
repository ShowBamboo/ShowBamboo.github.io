---
layout:     post                    # 使用的布局（不需要改）
title:      JavaScript正则表达式              # 标题 
subtitle:   总结一下正则表达式的用法    #副标题
date:       2019-08-23            # 时间
author:     BY Bamboo                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - JavaScript
---


> 正则表达式（Regular Expression，在代码中常简写为regex、regexp或RE）使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。搜索模式可用于文本搜索和文本替换。  

### 语法
    /正则表达式主体/修饰符(可选)  
    var re = /a/;  // 在两个斜线之间的字符串是不需要添加引号的  
    var re = new RegExp('a');  //有一种特殊情况下，要用new方式(正则传参的时候) 

先介绍几个有关的概念：  
### 转义字符：
    通过 \ 来实现  
    \d：数字 0-9  
    \D：非数字  
    \s：空格  
    \S：非空格  
    \w: 字符( 字母a-z 数字0-9 下划线_ )  
    \W: 非字符  
    \b: 端点 ( 起始、结束、空格 )  
    \B: 非端点  

### 修饰符：
    i：执行对大小写不敏感的匹配。  
    g：执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。  
    m：执行多行匹配。  

### 量词：
    {n, m} 匹配前一项至少n次,但是不能超过m次。  
    {n, } 匹配前一项n次,或者多次。  
    {n} 匹配前一项恰好n次。  
    + 匹配前一项1次或多次 {1,}  
    * 匹配前一项0次或多次 {0,}  
    ? 匹配前一项0次或1次 {0,1}  

### 可以操作正则的方法：
    字符串：match、search、replace、split  
    正则：test、exec  

#### 1.test() 
判断真假值，如果字符串中含有满足正则规则的文本，那么返回true，如果不满足正则的规则false。  
写法：正则.test(字符串)  
```
    var str = '72T9834';
    var re = /T9/;
    console.log(re.test(str));  //true
```
#### 2.exec()
正则去字符串中匹配，把匹配到的结果返回一个数组，如果匹配不到结果就返回null。  
写法: 正则.exec(字符串)  
和match的区别 :exec()不支持 g 修饰符不支持 g 修饰符  
```
    var str = 'hello world';
    var re = /o/g;
    console.log(re.exec(str)); //["o"] index: 4
```
#### 3.match()
正则去字符串中匹配，把匹配到的结果返回一个数组，如果匹配不到结果就返回null。  
写法: 字符串.match(正则)  
```
    var str = 'hello world';
    var re = /ell/;
    console.log( str.match(re) );   // ['ell']
```
正则默认是第一次匹配成功整个匹配就结束了，如何做到继续向字符串的后面进行匹配呢？可以通过修饰g来实现，g修饰符代表全局匹配。（从字符串的头匹配到字符串的尾）  
```
    var str = 'hd123ccv56fh4567df789';
    var re = /\d+/g;
    console.log(str.match(re));  //["123", "56", "4567", "789"]
```
#### 4.split()
使用正则表达式或者一个固定字符串分隔一个字符串。  
写法: 字符串.split(正则)  
```
    var str = '1sdf2df3ccc';
    var re = /\d/;
    console.log(str.split(re));  //["", "sdf", "df", "ccc"]
```
#### 5.search()
正则去匹配字符串，如果匹配到了，返回匹配的位置，如果没匹配到就返回 -1。  
写法: 字符串.search(正则)  
正则默认是区分大小写的 , 如何让正则不去区分大小写呢？可以用 i 修饰符来实现。  
```
    var str = 'hello world';
    var re = /W/i;
    console.log(str.search(re));   //6
```
#### 6.replace()
正则去匹配字符串，把匹配到的结果替换成指定的新字符。  
写法: 字符串.replace(正则 , 新的字符)  
```
    var str = 'abacad';
    var re = /a/g;
    str = str.replace(re, '*');
    console.log(str);  //  *b*c*d
```
字符范围: | (或的意思)  
```
    var str = 'abacadb';
    var re = /a|b/g;
    str = str.replace(re, '*');
    console.log(str);  //  ***c*d*
```
第二个参数，可以是字符串，也可以是一个回调函数。回调函数的第一个参数：就是当前匹配到的结果，以此类推。  

匹配子项: 正则中通过()可以实现子项的操作。  
```
    var str = 'hello world';
    var re = /(el)(lo)/;

    str.replace(re, function ($0, $1, $2) {
        console.log($0, $1, $2);
        return '*';
    }); //  ello el lo
```
匹配重复的子项：\1  \2  \3 ....  
```
    var str = 'aa11ccqw';
    var re = /([a-z0-9])\1/g;
    console.log(str.match(re));  //["aa", "11", "cc"]
```
字符范围: [ ] 选择指定的一个范围，并且都是或的关系。  
```
    var str = 'abc';
    var re = /a[bde]c/;
    var re1 = /a(b|d|e)c/;
    console.log(re.test(str));  // re和re1都是true
```
写在[ ]里的 ^ ,代表排除。注：写到中括号的第一个位置。  
```
    var str = 'awc';
    var re = /a[^bde]c/;
    console.log(re.test(str));  //true
```
### 常用正则表达式实例：
    匹配中文：/^[\u4e00-\u9fa5]$/  uniCode编码的16进制  
    匹配邮箱：/^[a-z0-9_-]+@[a-z0-9]+(\.[a-z]+){1,3}$/  
              /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/  
              /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/  
    验证用户名：/^[a-zA-Z][a-zA-Z0-9_]{4,15}$/   字母开头，允许5-16字节，允许字母数字下划线  
