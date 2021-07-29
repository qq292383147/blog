---
title: js中对象的属性名和属性值
date: 2021-07-29 11:38:24
tags: JavaScript
categories: JavaScript
---



##### 代码

```js
Copy/**
 * 对象的属性名
 * - 对象的属性名不强制遵循标识符的命名规范，可以是任意的名字，但在开发中
 *   尽量遵循标识符的命名规范
 */
// 创建对象obj1
var obj1 = new Object();
// 添加属性name
obj1.name = "唐僧";
console.log(obj1); // {name: "唐僧"}

/**
 * 如果要使用特殊的属性名，不能采用"."的方式来操作，需要使用另一种
 * 方式：
 *    语法：对象["属性名"] = 属性值
 * 读取时也用这种方式
 * 使用"[]"去操作属性会更加的灵活，在"[]"可以直接传递一个变量，这样
 * 变量值是多少就会读取那个属性
 */
obj1["888"] = 888;
obj1["###"] = '###';
console.log(`obj1["888"] = ${obj1["888"]}, obj1['888'] = ${obj1['888']}, obj1['###'] = ${obj1['###']}`); // obj1["888"] = 888, obj1['888'] = 888, obj1['###'] = ###
var k = '888';
// 将变量k放到[]中，用来读取属性值
console.log(`当k为'888'时, obj1[k] = ${obj1[k]}`); // 当k为'888'时, obj1[k] = 888

/**
 * 对象的属性值
 * - 对象的属性值可以是任意的数据类型，甚至也可以是一个对象
 */
// 创建另一个对象obj2
var obj2 = new Object();
obj2.address = '杭州市余杭区';
obj2.city = '杭州';
// 将对象obj2赋值给对象obj1的属性
obj1.profile = obj2;
// 此时输出对象obj1
console.log(obj1); // {888: 888, name: "唐僧", profile: {address: "杭州市余杭区", city: "杭州"}, ###: "###"}

/**
 * in运算符
 * - 通过该运算符可以检查一个对象中是否存在指定的属性，如果有则返回true，否则返回false
 * 语法：
 *     "属性名" in 对象
 */
// 检查对象obj1中是否存在属性name
if ("name" in obj1) {
    console.log(`对象obj1中存在属性name`); // 对象obj1中存在属性name
} else {
    console.log(`对象obj1中不存在属性name`);
}
// 检查对象obj1中是否存在属性city
if ("city" in obj1) {
    console.log(`对象obj1中存在属性city`);
} else {
    console.log(`对象obj1中不存在属性city`); // 对象obj1中不存在属性city
}
```
