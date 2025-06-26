---
title: JavaScript-手写优秀的拷贝
date: 2019-11-15 20:03:15
tags: JavaScript
categories: JavaScript
---

> 面试中，大家经常会遇到，面试官让你讲述什么是深拷贝，什么是浅拷贝，如何实现深拷贝，如何实现浅拷贝。这都是一下面试中经常遇到的问题。我们如果不经能说出，还能写出，那你就很叼了。

## 一、什么是浅拷贝？

创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是引用类型的指针。如果原对象改变了这个指针，拷贝对象也会受影响。

将 B 对象拷贝到 A 对象中，但不包括 B 里面的子对象。浅拷贝只复制一层对象的属性，并不包括对象里面的为引用类型的数据。 

![90](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/90.jpg)

## 二、如何实现浅拷贝

### 2.1 Object.assign();

Object.assign();在很多的文章中，有提及到Object.assign()是一个深拷贝，大家请注意一下，它是一个浅拷贝。这里稍微扯远一点，在面试中，如果让你实现一个Object.assign()；我们该怎么做了。代码如下。

- 判断浏览器是否支持Object.assign，不支持我们在Object上绑定一个。
- 目标值需不能为空，否则进行报错。避免存在值不是对象，我们手动进行一次转换。
- 循环拷贝对象，对每一个拷贝对象的属性进行拷贝。
- 返回目标值
- Object.assign属性是不可枚举的，所以设置Object.assignMy enumerable为false。

```js
// 判断是否支持assign属性
if (Object.assign == null) {
    Object.defineProperty(Object, 'assignMy', {
        value: function(target) {
            if (target == null) {
                throw new TypeError('xxxx');
            }
            var newObj = Object(target);
            for (var index = 1; index < arguments.length; index++) {
                var nextSource = arguments[index];
                if (nextSource != null) {
                    for (var source in nextSource) {
                       if(Object.prototype.hasOwnProperty.call(nextSource, source)) {
                            newObj[source] = nextSource[source];
                        }
                    }
                }
            }
            return newObj;
        },
        writable: true,
        configurable: true,
        enumerable: false
    });
}
```

![91](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/91.jpg)

### 2.2 扩展运算符(...)

![93](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/93.jpg)![92](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/92.jpg)

### 2.3 Array.prototype.slice() && Array.prototype.concat()

```js
function list() {
    return Array.prototype.slice.call(arguments);
}
var m = {a: 1, b: 2, c: { d: 3 }};
var list1 = list(1, 2, 3, m); 
m.c.d = 5;
console.log(list1);
```



![94](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/94.jpg)

## 三、什么是深拷贝

将一个对象冲内存中完全的拷贝出来，分配一个新的内存区域存放新的对象，且修改对象不会影响到原来的对象。

将 B 对象拷贝到 A 对象中，包括 B 里面的子对象。它不仅将原对象的各个属性逐个复制出去，而且将原对象各个属性所包含的对象也依次采用深复制的方法递归复制到新对象上。

![95](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/95.jpg)

## 四、如何实现深拷贝

### 4.1 Json.parse(JSON.stringify(xxxx))

- 优点：简单、已使用。
- 缺点：会忽略undefined、symbol。不能序列化函数。不能解决循环引用的问题。

### 4.2 消息通道messageChannel

```js
function clone(obj) {
    return new Promise(resolve => {
          const {port1, port2} = new MessageChannel();
          port2.onmessage = ev => resolve(ev.data);
          port1.postMessage(obj); 
    });
}
```

- 优点：能解决undefined和循环应用的问题。
- 缺点：是一个异步函数。

### 4.3 递归函数

```js
function deepClone(target) {
    function isObj(o) {
        return (typeof o === 'object' || typeof o === 'function') && o !== null;
    }
    if (isObj(target)) {
        let cloneTarget = Array.isArray(target) ? [] : {};
        for (const key in target) {
            cloneTarget[key] = deepClone(target[key]);
        }
        return cloneTarget;
    } else {
        return target;
    }
}
var target1 = {
    field1: 1,
    field2: undefined,
    field3: {
        child: 'child'
    },
    field4: [2, 4, 8],
	field5: function() {},
	field6: Symbol('field6')
};
console.time('clone');
var obj = deepClone(target1);
console.log(obj);
console.timeEnd('clone');
```

![96](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/96.jpg)

如果存在循环引用![97](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/97.jpg)

- 优点：能解决undefined、Symbol和函数的问题。
- 缺点：不能循环引用。

### 4.4优化递归函数

```js
function deepClone(target, map = new Map()) {
    function isObj(o) {
        return (typeof o === 'object' || typeof o === 'function') && o !== null;
    }
    if (isObj(target)) {
        let cloneTarget = Array.isArray(target) ? [] : {};
        if (map.get(target)) {
            return map.get(target);
        }
        map.set(target, cloneTarget);
        // 这里还可以使用while来提高性能
        for (const key in target) {
            cloneTarget[key] = deepClone(target[key], map);
        }
        return cloneTarget;
    } else {
        return target;
    }
}
var target1 = {
    field1: 1,
    field2: undefined,
    field3: {
        child: 'child'
    },
    field4: [2, 4, 8]
};
target1.target1 = target1;
console.time('clone');
var obj = deepClone(target1);
console.log(obj);
console.timeEnd('clone');
```

- 优点：能解决undefined、Symbol、函数的问题和循环引用问题。
- 缺点：存在一定的性能问题。