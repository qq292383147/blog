---
title: JS 关于问号相关问题及用法
date: 2021-10-18 08:42:59
tags: JavaScript
categories: JavaScript
---



### js问号点的作用？.和？？的用法



> 问号点 （?.）
> 问号问号 （?？）



### 问号点 （?.）

来先看一段 js

```js
const obj = {
	hh:"xxx"
}
let res = obj?.data?.list
```

这个是什么操作呢？？
这个 data 是哪里来的呢？这个list又是哪里来的呢？就算不是外面的obj这个对象里也没有data和list啊！！！经过询问大佬后得☞

```js
		let res = obj?.data?.list
<=等价=> let res = obj && obj.data && obj.data.list
```
作用就是判断这个对象（this.element）下的（businessObject）下的（value）下的（length）是否为null或者undefined，当其中一链为null或者undefined时就返回undefined，这样即使中间缺少一个属性也不会报错，双问号后面接的就是默认值。

```js
var obj ={}
console.log(obj?.a?.b ?? 233 ) //233
var obj={a:{b:1}}
console.log(obj?.a?.b??233) //1
```



### 问号问号 （??）

这个又是什么鬼操作呢？
其实我都没有运用过

再来 look一下 js

```js
console.log(1 || "xx") 			//1
console.log(0 || "xx") 			//xx
console.log(null || "xx")		//xx
console.log(undefined || "xx")  //xx
console.log(-1 || "xx") 		//-1
console.log("" || "xx") 		//xx

console.log(1 ?? "xx")			//1
console.log(0 ?? "xx") 			//0
console.log(null ?? "xx") 		//xx
console.log(undefined ?? "xx")  //xx
console.log(-1 ?? "xx") 		//-1
console.log("" ?? "xx") 		//''
```

哦哦，原来这是赋默认值哦。。。。
不过他是忽0和空字符串等错误的值