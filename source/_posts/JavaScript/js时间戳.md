---
title: js时间戳
date: 2019-03-22 00:15:19
tags: JavaScript
categories: JavaScript
---

**一：时间转时间戳：javascript获得时间戳的方法有四种，都是通过实例化时间对象 new Date() 来进一步获取当前的时间戳**

```js
var timestamp1 = Date.parse(new Date()); // 结果：1477808630000 不推荐这种办法，毫秒级别的数值被转化为000

  console.log(timestamp1);
```

```js
var timestamp2 = (new Date()).valueOf(); // 结果：1477808630404 通过`valueOf()`函数返回指定对象的原始值获得准确的时间戳值

console.log(timestamp2);
```

```js
var timestamp3 = new Date().getTime(); // 结果：1477808630404 ，通过原型方法直接获得当前时间的毫秒值，准确

console.log(timestamp3);
```

```js
var timetamp4 = Number(new Date()) ; //结果：1477808630404 ,将时间转化为一个number类型的数值，即时间戳*

console.log(timetamp4);
```

打印结果 如下：

![img](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/19.jpg)

 

**二，时间戳转时间**

```js
var timestamp4 = new Date(1472048779952);//直接用 new Date(时间戳) 格式转化获得当前时间

console.log(timestamp4);

console.log(tmestamp4.toLocaleDateString().replace(/\//g, "-") + " " + timestamp4.toTimeString().substr(0, 8)); //再利用拼接正则等手段转化为yyyy-MM-dd hh:mm:ss 格式
```



*效果如下：*

![img](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/20.jpg)

 

*不过这样转换在某些浏览器上会出现不理想的效果，因为toLocaleDateString()方法是因浏览器而异的，比如 IE为2016年8月24日 22:26:19 格式 搜狗为Wednesday, August 24, 2016 22:39:42*

 

*可以通过分别获取时间的年月日进行拼接，比如：*

```js
function getdate() {
            var now = new Date(),
                y = now.getFullYear(),
                m = now.getMonth() + 1,
                d = now.getDate();
            return y + "-" + (m < 10 ? "0" + m : m) + "-" + (d < 10 ? "0" + d : d) + " " + now.toTimeString().substr(0, 8);
}
```

##时间戳转时间

![](C:\Users\Administrator\Desktop\33.jpg)

```js
// 时间戳转时间
    getLocalTime(number) {
      var date = new Date(number);
      var Y = date.getFullYear() + "/";
      var M = (date.getMonth() + 1 < 10 ? "0" + (date.getMonth() + 1) : date.getMonth() + 1) + "/";
      var D = date.getDate() < 10 ? "0" + date.getDate() : date.getDate();

      var hour = date.getHours();
      var minute = date.getMinutes();
      // var second = date.getSeconds();
      return (Y + M + D +"   "+ hour + ":"+minute);
      // return (Y + M + D +"   "+ hour + ":"+minute +":"+ second);
```



## 获取时间戳的方法

![获取时间戳的方法](C:\Users\Administrator\Desktop\34.jpg)

```js
// 获取时间戳
    selectTimeStamp(time){
      // 获取某个时间格式的时间戳
      var timestamp2 = Date.parse(new Date(time));  
      // 如果想获取的时间戳为13位那就不用除1000
      timestamp2 = timestamp2 / 1000;
      return timestamp2
    }
```

