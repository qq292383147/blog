---
title: Vue中import模块、JS文件、class类文件、数组对象文件、第三方、样式等方式集合
date: 2021-08-03 09:36:50
tags: vue
categories: vue
---

vue中经常需要import各种文件，比如样式、组件、方法、js文件、模块等，具体每种如何使用。

## 一、引入第三方插件

概述

第三方插件，比如echart、jquery等

引入流程

### 1、先install安装

```bash
npm  install 插件名称  --save
```


### 2、import导入

```b
import echarts from 'echarts'
```


### 3、其他配置



全局引入的需要再 `main.js` 中配置，一般每个js库官网中会有说明



## 二、引入函数方法



> 2.1 单个函数引入
> 2.1.1 JS中export函数



#### 1、js文件的写法

新建一个JS文件 `util.js`

```js
export  function  testFunciton(options){
	//执行代码，注意代码中最后一般都需要return返回值
}
```



#### 2、引入需要加花括号，支持多个导入

```js
import {testFunction} from './util';   //方法名需要加花括号
```



> 2.1.2 JS中 `export default`函数



#### 1、js文件写法

```js
export default function  testFunciton(options){
    //执行代码，注意代码中最后一般都需要return返回值
}

//ES6写法
const testFunction=(options)=>{
    let x=   ;
    return x;
}
export default testFunction;
```

#### 2、引入不需要花括号，只能一个个导入

```js
import testFunction from './util';   //方法名不需要加花括号
```




>2.2 多个函数引入



### 1、js文件中写函数



多个函数的引入只能用 `export` ，不能用 `export default`

```js
export  function  testFuncitonA(options){
    //执行代码，注意代码中最后一般都需要return返回值
}
export  function  testFuncitonB(options){
    //执行代码，注意代码中最后一般都需要return返回值
}
export  function  testFuncitonC(options){
    //执行代码，注意代码中最后一般都需要return返回值
}
```


#### 2、函数引入

```js
import {testFunctionA,testFunctionB,testFunctionC,} from './util';   //方法名需要加花括号
```

##### 2.3 成组全部引入



#### 1、引入方式

```js
import * as hydroServiceUtil from "../utils/hydroServiceUtil.js";
```


将整个模块当作单一对象进行导入，该模块所有的导出都会作为对象的属性存在。



#### 2、调用方式

全局调用

`main.js` 中先引入,然后添加 vue 属性配置：

```js
Vue.prototype.$hydroServiceUtil = hydroServiceUtil;
```


直接用  `this.$hydroServiceUtil.method`  调用就可以了



单个 vue 文件调用

直接用 `hydroServiceUtil.method` 调用



#### 三、引入数组、对象JS文件

##### 3.1 引入数组

```js
//js文件
const config=[1,2,3,4,5]   //一般这种方式的数组引入的都是一个常亮，不会变了，所以const即可
export default config;
```



##### 3.2 引入对象

```js
//js文件
const config={
    id：1,
    name:"zhangsan",
}
export default config;	//调用时候，vue中先import进去，然后名称.id即可
```





#### 四、引入class类js文件

有时候需要 `js` 文件写 `class` 类

```js
//classtest.js文件中内容
class Person{
    // 构造函数
    constructor(x,y){
        this.x = x;
        this.y = y;
    }
    todoSome(){
        alert(this.x + "的年龄是" +this.y+"岁");
    }
}
export default  Person;
```


使用时候，先在 `vue` 文件中 `import` 进来，然后直接 `new` 即可

```js
var test= new classtest('haha','33');
test.todoSome();
```



<center color="red">~end~</center>
