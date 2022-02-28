---
title: JS 判断对象是否为空对象的几种方法
date: 2021-10-18 08:36:22
tags: JavaScript
categories: JavaScript
---



1.将 `json` 对象转化为 json 字符串，再判断该字符串是否为"{}"

```js
var data = {};

var b = (JSON.stringify(data) == "{}");

alert(b);//true
```



2.for in 循环判断

```js
var obj = {};

var b = function() {
    for(var key in obj) {
    return false;
}
 return true;
}

alert(b());//true
```



3.jquery 的 isEmptyObject 方法

此方法是 jquery 将2方法 (`for in`) 进行封装，使用时需要依赖 jquery

```js
var data = {};

var b = $.isEmptyObject(data);

alert(b);//true
```



4.Object.getOwnPropertyNames() 方法

此方法是使用 `Object` 对象的 `getOwnPropertyNames` 方法，获取到对象中的属性名，存到一个数组中，返回数组对象，我们可以通过判断数组的 `length` 来判断此对象是否为空

注意：此方法不兼容 ie8，其余浏览器没有测试

```js
var data = {};

var arr = Object.getOwnPropertyNames(data);

alert(arr.length == 0);//true
```



5.使用 ES6 的 Object.keys() 方法

与4方法类似，是ES6的新方法, 返回值也是对象中属性名组成的数组

```js
var data = {};

var arr = Object.keys(data);

alert(arr.length == 0);//true
```
