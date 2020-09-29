---
layout: post # 使用的布局（不需要改）
title: JavaScript中数组常用方法总结 # 标题
subtitle: 总结一下JS中常用的数组方法 #副标题
date: 2019-08-15 # 时间
author: BY Bamboo # 作者
header-img: img/post-bg-2015.jpg #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
    - JavaScript
---

> 数组是一种特殊类型的对象，在 JavaScript 中对数组使用 typeof 运算符会返回 "object"，数组就是一个集合。

创建数组

```
1. var arr = ['a','b','c','d'];  //出于简洁、可读性和执行速度的考虑，建议使用此方法
2. var arr = new Array('a','b','c','d');
```

多维数组

```
var arr = [
            ['a', 'b'],
            ['c', 'd']
        ];

        for (var i = 0; i < arr.length; i++) {
            for (var j = 0; j < arr[i].length; j++) {
                console.log(arr[i][j]);
            }
        }
```

#### 1.push()

往数组的最后添加新的子项，执行完的结果是当前数组的长度。

```
var arr = ['a', 'b', 'c', 'd'];
var val = arr.push('e', 'f');
console.log(arr);   // ["a", "b", "c", "d", "e", "f"]
```

#### 2.unshift()

往数组的起始添加新的子项，执行完的结果是当前数组的长度。

```
var arr = ['a', 'b', 'c', 'd'];
var val = arr.unshift('e', 'f');
console.log(arr);   // ["e", "f", "a", "b", "c", "d"]
```

#### 3.pop()

删除数组的最后一项，执行完的结果是数组被删除的那一项。

```
var arr = ['a', 'b', 'c', 'd'];
arr.pop();
console.log(arr);   // ["a", "b", "c"]
```

#### 4.shift()

删除数组的起始一项，执行完的结果是数组被删除的那一项。

```
var arr = ['a', 'b', 'c', 'd'];
arr.shift();
console.log(arr);   // ["b", "c", "d"]
```

#### 5.join()

把数组连接成一个字符串。

```
var arr = [1, 2, 3, 4];
var str = arr.join('+');
console.log( str );   // '1+2+3+4'
var str = arr.join('');
console.log( str );   // '1234'
var str = arr.join();  //不写参数，默认用逗号进行链接
console.log( str );   // '1,2,3,4'
```

#### 6.concat()

连接多个数组。

```
var a = [1, 2, 3];
var b = [4, 5, 6];
var c = a + b;
console.log(c);   //1,2,34,5,6   string
var c = a.concat(b, b);
console.log(c);   //[1, 2, 3, 4, 5, 6, 4, 5, 6]
```

#### 7.indexOf()

可返回某个指定的字符串值在字符串中首次出现的位置，对大小写敏感，如果要检索的字符串值没有出现，则该方法返回 -1。

```
var arr = ['red', 'yellow', 'blue', 'yellow'];
console.log(arr.indexOf('aaa'));   // -1
console.log(arr.indexOf('yellow'));  //1

第二个参数表示在字符串中开始检索的位置。
console.log(arr.indexOf('yellow', 2));  //3  从'blue'往后检索
```

#### 8.slice()

截取目标数组，第一个参数是起始位置，第二个参数结束位置（不包含结束位置）。

```
var arr = ['red', 'yellow', 'blue', 'yellow'];
console.log(arr.slice(1, 2));   //["yellow"]
```

#### 9.splice()

可以对数组进行添加、删除、替换。第一个参数：起始位置；第二个参数：删除的个数；第三个参数往后：要添加的元素，添加到起始位置的前面。

```
var arr = ['a', 'b', 'c', 'd', 'e'];

arr.splice(1, 2);
console.log(arr); //  ["a", "d", "e"]  删除功能

arr.splice(1, 2, 'hello', 'hi');
console.log(arr); //  ["a", "hello", "hi", "d", "e"]   替换功能

arr.splice(1, 0, 'hello', 'hi');
console.log(arr); //  ["a", "hello", "hi", "b", "c", "d", "e"]   添加功能
```

#### 10.reverse()

把整个数组进行颠倒。

```
var arr = [1, 2, 3, 4, 5];
arr.reverse(); // [5, 4, 3, 2, 1]
console.log(arr);
```

#### 11.every()

```
result会得到一个布尔值 true , false , 每一项都满足，整体返回true，有一项不满足整体就返回false

var arr = [5, 11, 2, 24, 8];
var result = arr.every(function (val, i, a) {   //当前数组元素，索引，整个数组
        return val < 23;
});
console.log(result);  //false
```

#### 12.some()

```
result会得到一个布尔值 true, false, 有一项满足条件， 整体返回true， 所有的都不满足条件整体才返回false

var arr = [5, 11, 2, 24, 8];
var result = arr.some(function (val, i, a) {
        return val < 6;
});
console.log(result);  //true
```

#### 13.filter()

把满足条件的子项筛选出来，并返回一个筛选后的数组。

```
var arr = [5, 11, 2, 24, 8];
var result = arr.filter(function (val, i, a) {
        return val < 10;
});
console.log(result);   //[5, 2, 8]
```

#### 14.map()

映射一个新的数组出来。

```
var arr = [5, 11, 2, 24, 8];
var result = arr.map(function (val, i, a) {
        return val * 2;
});
console.log(result);   //[10, 22, 4, 48, 16]
```

#### 15.reduce()

合并子项。

```
var arr = [5, 11, 2, 24, 8];
var result1 = arr.reduce(function (n1, n2) {
        return n1 - n2;
});
console.log(result1); //-40  即5-11-2-24-8

var result2 = arr.reduceRight(function (n1, n2) {
        return n1 - n2;
});
console.log(result2); //-34  即8-24-2-11-5
```

#### 总结

不能修改原数组的方法：join、concat、slice、map、filter...  
可以修改原数组的方法：push、pop、unshift、shift、splice、reverse、sort
