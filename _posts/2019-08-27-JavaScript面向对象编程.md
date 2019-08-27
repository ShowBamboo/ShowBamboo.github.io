---
layout:     post                    # 使用的布局（不需要改）
title:      JavaScript面向对象编程              # 标题 
subtitle:   总结一下JS面向对象的知识点    #副标题
date:       2019-08-27            # 时间
author:     BY Bamboo                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - JavaScript
---


数据类型 : 字符串，数字，布尔值 （基本类型）  
          对象、数组、函数（复合类型）  
          
赋值操作  
基本类型 : 只是把值进行赋值操作（传值）。  
复合类型 :把对象的地址进行赋值操作（传址）。  

数组的拷贝  
```
    var a = [['a','b'],2,3];  
    var b = a.concat();  //自带的concat和slice默认是浅拷贝
    var b = a.slice();
```
针对对象的时候： 常见的浅拷贝:3种  深拷贝:2种  
浅拷贝 : copy() -> for in 、  Object.assign()、 ...展开运算符  
```
    function copy(obj){   //浅拷贝
        var result = {};
        for(var attr in obj){
            result[attr] = obj[attr];
        }
        return result;
    }
```
深拷贝 : deepcopy() -> for in + 递归 、 JSON.parse() + JSON.stringify()  
```
        function isArray(arg) { //判断该对象是否为数组
            return Object.prototype.toString.call(arg) === '[object Array]';
        }

        function deepCopy(obj) { //深拷贝
            var result;
            if (isArray(obj)) {
                result = [];
            } else {
                result = {};
            }
            for (var attr in obj) {
                if (typeof obj[attr] == 'object') {
                    result[attr] = arguments.callee(obj[attr]);
                } else {
                    result[attr] = obj[attr];
                }
            }
            return result;
        }
```
字符串、数字、布尔值，不是对象，不能添加属性和方法。  

包装对象：基本类型都会有一个对应的包装对象（ String , Number , Boolean ），包装对象可以把自己的属性和方法给基本类型进行使用，然后包装对象消失。  

constructor : 是一个属性， 作用是返回对应的构造函数的 ，是自定义构造函数时候，唯一一个默认的自带属性。  

instanceof : 左边是对象，右边是构造函数。对象是否在构造函数的原型链上，如果在就返回true，如果不在就返回false  
```
        var arr = [1, 2, 3];

        console.log(arr instanceof Array); //true
        console.log(arr instanceof Object); //true
        console.log(arr instanceof RegExp); //false
```
```
        function Foo() {

        }

        function Bar() {

        }
        Bar.prototype = Foo.prototype;
        var f = new Foo();
        console.log(f instanceof Foo); //true
        console.log(f instanceof Bar); //true
        console.log(f instanceof Object); //true
```
in : 左边是一个属性或方法 , 右边是一个对象 , 判断属性或方法是否属性这个对象  
```
        function Foo() {
            this.username = 'xiaoming';
        }
        Foo.prototype.gender = '男';
        Foo.prototype.showName = function () {};

        var f = new Foo();

        console.log('username' in f); // true
        console.log('age' in f); //false
        console.log('gender' in f); // true
        console.log('showName' in f); // true
        console.log('toString' in f); // true
        console.log('constructor' in f); // true
```
hasOwnProperty : 判断是否有自身的属性，如果是对象自身的属性就返回true，但是如果是原型或原型链上的返回false  
```
        function Foo() {
            this.username = 'xiaoming';
        }
        Foo.prototype.gender = '男';
        Foo.prototype.showName = function () {};

        var f = new Foo();

        console.log(f.hasOwnProperty('username')); //true
        console.log(f.hasOwnProperty('gender')); //false
        console.log(f.hasOwnProperty('gender')); //false
        console.log(f.hasOwnProperty('toString')); //false
```
对象在运算的时候，会先调用valueOf()，如果返回对象，那么继续调用toString()  
toString() : 返回对象的字符串格式。  
valueOf() : 返回指定对象的原始值。  
```
        console.log(Object.prototype.toString({})); // '[object Object]'
        console.log(Object.prototype.toString.call([])); // '[object Array]'
        console.log(Object.prototype.toString.call('')); // '[object String]'
        console.log(Object.prototype.toString.call(null)); // '[object Null]'
        console.log(Object.prototype.toString.call(new Date)); //'[object Date]'
        console.log(Object.prototype.toString.call(new RegExp)); //'[object RegExp]'
```
拷贝继承  
属性 : 父类.call()  
方法 : 对象拷贝 ( for in ,  Object.assign(子类 , 父类) , ...(展开运算符)  )  
