---
title: vueJS总结笔记
date: 2019-04-03 01:34:47
tags: vue
categories: vue
---

<center><font face="Comic Sans MS" size="10">Vue.js</font></center>

Vue是MVVM的框架(MVVM将业务与视图进行分离)

M => `Model`(数据模型)

V => `View`(视图模型，负责将数据模型转化成UI展现出来，就是DOM结构)

VM => `ViewModel`(一个同步`view`和`model`的对象)

安装vue：`npm i vue`


创建`vue`实例：作用监管我们的`html`代码

`El`属性指定`vue`实例的监管范围(设置`id`)

`data`属性将要展示的变量存起来(设置对象)
```js
var vm = new Vue({

//用data属性将要展示的变量存起来，data后面跟一个对象

data:{}

})

注意：如果超过vue实例的管制范围，这个{{}}作用就会失效

差值表达式：写法
{{}} 作用是用来渲染data中的数据的

```


合法使用方式有以下几种：

1、直接写一个变量名

2、字符串拼接

3、数值运算

4、三元运算符

5、函数




## Vue常用系统指令

### V-text（不推荐使用）



作用：使用来让这个html标签能够渲染data中的数据

```html
<!-- v-text可以将一段文本渲染到指定的元素中 -->
<v-text="msg">
```

### V-html (不安全)


```html
<v-html="rawHtml">
<!-- 差值表达式和`v-text`会将数据解释为纯文本，而非 HTML -->
<!-- 被插入的内容都会被当做 HTML,但是对于没有HTML标签的数据绑定时作用同v-text和{{}} -->
```

## v-bind 响应更新HTML特性(用于动态绑定属性)

作用：可以给html元素或者组件动态地绑定一个或多个attribute，或者一个组件prop动态绑定表达式

使用方法：在标签属性位置 v-bind：需要动态绑定的属性=”data中的变量”


### 1、img的src从imageSrc变量中取得

```html
<img v-bind:src="imageSrc" >

<!-- 简写 img  :src="imageSrc" -->
```


### 2、从classA, classB两个变量的值作为class的值

结果是：
```html
<div class="A B">classA, classB</div>        
<div v-bind:class="[classA, classB]">classA, classB</div>

<!--简写：<div :class=”[classA, classB]”>classA,classB</div> -->
```

### 3、isRed变量如果为true，则class的值为red，否则没有

```html
<div v-bind:class=”{red:isRed}”>isred</div>
```

### 4、div的class属性值一定有classA变量的值，而是否有classB和classC变量的值取决于isB和isC是否为true

```html
<div v-bind:class="[classA, { classB: isB, classC: isC }]">数组对象</div>
```

### 5、变量加常量

```html
<div v-bind:style="{ fontSize: size + 'px' }">size22</div>
```


### 6、变量加常量的另一种写法

```html
<img v-bind="{src:imageSrc+'?v=1.0'}" >
```

###7、对象数组

```html
<div v-bind:style="[styleObjectA, styleObjectB]">styleObjectA, styleObjectB</div>
```

在绑定prop时，prop必须在子组件中声明。可以用修饰符指定不同的绑定类型。

`.sync`  双向绑定

`.once`  单次绑定

`.camel`  将绑定的特性名字转换回驼峰命名。只能用于普通HTML特性的绑定，通常用于绑定用驼峰命名的SVG特性。

```html
<my-component :prop[.sync|.once|.camel]="someThing">
```

### v-for 渲染重复数据 

#### :key 属性具有 唯一性 ，不能重复，它能够唯一标识数组的每一组

将来数据中的某一项的值发生了改变，则v-for只会更新当前项对应的这个dom元素的值，而不是更新整个数据，从而提高效率

```
$index 可以获取相对应的数组索引
```

注意：以下变动不会触发视图更新

- 1. 通过索引给数组设置新值

- 2. 通过length改变数组

```
注：ECMAScript 5 无法检测到新属性添加到一个对象上或者在对象中删除。要处理这种情况，Vue.js增加了三种方法：`$add(key,value)`、`$set(key,value)`和`$delete(key)`,这些方法可以用来添加和删除属性，同时触发视图更新。
```

`v-for`指令可以用来渲染数组或者对象，在渲染数据时，数据模型中的数据变化了之后，视图会跟着变化

### 1、数组

A.在标签的属性位置写上 v-for=”item in  arr” item为形参，可以随便起名字，它表示数组中的每一项：arr 表示需要循环渲染的数组

B.在标签的属性位置写上 v-for=”(item,index) in arr” index表示数组项中的索引，名字随意取

### 2、对象

A.在标签的属性位置写上 v-for=”val in obj” var形参，可以随意取名字，它表示对象中key对应的值：obj表示需要循环的对象

B.在标签的属性位置写上 v-for=”(val, key, index) in obj” key就表示对象的键，index就表示这个键对应的索引，这个索引和数组类似，也是从0开始的


注意：

- 1、当使用数组的length属性改变数组长度时，不会触发视图的自动更新

- 2、当使用数组索引改变数组的时候，也不会触发视图更新

- 3、v--for指令在使用的时候一定要结合key属性来使用，这个属性能唯一标识数组中的每一项，请注意，key的值是一且不重复的，它能提升渲染效率

解决方式：

- 1、使用Vue.set(arr, index, newData) -->添加响应式

- 2、使用数组的splice方法


```html
<ul>

    <li v-for="item in user">{{item.name}}</li>

    <li v-for="(item, index) in user" :key="index">{{index}}.{{item.name}}</li>

    <li>---------------华丽的分割线---------------</li>

    <li v-for="value in boss">{{value}}</li>

    <li v-for="(value, key, index) in boss"> {{index}}.{{key}}:{{value}}</li>

</ul>

<script>

    var vm = new Vue({

      el: '#app',

      data: {

        user: [

          {name: 'jack'},

          {name: 'neil'},

          {name: 'rose'}

        ],

        boss: {

          name: '马云',

          age: 50,

          money: 1000000002030

        }

      }

    })

</script>
```


## v-model

双向数据绑定：数据模型的值和视图模型的值进行同步变化

1、在表单控件或者组件上创建双向绑定

2、v-model仅能在input元素中使用

书上的看法是:v-model指令用来在input、select、text、checkbox、radio等表单控件元素上创建双向数据绑定。


在v-model指令后面还可以添加多个参数（number[自动转类型为number类型]、lazy[只改在change事件上]、debounce[延迟]）


```html
<input type="text" v-model="uname" />

New vue({

Data:{

uname: '' //这个属性值和input元素的值相互一一对应，二者任何一个的改变都会联动的改变对方

}

})
```


### v-on 绑定事件监听器 

  1、作用：绑定事件 监听 ，表达式可以是一个方法的名字或一个内联语句，

  如果没有修饰符也可以省略，用在普通的html元素上时，只能监听 原生

  DOM 事件。用在自定义元素组件上时，也可以监听子组件触发的自定义事件。



```
在监听原生DOM事件时，如果只定义一个参数，DOM event为事件的唯一参数：如果在内联语句处理器中访问原生DOM事件，则可以用特殊变量$event把它传入方法。

内联语句可以访问一个$arguments属性，它是一个数组，包含了传给子组件的$emit回调的参数。
```
方法处理器：

```html
<button v-on:click=”doThis”></button>
```

内联语句：

```html
<button v-on:click=”doThat(‘hello’ , $event)”></button>
```

缩写：

```html
<button @click=”doThis”></button>
```

### 2、常用事件：
```
<!-- 方法处理器 -->
v-on:click
v-on:keydown
v-on:keyup
v-on:mousedown
v-on:mouseover
v-on:submit
```

```html
<!-- 阻止默认行为，没有表达式 -->

<form v-on:submit.prevent></form>

....
```

### 3、v-on的缩写形式：可以使用@替代 v-on:

```html
<button @click="doThis"></button>
```

### 4、按键修饰符

触发像`keydown`这样的按键事件时，可以使用按键修饰符指定按下特殊的键后才触发事件

```html
<!-- 给封装好的input组件绑定keydown事件的时候，必须加上.native修饰符 -->
```

写法：

```html
<input type="text" @keydown.(enter/char)="kd1">  当按下回车键时才触发kd1事件
```

或者：

```html
<!-- Vue.config.keyCodes.a = 65 ->

<input type="text" @keydown.a="kd1">  这样即可触发
```

###  v-on按键修饰符 

文档地址：<https://cn.vuejs.org/v2/guide/events.html#键值修饰符>

`.enter`&nbsp;&nbsp;&nbsp;`.tab`&nbsp;&nbsp;&nbsp;`.delete`&nbsp;(捕获 “删除” 和 “退格” 键)&nbsp;&nbsp;`.esc`

`.space`&nbsp;&nbsp;&nbsp;`.up`&nbsp;&nbsp;&nbsp;`.down`&nbsp;&nbsp;&nbsp;`.left`&nbsp;&nbsp;&nbsp;`.right`

可以自定义按键别名：

在vue.2.0版本中扩展一个f1的按键修饰符写法：

Vue.config.keyCodes.`f1` = 112

```html
<!-- 使用 -->
<button @keyup.f1="someFunc"></button>
```

#### 总结：

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/1.png) 


### V-if 是否渲染 

>1、作用：根据表达式的值的真假条件来决定是否渲染元素，如果条件为false不渲染（达到隐藏元素的目的），为true则渲染。在切换时元素及它的数据绑定被销毁并重建
>2、v-if指令可以完全根据表达式的值在DOM中生成或移除一个元素。如果v-if表达式赋值为false，那么对应的元素就会从DOM中移除;否则，对应元素的一个克隆将被重新插入DOM中。
>3、通常我们使用写法居多：

```html
<h1 v-if="isShow">Yes</h1>
<!-- 也可以用 v-else 添加一个 “else” 块：-->

<h1 v-if="isShow">Yes</h1>

<h1 v-else>No</h1>

<!-- Handlebars 模板 -->

{{#if isShow}}

<h1>Yes</h1>

{{/if}}
```

注意：v-else 元素必须紧跟在 v-if 元素否则它不能被识别。

```js
new Vue({

data:{

  isShow:true

 }

});
```

### v-show 显示或者隐藏 

1、根据表达式的真假值，切换元素的 display CSS 属性，如果为false，则在元素上添加 display:none来隐藏元素，否则移除display:none实现显示元素 

```html
<h1 v-show="isShow"  >Yes</h1> 
```

### v-if和v-show的总结： 

`v-if`和`v-show` 都能够实现对一个元素的隐藏和显示操作,但是`v-if`是将这个元素添加或者移除到dom  中，而`v-show`是在这个元素上添加 style="display:none"和移除它来控制元素的显示和隐藏的

```
注：v-show不支持<template>语法. 
```

`v-if`与`v-show`之间的关系及不同：

`v-if`中的模板可能包括数据绑定或子组件。

`v-if`是真实的条件渲染，因为它会确保条件块在切换时合适地销毁与重建条件块内的事件监听器和子组件。

`v-if`初始渲染时条件为假，则什么也不做，在条件第一次变为真时才开始局部编译（编译会被缓存起来）

`v-show`元素始终被编译并保留，只是简单地基于css切换。


总结：

`v-if`有更高的切换消耗，而`v-show`有更高的初始渲染消耗。因此，如果需要频繁切换，则使用v-show较好，如果在运行时条件不大可能改变，则使用`v-if`较好。


## v-cloak&nbsp;&nbsp;隐藏未编译 

`v-cloak`指令保持在元素上直到关联实例结束编译后自动移除，`v-cloak`和`CSS`规则如[v-cloak] { `display`: none } 一起用时，这个指令可以隐藏未编译的`Mustache`标签直到实例准备完毕。

```html
<!-- 通常用来防止<font color="#FF34B3">{{}}</font>表达式闪烁问题 -->

<!-- 在span上加上 v-cloak和css样式控制以后，浏览器在加载的时候会先把span隐藏起来，知道 Vue实例化完毕以后，才会将v-cloak从span上移除，那么css就会失去作用而将span中的内容呈现给用户 -->
<span v-cloak>{{msg}}</span>    

new Vue({

 data:{

  msg:'hello ivan'

 }

})
```

### 用自己的电脑做服务器&nbsp;&nbsp;json-server 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/2.png) 

```shell
 npm i json-server -g 
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/3.png) 

```shell
 json-server --watch db.json 
```


![img](https://qq292383147.github.io/pictureLibrary/picture/vue/4.png) 

```shell
 json-server --watch db.json 
```

`ref` 获取`dom`对象或者组件对象

作用：定义一个`dom`引用（在标签属性位置写上ref="自己定义名字"）

```
dom获取：this.$refs.自己定义的名字

ref的作用类似于document.getElementByID,在vue中想要获取一个dom对象或者组件对象，则只需要 在此元素上添加一个ref="自定义名称",再使用 this.$refs.自定义名称即可获取
```

通过ref获取到的dom的`validate`方法实现js校验。这个方法是内部封装好的，直接调用即可。该方法中传递一个函数，该函数有一个布尔值作为参数，为true表示校验通过，为false表示失败

```js
this.$refs[refName].validate(isPass => {
```

## 自定义指令 

创建：Vue.directive( '指令名字' , `配置对象`)  全局自定义指令

它接收两个参数：指令ID与定义对象。也可以用组件的directives选项注册一个全局自定义指令。

指令名字：推荐使用全小写

配置对象：inserted函数

>1、el参数：指的是使用自定义指令的dom元素
>2、Binding参数：一个记录自定义指令信息的对象  vaule属性

<font color="red">使用：v-指令名字</font>

```
利用Vue.directive('指令id',{inserted:function(el,binding){}})
```

指令`id`可由程序员自行定义，注意和系统指令名称有所区别


```html
<!-- focus,在某个元素上具体使用的时候请在 指令id前面再加上 v- -->
<input v-focus>
```

第二个参数是一个对象，其中inserted是一个函数，表示 "被绑定元素插入父节点时调用"

`inserted`的参数：

`el`参数：表示使用此自定义指令的dom对象

`binding`参数：一个对象，包含以下属性;

`name`：指令名，不包括 v- 前缀;

`value`：指令的绑定值，例如：`v-focus`="colorvalue", value 的值是`colorvalue`这个变量的值，colorvalue定义在data(){}中

expression：绑定值的字符串形式。例如 `v-focus`="colorvalue" ，`expression`的值是 "colorvalue"

<h2>过滤器filters</h2> 

作用：过滤数据，将数据格式从一种转换成另外一种

创建：Vue.`filter`('过滤器名字',函数)

第一个参数为过滤器ID，作为用户自定义过滤器的唯一标识;第二个参数则为具体的过滤器函数。过滤器函数以值为参数，返回转换后的值。

1、函数的默认表示要过滤的数据
2、在函数中必须要return

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/5.png) 


<h3>1、私有过滤器</h3>

Vue2.0前定义格式

```js
new vue({
 el: '#app',
 filters: {
 '过滤器名称':function(管道符号 | 左边对象的值, 参数1, 参数2, ....) {
  return 对管道符号 | 左边参数的值做处理以后的值

  }
 }
})
```

Vue2.0调用过滤器传参写法：

```html
{{ msg | 过滤器id('参数1','参数2' ....) }}
```

<h3>2、全局过滤器</h3>

```
可以用全局方法 Vue.`filter()` 注册一个全局自定义过滤器，它接收两个参数：过滤器 `ID` 和过滤器函数。过滤器函数以值为参数，返回转换后的值

Vue2.0 使用：参数调用时用()，多个参数中间使用逗号分开 {{ msg | 过滤器名称('参数1','参数2' ....) }}
```

## 计算属性 computed

计算属性是当其依赖属性的值发生变化时，这个属性的值会自动更新，与之相关的dom部分也会同步自动更新。

定义：根据data中已有的数据，计算得到一个新的属性

优点：依赖缓存，效率高

缺点：不能使用异步

创建：函数中必须有return

注意 ====> 这个函数名可以当成一个变量来使用

```js
computed: {
  fullName: function () {
    console.log(this.firstName + this.lastName)
    return this.firstName + this.lastName

   }
  }
}
```

## 侦听器 watch

作用：用来监听data中数据的变化

优点：里面可以使用异步

缺点：效率比较低

创建：和计算属性不一样，里面不要写return

```js
watch: {

   firstName: function (val) {
     this.fullName = val + ' ' + this.lastName
   },
   lastName: function (val) {
     this.fullName = this.firstName + ' ' + val
   }
  }
```

 注意：通常情况下用computed，当需要在数据变化时执行异步或开销较大的操作时，用`watch` 

## 深度监听

 如果要监听对象，像以前那样写是不行的，必须要改成深度监听的写法 

```html
 <h2>{{fullName}}</h2>
```

```js
 data：{ 
  user：{ 
  Name：'jack' 
 }, 
 fullName: '' 
 } 
 watch: { 
 user: { 
    // handler表示对象属性变化的处理函数，它只能叫这个名字，不能改成其他的名字 
    handler(newVal) { 
      this.fullName = '欧阳' + newVal.name 
    }, 
    // deep:true表示开启深度监听 
    deep:true, 
    // immediate:true 表示监听立马执行一次 
    immediate:true 
   } 
 } 
```

`transition` 结合 `animate.css` 实现

```js
// 1. 导入animate.css
// 2. 使用
<link rel="stylesheet" href="./animate.css">
<transition enter-active-class="animated fadeInRight" leave-active-class="animated fadeOutRight"/>
<span style="display:block;width:300px;" v-if="isshow">hello 黑马</span>
</transition>
 // 利用methods中的方法去控制data中的isshow属性，实现元素的显示与隐藏
```

`transition`结合动画钩子函数实现

注意:`enter`和`leave`钩子中，当动画结束一定要调用`done()`函数，不然后续钩子函数不会被调用
2.0 在想要进行动画的元素上使用 `<transition>`标签包住 

## transition

​动画进入事件： 

`​@before-enter `

​`@enter `

`​@after-enter `

`Methods`配置 

注意：

- 1、methods中定义的方法内的this始终指向创建的Vue实例

- 2、与事件绑定的方法支持参数event即原生DOM事件的传入

- 3、方法用在普通元素上时，只能监听原生DOM事件：用在自定义元素组件上时，也可以监听子组件触发的自定义事件。

## Promise

作用：是一种 异步 解决方式，解决 回调地狱 

- 1、promise里面保存的是状态，两种情况：成功或失败

`fulfilled`：成功&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;`rejected`：失败

- 2、then()函数中访问 成功状态 的数据

- 3、catch()函数访问 失败状态 的数据


```js
Let promiseObj = new Promise(function( resolve ,  reject ) {

// 成功或失败

})

// 调用 (链式编程) 

  PromiseObj.then(function(data) {

// 成功的逻辑

})

  .catch(function(data) {

// 失败的逻辑

})
```

## Axios (要安装比如`npm i axios` 或者使用`cds`引入)

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/6.png) 

- 1、基于promise的请求库
- 2、Get请求传参

```js
methods: {

  getData: function () {

    var url = 'http://www.liulongbin.top:3005/api/getprodlist'

    axios.get(url)

      .then(res => {

        this.list = res.data.message

        console.log(this.list);

      })

      .catch(error => {

        console.log(error);

      })

  }

}
```

<h2>2、Post请求传参</h2>

```js
methods: {
  getData: function () {
    var url = 'http://www.liulongbin.top:3005/api/addproduct'
    axios.post(url, "name=hello")
      .then(res => {
        console.log(res);
      })
      .catch(error => {
        console.log(error);
      })
  }
}
```

<h3>3、Delete请求传参</h3>

暂时不说明

<h2>vue过渡&动画</h2>

可以给任何元素和组件添加进入或离开的过渡

```html
<blockquote>
  <p>条件渲染 (使用 v-if)</p>
  <p>条件展示 (使用 v-show)</p>
  <p>动态组件</p>
</blockquote>
```


作用：将需要添加过渡的元素用transition组件包裹起来，结合css或者js钩子函数就能实现该元素进入或者离开的动画效果

在`transition`这个标签中有两个属性：

```html
<blockquote>
  <p>1. enter-active-class：控制动画的进入</p>
  <p>2. leave-active-class：控制动画的离开</p>
</blockquote>
```



写法注意点：

```html
<blockquote>
  <p>1. 两个属性中均要编写 animate.css中定义好的一个类  animated</p>
  <p>2. 在两个属性中分别取animate.css中控制的动画样式即可(按需获取)</p>
</blockquote>
```





<h2>过渡动画进入</h2>

`before-enter` 过渡动画进入之前，一般在这个方法中定义目标元素的初始位置

`enter` 过渡动画进入中，在这个方法中定义目标元素的结束位置

`after-enter` 过渡动画结束后，通常在这个方法里面重置初始值

`enter-cancelled` 取消过渡动画时被调用

<h2>过渡动画离开</h2>

`​before-leave` 动画离开之前触发

`​leave` 过渡动画进入中触发

`​after-leave` 过渡动画离开结束后

`leave-cancelled` 取消过渡动画时被调用



### Vue组件的创建

vue.`component`(组件名,  配置项)方法 

 注意：`template`里面的标签只能有一个根节点 

 组件的命名可以全小写，可以大写驼峰，还可以连字符('-') 

 如果使用驼峰命令，那么在页面使用的时候，要使用连字符 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/7.png) 

 组件内部指令方法data使用 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/8.png) 

###  组件中的指令以及事件绑定 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/9.png) 


###  父子组件创建 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/10.png) 

####  父组件传值给子组件(props) 

 注意：`props`要接收父组件传递过来的数据，首先得通过`props`属性定义一个坑 

 `props`：['sonmoney'] 

 在使用子组件的位置，利用v-bind指令，给子组件内部的坑传值 
```js
 // 调用money 
 <h1>{{  money  }}</h1> 
 <son :sonmoney = "money"></son> 
 data { 
 return   { 
  money:   9999 
  } 
 } 
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/11.png) 

####  子组件传值给父组件


```js
($emit) 
data() { 
 return { 
    songfname: 'rose'
    } 
 } 
```


```js
// 1. 通过this.$emit() 方法向父亲发射事件及数据  
// $emit() 函数这里有两个参数，一个是自定义事件名称，另一个是数据 
 methods: { 

 tellFather() { 
    this.$emit('emitName', this.girlfriendName) 
    } 
 } 
```
### 2.在使用子组件的地方，通过 v-on 指令去监听子组件发射过来的事件 
```js
 template: '
 <div>我的儿子告诉我，他交往了一个女朋友叫{{songfname}}
 <son @emitName="  getName"></son>
 </div>'
 components:{ son } 
```

### 3. 通过函数的默认参数，接收了组件发射过来的数据 
```js
 methods: { 

 getName(name) { 
```
### 4.直接给父组件中的变量赋值 
```js
 this.songfname = name 
  } 
 } 
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/12.png) 

### 非父子传参 

- 1.创建事件总线eventbus,它是一个空的vue实例，它可以用来作为非父子组件通信的桥梁（与son同级） 

>(1)   let evtbus = new Vue() 

- 2.在methods方法定义函数，设置利用事件总线，发射一个自定义事件，以及数据 

```
(1)   Evtbus.$emit('emitName', this.gfName) 
```



- 3. 在daughter组件挂载到页面的时候就一直监听，通过事件总线监听，兄弟什么时候发射事件过来，没什么执行自己的逻辑 

```js
// 事件总线通过$on方法监听的事件名称，第二个参数是一个回调函数 
   evtbus.$on(  'emitName', (name) => { 
		this.saoziName = name 
	}) 
```



![img](https://qq292383147.github.io/pictureLibrary/picture/vue/13.png) 

###  利用  component  组件和is属性实现动态组件  （  tab栏切换  ） 

动态组件通过`component`组件实现，这个组件在一个is属性，`is`属性的值是谁，它就会展示哪个组件

实现如下：

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/14.png) 

### 局部自定义指令和局部过滤器( 注意：只能在组件里 )
```js
// 创建 局部 自定义指令通过directives属性创建；局部自定义指令在哪个组件创建，就只能在那个组件使用

directives: {
 myfocus: {
   inserted(el) {
     el.focus()
   }
  }
}
// 创建 局部 过滤器通过filters

filters: {

fmtTime(time) {
   let y = time.getFullYear()
   return y + '年'
   }
}
```

##  组件生命周期 

###  create 和 mounted 相关 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/15.png) 

###  update 相关 

这里我们在 chrome console里执行以下命令

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/16.png) 

 

####  destroy 相关 

有关于销毁，暂时还不是很清楚。我们在console里执行下命令对 vue实例进行销毁。销毁完成后，我们再重新改变message的值，vue不再对此动作进行响应了。但是原先生成的dom元素还存在，可以这么理解，执行了destroy操作，后续就不再受vue控制了。

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/17.png) 

## 总结 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/18.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/19.png) 


## 插槽的几种方式 

### 单个插槽 
```
除非子组件模板包含至少一个 <slot> 插口，否则父组件的内容将会被丢弃。
当子组件模板只有一个没有属性的插槽时，
父组件传入的整个内容片段将插入到插槽所在的 DOM 位置，并替换掉插槽标签本身。

最初在 <slot> 标签中的任何内容都被视为 备用内容。
备用内容在子组件的作用域内编译，并且只有在宿主元素为空，且没有要插入的内容时才显示备用内容。
```
例：
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 单个插槽</title>
<script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="example">
    <div>
  <h1>我是父组件的标题</h1>
  <my-component>
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
  </my-component>
</div>
</div>
```

```js
var childNode = {
//当没有<slot>时，父组件的其他内容不会显示，当有<slot>时，要是父组件中的内容不为空
//<slot>中的内容就不会显示
 template: `
 <div>
  <h2>我是子组件的标题</h2>
  <slot>
 //只有在没有要分发的内容时才会显示。
  </slot>
</div>
 `,
};
```

```js
// 创建根实例
new Vue({
 el: '#example',
 components: {
  'my-component': childNode
 }
})
</script>
</body>
</html>
```

## 具名插槽 
```
<slot> 元素可以用一个特殊的特性 name 来进一步配置如何分发内容。
多个插槽可以有不同的名字。具名插槽将匹配内容片段中有对应 slot 特性的元素。

仍然可以有一个匿名插槽，它是 默认插槽,
作为找不到匹配的内容片段的备用插槽。
如果没有默认插槽，这些找不到匹配的内容片段将被抛弃。
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 具名插槽</title>
<script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="example">
	<app-layout>
  <h1 slot="header">这里可能是一个页面标题</h1>
  <p>主要内容的一个段落。</p>
  <p>另一个主要段落。</p>
  <p slot="footer">这里有一些联系信息</p>
</app-layout>
</div>
```
```js
	<script>
  Vue.component('app-layout',{
	template:'<div class="container">'+
  '<header>'+
    '<slot name="header"></slot>'+
  '</header>'+
  '<main>'+
    '<slot></slot>'+
  '</main>'+
  '<footer>'+
    '<slot name="footer"></slot>'+
  '</footer>'+
'</div>'
	})

// 创建根实例
new Vue({
 el: '#example',
})
</script>
</body>
</html>
```
- 1.具名插槽首先需要给slot组件指定一个name属性，也就是给插槽取名字

  

- 2.给标签添加slot属性，slot属性的值与下面的name属性的值对应，就表示把这段内容插入到哪个坑里面

## 作用域插槽 

作用域插槽是一种特殊类型的插槽，用作一个 (能被传递数据的) 可重用模板，来代替已经渲染好的元素。

在子组件中，只需将数据传递到插槽，就像你将 prop 传递给组件一样：

```html
<div class="child">

  <slot text="hello from child"></slot>

</div>
```

```
在父级中，具有特殊特性 slot-scope 的 <template> 元素必须存在，表示它是作用域插槽的模板。

slot-scope 的值将被用作一个临时变量名，此变量接收从子组件传递过来的 prop 对象：

在 2.5.0+ ，slot-scope  能被用在任意元素或组件中而不再局限于  <template>。
```

```html
<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8">

<title>Vue 测试实例 - 作用域插槽</title>

<script src="https://cdn.bootcss.com/vue/2.2.2/vue.min.js"></script>

</head>

<body>

<div id="example">

<parent-com></parent-com>

</div>

    <script>

   Vue.component('child-com',{

        template:'' +

        '<ul>' +

        '   <slot name="child-ul" v-for="item in animal" v-bind:text="item.name"></slot>' +

        '</ul>',
```
```js
        data:function(){

            return {

                animal:[

                    {name:'大象'},

                    {name:'小狗'},

                    {name:'小猫'},

                   {name:'老虎'}

                ]

            }

        }

    });
    //父组件

    // 在父组件的模板里，使用一个Vue自带的特殊组件<template> ，

    // 并在该组件上使用scope属性，值是一个临时的变量，存着的是由子组件传过来的

    // prop对象，在下面的例子中我把他命名为props。

    //  获得由子传过来的prop对象。这时候，父组件就可以访问子组件在自定义属性上暴露的数据了。

    Vue.component('parent-com',{

        template:'' +
       '<div class="container">' +

        '<p>动物列表</p>' +

        '<child-com>' +

        '   <template scope="props" slot="child-ul">' +

        '       <li class="child-ul">{{ props.text }}</li>' +

        '   </template>' +

        '</child-com>' +

        '</div>'
    });
 
// 创建根实例

new Vue({

 el: '#example',

})

</script>

</body>

</html>

 this.msg = 'hello itcast'; 
```
 它是一个异步操作，导致之前获取到的值不能被改变更改之后的值 

解决的方法：

借助于 Vue.`nextTick(callback)`。
它的作用是等到数据更新完成之后，再去执行回调函数里面的内容
```js
this.$nextTick(() =>{

//设置操作

})

// 提示：Vue.nextTick(回调函数)  等价于 this.$nextTick(回调函数) 也是Vue.nextTick的别名
```


##  动态渲染数据 

```js
全局Vue.set()	它的别名是Vue.$set()
```



### 路由 router 

```js
  // 引入路由文件 

<script src=”./vue-router.js”><script>

 // 创建路由所需要的组件 

 // 首页组件 

 let homeCom = Vue.component('home', { 

 template:'<div>进入首页</div>  ’ 

 }) 

 // 商品分类组件 

 let productCom = Vue.component({ 

 Template:` 

<div>商品分类</div>

 ` 

 }) 

 // 通过VueRouter构造函数，常见路由实例 

 let routerObj = new VueRouter({ 

 // 给路由实例中添加路由配置 
```

 配置路由通过`routers`属性配置 

 它是一个数组，数组中放的是一个一个的路由对象， 

 路由对象中包含`name`给路由规则取名字、`path`路径 

### component匹配路径所对应的组件 

```js
 routes：[ 
 {name: 'homePage' , path:'/home', component:   homeCom  }, 
 {name:'productPage' , path:'/product', component: productCom}, 
 ] 
 }) 
 //  将路由对象注入到vue对象中，让整个vue应用程序拥有路由 
 var vm= new Vue({ 
 el:   '#app', 
 router：routerObj, 
 data: { 
 } 
 }) 

<div id="app">
 // 要在页面上做路由跳转，需要使用router-link组件。 
```


 这个组件将来会被渲染成a标签， 

 他有一个to属性，表示需要跳转到的路径， 

 这个路径必须和下面定义路由规则的path一一对应 
```html
 <ul> 

 <li><router-link to=  ”  /home  ”  >首页</router-link></li> 

 <li><router-link to=  ”  /product  ”  >商品</router-link></li> 

 </ul> 

 </div> 
```
如果想获取路由参数（定义、获取）：
```js
// 通过 冒号 + 参数名 --> 定义一个路由参数

{name: ‘productPage’, path: ’/product/:pid’, component: productCom}

// 在页面中要获取路由参数，通过$route.params.参数名 来获取

// $route表示当前页面的路由对象

mounted () {

console.log(this.$route.params.pid);

}
```

#### 如果实现通过id获取的参数动态取json数据如何实现？ 

```
注意：当使用路由参数时，原来的组件实例会被费用。
因为两个路由都渲染同个组件比起销毁再创建，复用则显得更加高效。
不过，这也意味着组件的生命周期钩子不会被调用。
则我们需要复用组件时，想对路由参数的变化作出响应的话，可以用watch(监测变化) $route 对象  
```



- 1.监听路由参数的变化 

- 2.'$route'(to, from): to 表示将要去(go)的路由对象，from表示从哪个路由对象离开 
```js
 watch: { 
  '$route': { 
  let pid =   to  .params.pid; 
  axios.get('http://localhost:3000/list/' + id) 
    .then(res => { 
     this.list = res.data.products 
    }) 
  }, 
   immediate: true 
} 
```

### 编程式导航及路由嵌套 
```js
 <script>

    let cookBookCom = Vue.component('book', {

      template: `

          <div class="book">番茄炒鸡蛋，鸡蛋炒番茄，番茄鸡蛋汤。。。。。。。</div>

      `

    })

    let homeCom = Vue.component('home', {

      template: '<div>欢迎来到商城首页</div>'

    })

    let productCom = Vue.component('product', {

      // 1.3 定义子路由的坑

      template: `

            <div class="product">

              <p>这是商品分类,该分类的id是：{{$route.params.pid}}</p>

              <ul>

                <li v-for="(item, index) in list" :key="index">{{item}}</li>

              </ul>

              <button @click="viewCookbook">查看菜谱</button>

              <router-view></router-view>

            </div>

      `,

      methods: {

        viewCookbook() {

         // 编程式导航，也就是通过js代码跳转 this.$router.push()

          // $router表示的是整个的路由对象

          // console.log(this.$router);

 

          // 跳转方式有以下几种

          // this.$router.push('/home')

          // this.$router.push({name: 'homePage'})

          // this.$router.push({path: '/home'})

 

          // 1.2 

          this.$router.push({name: 'bookPage'})

          // this.$router.push('/product/' + this.$route.params.pid + '/book')

        }

      },

      data() {
        return {
          list: []
        }
      },
      watch: {
        '$route': {
          handler(to, from) {

            let pid = to.params.pid;

            axios.get('http://localhost:3000/list/' + pid)
              .then(res => {
                console.log(res.data);
                this.list = res.data.products
              })
          },
          immediate: true
        }
      },
    })
    let routerObj = new VueRouter({
      routes: [{
          name: 'homePage',
          path: '/home',
          component: homeCom
        },
        {
          name: 'productPage',
          path: '/product/:pid',
         component: productCom,
          // 1.1 子路由（嵌套路由）通过children属性实现,children是一个数组，数组里面放的也是路由对象，里面也是path/name/component这些属性，注意一点，就是path前面不能加 /
          children: [
            {name: 'bookPage', path: 'book', component: cookBookCom}
          ]
        },
      ]
    })
    var vm = new Vue({
      el: '#app',
      router: routerObj,
		data: {
      }
    })
  </script>
```


 通过传入`to` 属性指定链接 

 `router-link` 默认会被渲染成一个`<a>`标签 
```html
<router-link to="/foo"></router-link>

<!-- 路由出口 -->

<!-- 路由匹配到的组件将渲染在这里 -->

<router-view></router-view>
```

```js
// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

// 1. 定义 (路由) 组件。

// 可以从其他文件 import 进来

const = { template: '<div>foo</div>' }

const = { template: '<div>bar</div>' }

// 2. 定义路由

// 每个路由应该映射一个组件。 其中"component" 可以是

// 通过 Vue.extend() 创建的组件构造器，

// 或者，只是一个组件配置对象。

// 我们晚点再讨论嵌套路由。

const r = [

{ path: '/foo', component: Foo },

{ path: '/bar', component: Bar }]

// 3. 创建 router 实例，然后传 `routes` 配置

// 你还可以传别的配置参数, 不过先这么简单着吧。

const router = new VueRouter({

// (缩写) 相当于 routes: routes})

// 4. 创建和挂载根实例。

// 记得要通过 router 配置参数注入路由，

// 从而让整个应用都有路由功能

const app = new Vue({

  router}).$mount('#app')

// 现在，应用已经启动了！

通过注入路由器，我们可以在任何组件内通过 this.$router 访问路由器，也可以通过 this.$route 访问当前路由：

// Home.vueexport default {

  computed: {

    username () {

      // 我们很快就会看到 `params` 是什么

      return this.$route.params.username

    }

  },

  methods: {

goBack () {

window.history.length > 1?this.$router.go(-1): this.$router.push('/')

    }

  }}
```



# 路由动态传参 query和params的区别

/data/:id这个路由匹配/data/1,/data/2这里的 id 叫 params
 /data?id=1 /data?id=2 这里的 id 叫 query

当你使用params方法传参的时候，要在路由后面加参数名，并且传参的时候，参数名要跟路由后面设置的参数名对应。使用query方法，就没有这种限制，直接在跳转里面用就可以。
 这句话怎么理解呢？看下边：
 如果你要使用params传参，那么你的路由页面index.js必须带上参数，如下

```csharp
{
   path: '/detail/:id/',
   name: "detail",
   component: detail//这个details是传进来的组件名称
 }

使用： 
方法1：<router-link :to="{ name: 'details', params: { id: 123 }}">点击按钮</router-link>
方法2：this.$router.push({name:'details',params:{id:123}})
页面url显示结果是：http://localhost:8081/#/details/123
```

如果你要使用query传参，那么你的路由页面index.js必须带上参数，如下

```csharp
{
   path: '/detail',//这里不需要参入参数，参见上面的params写法
   name: "detail",
   component: detail//这个details是传进来的组件名称
 }

使用： 
方法1：<router-link :to="{ name: 'details', query: { id: 123 }}">点击按钮</router-link>
方法2：this.$router.push({name:'details',query:{id:123}})

方法3：<router-link :to="{ path: 'details', query: { id: 123 }}">点击按钮</router-link>
方法4：this.$router.push({path:'details',query:{id:123}})
页面url显示结果是：http://localhost:8081/#/details?id=123

```

这里看方法3,4,其实是对应方法1,2的，也就是说使用query方法，可以与path和name共用，2个都可以，但是params只能对应name。

要是想获取参数值：各自的获取方法是：
 query和params分别是：this.$route.query.id，this.$route.params.id

顺便说一些参数是多个的情况
 params传参，如果路由index.js如下：

```csharp
{
   path: '/detail/:id/:name',
   name: "detail",
   component: detail//这个details是传进来的组件名称
 }

```

那么跳转写法：this.$router.push({name:'detail',params:{id:123,name:'lisi'}})
 效果：[http://localhost:8081/#/details/123/lisi](https://link.jianshu.com?t=http%3A%2F%2Flocalhost%3A8081%2F%23%2Fdetails%2F123%2Flisi)
 query的写法参考上面。

query跟params，前者在浏览器地址栏中显示参数，后者则不显示。



编写单页面的步骤

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/20.png) 

JavaScript 

- 1、创建组件：创建单页面应用需要渲染的组件

- 2、创建路由：创建VueRouter实例

- 3、映射路由：调用VueRouter实例的map方法

- 4、启动路由：调用VueRouter实例的start方法

## HTML 

- 1、使用`v-link`指令

- 2、使用 router-view 标签

 

### 重定向 router.redirect 

应用在首次运行时右侧是一片空白，应用通常都会有一个首页，例如：Home页。
使用router.redirect方法将根路径重定向到/home路径：
```js
router.redirect({

    '/': '/home'

})

router.redirect方法用于为路由器定义全局的重定向规则，全局的重定向会在匹配当前路径之前执行。

{

 name: 'default',

 // *表示所有，意思就是如果页面访问的路径没有匹配到上面的任何一个，那剩下的所有路由规则都走下面这条规则

path: '*',

// 通过redirect属性实现重定向

redirect：{name: 'homePage'}

}
```
##  执行过程 
```
当用户点击v-link指令元素时，我们可以大致猜想一下这中间发生了什么事情：

· vue-router首先会去查找v-link指令的路由映射

· 然后根据路由映射找到匹配的组件

· 最后将组件渲染到<router-view>标签
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/21.png) 

 

## 嵌套路由 

>嵌套路由是个常见的需求，假设用户能够通过路径/home/news和/home/message访问一些内容，一个路径映射一个组件，访问这两个路径也会分别渲染两个组件。

 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/22.png) 

实现嵌套路由有两个要点：

· 在组件内部使用 router-view 标签

· 在路由器对象中给组件定义子路由

现在我们就动手实现这个需求。

组件模板：
```html
<template id="home">

    <div>

        <h1>Home</h1>

        <p>{{msg}}</p>

    </div>

    <div>

        <ul class="nav nav-tabs">

            <li>

                <a v-link="{ path: '/home/news'}">News</a>

            </li>

            <li>

                <a v-link="{ path: '/home/message'}">Messages</a>

            </li>

        </ul>

        <router-view></router-view>

    </div></template>

<template id="news">

    <ul>

        <li>News 01</li>

        <li>News 02</li>

        <li>News 03</li>

</ul>

</template>

<template id="message">
    <ul>
        <li>Message 01</li>

        <li>Message 02</li>

        <li>Message 03</li>
</ul>
</template>
```
组件构造器：

```js
var Home = Vue.extend({

    template: '#home',

    data: function() {

        return {

            msg: 'Hello, vue router!'

        }

    }

})

var News = Vue.extend({

    template: '#news'

})

var Message = Vue.extend({

    template: '#message'

})
```

路由映射：

```js
router.map({

    '/home': {

        component: Home,

        // 定义子路由

        subRoutes: {

            '/news': {

                component: News

            },

            '/message': {

                component: Message

            }

        }

    },

    '/about': {

        component: About

    }

})
```

在/home路由下定义了一个subRoutes选项，/news和/message是两条子路由，它们分别表示路径/home/news和/home/message，这两条路由分别映射组件News和Message。

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/23.png) 

 注意：这里有一个概念要区分一下，  /home/news  和  /home/message  是  /home  路由的子路由，与之对应的News和Message组件并不是Home的子组件。 

 

#  具名路径 

在有些情况下，给一条路径加上一个名字能够让我们更方便地进行路径的跳转，尤其是在路径较长的时候。

我们再追加一个组件NewsDetail，该组件在访问/home/news/detail路径时被渲染，组件模板：


    <template id="newsDetail">
    <div>
    News Detail - {{$route.params.id}} ......
    
    </div></template>

组件构造器：

```js
var NewsDetail = Vue.extend({

    template: '#newsDetail'

})
```



##  具名路由映射 
```js
router.map({

    '/home': {

        component: Home,

        subRoutes: {

            '/news': {

               name: 'news',

               component: News,

                subRoutes: {

                    'detail/:id': {

                        name: 'detail',

                        component: NewsDetail

                    }

                }


            },

            '/message': {

                component: Message

            }

        }

    },

    '/about': {

        component: About

    }

})
```
注意：我们在定义/homes/news/和home/news/detail/:id路由时，给该路由指定了name属性。
/:id是路由参数，例如：如果要查看id = '01'的News详情，那么访问路径是/home/news/detail/01。

Home组件和News组件模板：
```html
<template id="home">

    <div>

        <h1>Home</h1>

        <p>{{msg}}</p>

    </div>

    <div>

        <ul class="nav nav-tabs">

            <li>

                <a v-link="{ name: 'news'}">News</a>

            </li>

            <li>

                <a v-link="{ path: '/home/message'}">Messages</a>

            </li>
        </ul>

        <router-view></router-view>

</div>

</template>

<template id="news">

    <div>
        <ul>
            <li>

                <a v-link="{ name: 'detail', params: {id: '01'} }">News 01</a>

            </li>

            <li>

                <a v-link="{ path: '/home/news/detail/02'}">News 02</a>

            </li>

            <li>
                <a v-link="{ path: '/home/news/detail/03'}">News 03</a>
            </li>
        </ul>

        <div>
            <router-view></router-view>
        </div>
</div>
</template>

<a v-link="{ name: 'news'}">News</a>和<a v-link="{ name: 'detail', params:{id: '01'} }">News 01</a>这两行HTML代码，使用了具名路径。
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/24.png) 

##  v-link指令 

用了这么久的`v-link`指令，是该介绍一下它了。


```html
<!-- 在原生HTML中，我们用<a>标签的href属性来导航，在vue-router应用中，
我们还是使用<a>标签，不同的是，我们使用v-link属性而不是href属性。 -->
<a v-link="{ path: '/join/DDFE' }">Join DDFE</a>
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/25.png) 

具体来讲，v-link有三种用法：
```html
<!-- 字面量路径 --><a v-link="'home'">Home</a>

<!-- 效果同上 --><a v-link="{ path: 'home' }">Home</a>

<!-- 具名路径 --><a v-link="{ name: 'detail', params: {id: '01'} }">Home</a>
```
v-link 会自动设置 <a> 的 href 属性，你无需使用href来处理浏览器的调整，原因如下：

1、它在 [HTML5](http://lib.csdn.net/base/html5) `history` 模式和 `hash` 模式下的工作方式相同，所以如果你决定改变模式，或者 IE9 浏览器退化为 hash 模式时，都不需要做任何改变。
<br>
2、在 HTML5 history 模式下，v-link 会监听点击事件，防止浏览器尝试重新加载页面。
<br>
3、在 HTML5 history 模式下使用 root 选项时，不需要在 v-link 的 URL 中包含 root 路径。

##  路由对象 

```
在使用了 vue-router 的应用中，路由对象会被注入每个组件中，赋值为 this.$route ，并且当路由切换时，路由对象会被更新。
```


路由对象暴露了以下属性：

```
 $route.path 
字符串，等于当前路由对象的路径，会被解析为绝对路径，如 "/home/news" 。

 $route.params 
对象，包含路由中的动态片段和全匹配片段的 键值对 

 $route.query 
对象，包含路由中查询参数的键值对。例如，对于 /home/news/detail/01?favorite=yes ，会得到$route.query.favorite == 'yes' 。

 $route.router 
路由规则所属的 路由器 （以及其所属的 组件 ）。

 $route.matched 
数组，包含当前匹配的路径中所包含的所有片段所对应的配置 参数对象 。

 $route.name 
当前 路径的名字 ，如果没有使用具名路径，则名字为空 。
```
在页面上添加以下代码，可以显示这些路由对象的属性：
```html
<div>
    <p>当前路径：{{$route.path}}</p>
    <p>当前参数：{{$route.params | json}}</p>
    <p>路由名称：{{$route.name}}</p>
    <p>路由查询参数：{{$route.query | json}}</p>
    <p>路由匹配项：{{$route.matched | json}}</p>
</div>
<!-- $route.path, $route.params, $route.name, $route.query这几个属性很容易理解，看示例就能知道它们代表的含义。 -->
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/26.png) 
```
（由于$route.matched内容较长，所以没有将其显示在画面上）

这里我要稍微说一下$router.matched属性，它是一个包含性的匹配，它会将嵌套它的父路由都匹配出来。

例如，/home/news/detail/:id这条路径，它包含3条匹配的路由：
1、/home/news/detail/:id
2、/home/news
3、/home
<br>
另外，带有 v-link 指令的元素，如果 v-link 对应的 URL 匹配当前的路径，该元素会被添加特定的class，该class的默认名称为v-link-active。例如，当我们访问/home/news/detail/03这个URL时，根据匹配规则，会有3个链接被添加v-link-active。
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/27.png) 

##  让链接处于活跃状态 

以上画面存在两个问题：

- 1、当用户点击Home链接或About链接后，链接没有显示为选中

- 2、当用户点击News或Message链接后，链接没有显示为选中

##  设置activeClass 

第1个问题，可以通过设定v-link指令的activeClass解决。
```html
<a class="list-group-item" v-link="{ path: '/home', activeClass: 'active'}">Home</a>

<a class="list-group-item" v-link="{ path: '/about', activeClass: 'active'}">About</a>
```

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/28.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065517841-1680312207.png)

设定了v-link指令的activeClass属性后，默认的v-link-active被新的class取代。

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/29.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065518716-104060093.png)

第2个问题，为v-link指令设定activeClass是不起作用的，因为我们使用的是bootstrap的样式，需要设置a标签的父元素<li>才能让链接看起来处于选中状态，就像下面的代码所展现的：
```html
<ul class="nav nav-tabs">
    <li class="active">
        <a v-link="{ path: '/home/news'}">News</a>
    </li>
    <li>
        <a v-link="{ path: '/home/message'}">Messages</a>
    </li></ul>
```
如何实现这个效果呢？你可能会想到，为Home组件的data选项追加一个currentPath属性，然后使用以下方式绑定class。
```html
<ul class="nav nav-tabs">
    <li :class="currentPath == '/home/news' ? 'active': ''">
        <a v-link="{ path: '/home/news'}">News</a>
    </li>
    <li :class="currentPath == '/home/message' ? 'active': ''">
        <a v-link="{ path: '/home/message'}">Messages</a>
    </li></ul>
```

现在又出现了另一个问题，在什么情况下给currentPath赋值呢？

用户点击v-link的元素时，是路由的切换。
每个组件都有一个route选项，route选项有一系列钩子函数，在切换路由时会执行这些钩子函数。
其中一个钩子函数是data钩子函数，它用于加载和设置组件的数据。

```js
var Home = Vue.extend({

    template: '#home',

    data: function() {

        return {

            msg: 'Hello, vue router!',

            currentPath: ''

        }

    },
    route: {

        data: function(transition){

            transition.next({

                currentPath: transition.to.path

            })

        }

    }

})
```
该示例运行效果如下：

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/30.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065519669-735239613.png)

##  钩子函数(06) 

路由的切换过程，本质上是执行一系列路由钩子函数，钩子函数总体上分为两大类：

· 全局的钩子函数

· 组件的钩子函数

全局的钩子函数定义在全局的路由对象中，组件的钩子函数则定义在组件的route选项中。

##  全局钩子函数 

全局钩子函数有2个：

· beforeEach：在路由切换开始时调用

· afterEach：在每次路由切换成功进入激活阶段时被调用

##  组件的钩子函数 

组件的钩子函数一共6个：

· data：可以设置组件的data

· activate：激活组件

· deactivate：禁用组件

· canActivate：组件是否可以被激活

· canDeactivate：组件是否可以被禁用

· canReuse：组件是否可以被重用

##  切换对象 

每个切换钩子函数都会接受一个 transition 对象作为参数。这个切换对象包含以下函数和方法：

· transition.to 
表示将要切换到的路径的[路由对象](http://router.vuejs.org/zh-cn/route.html)。

· transition.from 
代表当前路径的路由对象。

· transition.next() 
调用此函数处理切换过程的下一步。

· transition.abort([reason]) 
调用此函数来终止或者拒绝此次切换。

· transition.redirect(path) 
取消当前切换并重定向到另一个路由。

##  钩子函数的执行顺序 

全局钩子函数和组件钩子函数加起来一共8个，为了熟练vue router的使用，有必要了解这些钩子函数的执行顺序。

为了直观地了解这些钩子函数的执行顺序，在画面上追加一个Vue实例：
```js
var well = new Vue({

    el: '.well',

    data: {

        msg: '',

       color: '#ff0000'

    },

    methods: {

        setColor: function(){

            this.color = '#' + parseInt(Math.random()*256).toString(16)

                        + parseInt(Math.random()*256).toString(16)

                        + parseInt(Math.random()*256).toString(16)

        },

        setColoredMessage: function(msg){

            this.msg +=  '<p style="color: ' + this.color + '">' + msg + '</p>'

        },

        setTitle: function(title){

            this.msg =  '<h2 style="color: #333">' + title + '</h2>'

        }
    }

})
```
well实例的HTML：
```html
<div class="well">

    {{{ msg }}}</div>
```
然后，添加一个RouteHelper函数，用于记录各个钩子函数的执行日志：
```js
function RouteHelper(name) {

    var route = {

        canReuse: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:canReuse')

            return true

        },

        canActivate: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:canActivate')

            transition.next()

        },

        activate: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:activate')

            transition.next()

        },

        canDeactivate: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:canDeactivate')

            transition.next()

        },

        deactivate: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:deactivate')

            transition.next()

        },

        data: function(transition) {

            well.setColoredMessage('执行组件' + name + '的钩子函数:data')

            transition.next()

        }

    }

    return route;

}
```
最后，将这些钩子函数应用于各个组件：
```js
var Home = Vue.extend({

    template: '#home',

    data: function() {

        return {

            msg: 'Hello, vue router!',

            path: ''
        }

    },

    route: RouteHelper('Home')

})

var News = Vue.extend({

    template: '#news',

    route: RouteHelper('News')

})

var Message = Vue.extend({

    template: '#message',

    route: RouteHelper('Message')
})

var About = Vue.extend({

    template: '#about',

    route: RouteHelper('About')
})
```
我们按照以下步骤做个小实验：

- 1. 运行应用（访问/home路径）

- 2. 访问/home/news路径

- 3. 访问/home/message路径

- 4. 访问/about路径

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/31.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065520701-1747230444.png)

##  切换控制流水线 

当用户点击了/home/news链接，然后再点击/home/message链接后，vue-router做了什么事情呢？它执行了一个切换管道

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/32.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065521701-1824249305.png)

如何做到这些呢？这个过程包含一些我们必须要做的工作：

- 1、可以重用组件Home，因为重新渲染后，组件Home依然保持不变。

- 2、需要停用并移除组件News。

- 3、启用并激活组件Message。

- 4、在执行步骤2和3之前，需要确保切换效果有效——也就是说，为保证切换中涉及的所有组件都能按照期望的那样被停用/激活。

 

##  切换的各个阶段 

我们可以把路由的切换分为三个阶段：可重用阶段，验证阶段和激活阶段。

我们以home/news切换到home/message为例来描述各个阶段。
（以下文字描述参考：<http://router.vuejs.org/zh-cn/pipeline/index.html>）

###  1. 可重用阶段 

检查当前的视图结构中是否存在可以重用的组件。这是通过对比两个新的组件树，找出共用的组件，然后检查它们的可重用性（通过 canReuse 选项）。默认情况下， 所有组件都是可重用的，除非是定制过。

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/33.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065522701-996052433.png)

###  2. 验证阶段 

检查当前的组件是否能够停用以及新组件是否可以被激活。这是通过调用路由配置阶段的canDeactivate 和canActivate 钩子函数来判断的。

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/34.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065523560-1593453726.png)

###  3.激活阶段 

一旦所有的验证钩子函数都被调用而且没有终止切换，切换就可以认定是合法的。路由器则开始禁用当前组件并启用新组件。

[![img](https://qq292383147.github.io/pictureLibrary/picture/vue/35.png)](http://images2015.cnblogs.com/blog/341820/201607/341820-20160721065524294-115652970.png)

此阶段对应钩子函数的调用顺序和验证阶段相同，其目的是在组件切换真正执行之前提供一个进行清理和准备的机会。界面的更新会等到所有受影响组件的 deactivate 和 activate 钩子函数执行之后才进行。

data 这个钩子函数会在 activate 之后被调用，或者当前组件组件可以重用时也会被调用。

 

## Webpack 

`webpack` 是一个现代 JavaScript 应用程序的模块打包器(module bundler)，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Sass，TypeScript等），并将其转换和打包为合适的格式供浏览器使用。

 

重点内容：

1、入口(entry)：指示webpack 应该使用哪个模块，来作为构建其内部依赖图的开始

2、输出(output)：告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist

3、加载器(loader)：loader 让 webpack 能够去处理那些非 JavaScript 文件，比如css，图片

4、插件(plugins)：插件可以用于执行范围更广的任务，比如打包优化和压缩

## Webpack安装

注意：先安装node环境

镜像源：
```shell
1、npm install nrm -g     // 安装nrm

2、nrm ls  			   // 查看镜像源

3、nrm use taobao(210)  // 选择淘宝镜像，也可以选择cnpm
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/36.png) 

> 注意：在`webpack` 的配置文件中，`mode：development` 模式是开发模式，不压缩文件，如果要打包项目建议使用 `mode：production` 模式

## 使用webpack

新建项目文件夹 test-webpack，运行如下命令：

`npm init -y`  查看package.json的运行框架库 

`npm i webpack -D`  安装package.json的框架库到当前项目中

`npm i webpack-cli -D`

## webpack初始化使用 

- 1、根目录下面新建src目录，在该目录下面创建自己的js文件

- 2、然后运行`npx webpack`将创建处理的js文件打包,(会生成一个dist目录，默认打包出来的文件是main.js)此时会有警告，意思是`mode`选项没有设置。`mode`模式有两种，一种是`deveopment`，一种是`production`

- 3、添加`mode`选项，运行命令 `npx webpack --mode development` 

 (这是把多个文件编译后合并成一个html能读得懂的文件，然后放在同一目录下) 

- 4、修改代码， 自动重新打包 ，运行命令`npx webpack --mode development --watch`

(跟上面一样，添加了一个监听，作用是当你修改代码的时候，会同步生成)

####  webpack配置文件 

- 1、配置 `webpack.config.js`

- 2、运行`npx webpack`


![img](https://qq292383147.github.io/pictureLibrary/picture/vue/37.png) 

####  webpack热更新 

安装 `npm i webpack-dev-server -D`

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/38.png) 

```js
// 3、index.html中修改
<script src="/dist/bundle.js"></script> 
```

- 4、运行： npx webpack-dev-server 选择进入dist目录下面

- 5、运行： npx webpack-dev-server --inline --hot --open --port 8090   --hot 热重载

- 6、配置script： "dev": "webpack-dev-server --inline --hot --open --port 8090" 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/39.png) 

- 7、运行 npm run dev 

## webpack loader 加载器

####  webpack处理css 

安装 `npm i css-loader style-loader -D` 

- 1、css-loader 用于处理后缀名为.css的文件

- 2、style-loader 用于将处理好的样式，加入到页面中的style标签中去

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/40.png) 

> 注意： 
>
> 1、test 表示匹配的文件类型，use 表示对应要调用的 loader
>
> 2、use 数组中指定 的 loader 顺序是固定的
>
> 3、多个 loader 的调用顺序是：从后往前调用 调用到 style-loader 后如果没有参数则把处理结果发送到 webpuck



####  webpack处理less和sass 

- 1、运行`npm i less less-loader -D`

运行`npm i sass-loader node-sass -D`


```js
{
    test: /\.less$/,
    use: [{
        loader: 'style-loader'
    }, {
        loader: 'css-loader'
    }, {
        loader: 'less-loader'
    }]
},
{
    test: /\.scss$/,
    use: [{
        loader: 'style-loader'
    }, {
        loader: 'css-loader'
    }, {
        loader: 'sass-loader'
    }]
}
```


##  webpack-图片&字体 

`npm i file-loader url-loader -D`

url-loader封装了file-loader

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/41.png) 

####  webpack处理html模板文件 

 `npm i html-webpack-plugin -D `

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/42.png) 

####  webpack转换es6语法 

 npm i babel-loader @babel/core @babel/preset-env -D 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/43.png) 

##  单文件组件 

###  结合webpack处理单文件组件 

####  配置webpack相关loader 

`npm i vue -S`

`npm i vue-loader vue-template-compiler -D`

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/44.png) 

####  使用vue文件创建vue组件 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/45.png) 

####  引入组件,并将组件渲染到页面 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/46.png) 

####  路由配置 

`npm install vue-router --save`

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/47.png) 

##  vue-cli 脚手架工具 

安装：

 `npm install -g @vue/cli`  下载工具

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/48.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/49.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/50.png) 

 `vue create admin`   通过上面的工具下载3.X模板

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/51.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/52.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/53.png) 

注意：在使用vue环境开发需注意代码格式

安装ElementUI的3.X模板还需要以下

`npm i axios element-ui vue-amap vue-echarts vue-quill-editor -S`

 vue 开发中使用 Element 组件快速开发
```html
<style lang="scss" scoped>

/* scoped属性的作用是将样式变为局部作用域的样式，实现方式是在css选择器后面加上一段随机生成的字符串，防止相同的类名间样式篡改 */
```

## Weex

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/54.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/55.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/56.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/57.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/58.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/59.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/60.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/61.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/62.png) 

做适配时记得安装 `npm i postcss-pxtorem -D` 

Weex基础：

a:作用：定义了指向某个页面的一个超链接

注意：
1. href属性必须是weex的vue文件编译成的js文件的链接，不能是一个类似于http://www.baidu.com这种网址

2. 写文字必须用text组件包裹

3. 不要使用click事件，因为你不能保证它和href的执行顺序

div：作用：容器组件，包裹其他组件

注意：

>1. 嵌套层级不能过深，容易引起性能问题
>2. 不支持背景图片：background-imgage
>3. 样式不支持：background：green写法
>4. 在原生设备中无法滚动

text：作用：渲染文本

注意：
```js
// 只能包含文本值，不能包含子组件
// 直接写文本首尾空格会被去掉，可以通过<font color="#FF34B3">{{}}</font>来绑定写头尾空格
// 超出显示省略号设置样式lines
// 字体图标
```
image：作用：渲染图片

注意：
>1. 不能写成img
>2.  必须指定宽高
>3. 双标签
>4. 不支持本地图片

 input   作用：接受用户输入字符
<br>
 list   作用：提供垂直列表的功能
<br>
 cell ：作用：定义列表中的子列表项
<br>
 loading \ refresh 
<br>
 通用样式 :
<br>
长度只支持px，不支持rem，em， 百分数
<br>
border不支持组合写法：border: 1 solid #ff0000;
<br>
不支持z-index，越靠后的元素，层级越高
<br>
不支持样式嵌套，只能写一层
<br>
只支持flex布局，元素默认flex属性,无需单独定义display: flex
<br>
flex默认主轴方向为column
<br>
不能通过true或者false动态添加类名，要通过函数返回才有效
<br>
 全屏显示 flex: 1
<br>
 内置模块  stream
<br>

### weex-ui 


## VueX 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/63.png) 

>state ,驱动应用的数据源；
>view ,以声明方式将  state  映射到视图；
>actions ,响应在  view  上的用户输入导致的状态变化。

Vuex 是专门为 Vue.js 设计的状态管理库,以利用 Vue.js 的细粒度数据响应机制来进行高效的状态更新。

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/64.png) 

vuex是一个专门为vue.js设计的集中式状态管理架构。状态？我把它理解为在data中的属性需要共享给其他vue组件使用的部分,就叫做状态。简单的说就是data中需要共用的属性。 
(就是一种向各个组件可以传参的方式)
<br>
每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的 状态 (state) 。Vuex 和单纯的全局对象有以下两点不同：
<br>

Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
<br>
你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地 提交 (commit) mutation 。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

```js
 // 如果在模块化构建系统中，请确保在开头调用了 Vue.use(Vuex) 

 const store = new Vuex.Store({ 

   state: { 

     count: 0 

   }, 

   mutations: { 

     increment (state) { 

       state.count++ 

     } 

   }}) 
```
现在，你可以通过 store.state 来获取状态对象，以及通过 store.commit 方法触发状态变更：

```js
 store.commit('increment') 

 console.log(store.state.count) // -> 1 
```

再次强调，我们通过提交 `mutation` 的方式，而非直接改变 `store.state.count`，是因为我们想要更明确地追踪到状态的变化。这个简单的约定能够让你的意图更加明显，这样你在阅读代码的时候能更容易地解读应用内部的状态改变。此外，这样也让我们有机会去实现一些能记录每次状态改变，保存状态快照的调试工具。有了它，我们甚至可以实现如时间穿梭般的调试体验。

由于 `store` 中的状态是响应式的，在组件中调用 store 中的状态简单到仅需要在计算属性中返回即可。触发变化也仅仅是在组件的 `methods` 中提交 `mutation`。

##  1. 准备 

用脚手架搭建一个项目 
安装vuex 
`npm install vuex –save`

新建文件夹store,并在此文件夹下新建store.js文件。项目目录,如下: 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/65.png)

### 1.main.js添加

<font color="#1c6f4b">//引入vuex文件</font>

```js
import store from './store/store.js'//注意文件路径
```

### 2.store文件夹下的store.js

<font color="#1c6f4b">//引入我们的vue和vuex。</font>

`import Vue from 'vue'`

`import Vuex from 'vuex'`

<font color="#1c6f4b">//使用我们vuex，引入之后用Vue.use进行引用</font>

Vue.use(Vuex);

##  2.开始demo 

准备工作完成后,我们只使用helloworld.vue和store.js文件 
1.在helloworld.vue文件中，直接更改
```html
    <template>

    <div>

        <h2>{{msg}}</h2>

        <hr/>

        <h3>{{$store.state.count}}</h3>

        <div>

            <button @click="$store.commit('add')">+</button>

            <button @click="$store.commit('reduce')">-</button>
        </div>

    </div>

</template>

<script>

    //引入store文件

    import store from '@/store/store.js'

    export default{
        data(){

            return{

                msg:'Hello Vuex',

            }

        },

        store

    }

</script>
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/66.png) 
2.store.js文件中添加

```js
const state = {

   count:1

}

 

const mutations={

    add(state){

        state.count+=1;

    },

    reduce(state){

        state.count-=1;

    }
}

export default new Vuex.Store({

    state,mutations

});
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/67.png) 
完成页面,点击按钮可以+1或-1 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/68.png)

##  state访问状态对象 

学习状态对象赋值给内部对象，也就是把stroe.js中的值，赋值给我们模板里data中的值。有三种赋值方式

>通过computed的计算属性直接赋值
>通过mapState的对象来赋值
>通过mapState的数组来赋值

###  1.通过computed的计算属性直接赋值 
```js
(helloword.vue)

computed:{

         count(){

             return this.$store.state.count;

         }

     },
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/69.png)

 

```
这里需要注意的是 return this.store.state.count这一句，一定要this，要不你会找不到store的.
```



### 2.通过mapState的对象来赋值
```js
import {mapState} from 'vuex';//用import引入mapState。

computed:mapState({

count:state=>state.count  //理解为传入state对象，修改state.count属性

       }),
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/70.png)

###  3.通过mapState的数组来赋值 

`computed:mapState(["count"])`

这个算是最简单的写法了，在实际项目开发当中也经常这样使用。 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/71.png)

##  Mutation修改状态 

他是同步事务. 
更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数：

前面我们已经用到过了 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/72.png) 
要唤醒一个 mutation handler，你需要以相应的 type 调用 store.commit 方法： 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/73.png)

提交载荷（Payload） 
你可以向 store.commit 传入额外的参数，即 mutation 的 载荷（payload）： 
现在store.js文件里给add方法加上一个参数n。
```js
const mutations={

    add(state,n){

        state.count+=n;

    },

    reduce(state){

        state.count-=1;

    }

}
```
在Count.vue里修改按钮的commit( )方法传递的参数，我们传递10，意思就是每次加10.
```html
<button @click="$store.commit('add',10)">+10</button>

<button @click="$store.commit('reduce')">-1</button>
```

###  模板获取Mutations方法 
```
实际开发中我们也不喜欢看到$store.commit( )这样的方法出现，我们希望跟调用模板里的方法一样调用。 
```

例如：@click=”reduce” 就和没引用vuex插件一样。 
在helloworld.vue上进行如下更改

```js
import { mapState,mapMutations } from 'vuex';

 methods:mapMutations([

        'add','reduce'

]),

<button @click="add(10)">+10</button>

<button @click="reduce">-1</button>
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/74.png) 
或者这么写,也可以
```html
<button @click="add10(10)">+10</button>

<button @click="reduce1">-1</button>
```

```js
methods:{

...mapMutations({

add10: 'add' ,// 将this.add10() 映射为 this.$store.commit('add')

reduce1:'reduce'//其实就是方法又命名了一下

})

},
```
## getters计算过滤操作 

getters从表面是获得的意思，可以把他看作在获取数据之前进行的一种再编辑,相当于对数据的一个过滤和加工。你可以把它看作store.js的计算属性。

##  getters基本用法： 

比如我们现在要对store.js文件中的count进行一个计算属性的操作，就是在它输出前，给它加上100.我们首先要在store.js里用const声明我们的getters属性。
```js
const getters = {

    count:function(state){

        return state.count +=100;

    }

}

computed:{
    ...mapState(["count"]),

    count(){

        return this.$store.getters.count;

    }

},
```

需要注意的是，你写了这个配置后，在每次count 的值发生变化的时候，都会进行加100的操作。 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/75.png)

###  用mapGetters简化模板写法 

首先用import引入我们的mapGetters

import { mapState,mapMutations,mapGetters } from 'vuex';

在computed属性中加入mapGetters

...mapGetters(["count"])

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/76.png)

##  actions异步修改状态 

actions是异步的改变state状态，而Mutations是同步改变状态 
在actions里写了两个方法addAction和reduceAction，在方法体里，我们都用commit调用了Mutations里边的方法。细心的小伙伴会发现这两个方法传递的参数也不一样。

`context`：上下文对象，这里你可以理解称`store`本身。 
{commit}：直接把commit对象传递过来，可以让方法体逻辑和代码更清晰明了。
```html
<button @click="$store.dispatch('addAction',10)">+</button>

<button @click="$store.dispatch('reduceAction')">-</button>
```

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/77.png) 
这样就能看到效果了,

###  mapActions 辅助函数 

在组件中分发 Action 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/78.png)

增加异步检验
```js
  addAction(context){

        setTimeout(() => {

            context.commit('add',10)

          }, 3000)
```

##  module模块组 

随着项目的复杂性增加，我们共享的状态越来越多，这时候我们就需要把我们状态的各种操作进行一个分组，分组后再进行按组编写。那今天我们就学习一下module：状态管理器的模块组操作。
```js
const moduleA = {
    state
}

export default new Vuex.Store({

    modules:{a:moduleA}

})

<h3>{{$store.state.a.count}}</h3>
```
或
```js
computed:{

    count(){

        return this.$store.state.a.count;

    }

},
```
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/79.png)

### methods 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/80.png)

完整版 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/81.png)

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/82.png)

另一种格式 
![img](https://qq292383147.github.io/pictureLibrary/picture/vue/83.png)

基于VueJs通用应用框架实现服务端渲染（SSR）数据  Nuxt.js 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/84.png) 

安装和配置

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/85.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/86.png) 



文件结构分析

`layouts`  // 布局目录，用于组织应用的布局组件，不可更改⭐

`pages`   // 用于组织应用的路由及视图,Nuxt.js根据该目录结构自动生成对应的路由配置，文件名不可更改⭐

`static`  // 用于存放应用的静态文件，此类文件不会被 Nuxt.js 调用 Webpack 进行构建编译处理。 服务器启动的时候，该目录下的文件会映射至应用的根路径 / 下。文件夹名不可更改。⭐

`store`       // 用于组织应用的Vuex 状态管理。文件夹名不可更改。⭐

`nuxt.config.js` // 用于组织Nuxt.js 应用的个性化配置，以便覆盖默认配置。文件名不可更改。⭐

`Nuxt.js` 依据 pages 目录结构自动生成 vue-router 模块的路由配置。

## 页面跳转

>1. 不要写成a标签，因为是重新获取一个新的页面，并不是SPA
>2. <nuxt-link to="/users"></nuxt-link>
>3. this.$router.push('/users')

## 动态路由
>在 Nuxt.js 里面定义带参数的动态路由，需要创建对应的以下划线作为前缀的 Vue 文件 或 目录。
>获取动态参数{{$route.params.id}}


## 嵌套路由

>1. 添加一个Vue文件，作为父组件
>2. 添加一个与父组件同名的文件夹来存放子视图组件
>3. 在父文件中，添加<nuxt-child></nuxt-child>组件，用于展示匹配到的子视图

## 创建layout
```
1. 去layouts文件夹下面新建一个新的layout组件，例如teachers.vue，并在这个组件中添加<nuxt />组件，这样，所有和teachers相关的页面都会有公共的layout

2. 给需要用到teachers.vue的组件添加layout属性，并指定需要使用的layout，例如：layout: 'teachers'
```

## 创建特殊layout : error

`layouts`文件夹下面新建error.vue，error是关键字

新建一个组件
<br>
在components文件夹下面新建一个Header.vue组件
<br>
引入组件，注意路径的~符号，表示根目录
<br>
layout中也能使用组件
<br>

## 样式配置

`nuxt.config.js`中设置设置全局样式文件路径

ElementUI使用
>1. 下载`npm i element-ui -S`
>2. 在plugins文件夹下面，创建ElementUI.js文件

```js
import Vue from 'vue'

import ElementUI from 'element-ui'

Vue.use(ElementUI)

在nuxt.config.js中添加配置

css: [

  'element-ui/lib/theme-chalk/index.css'

],

plugins: [

  {src: '~/plugins/ElementUI', ssr: true }

],

build: {

  vendor: ['element-ui']

}
```

## 异步数据

`Nuxt.js` 扩展了 Vue.js，增加了一个叫 asyncData 的方法，使得我们可以在设置组件的数据之前能异步获取或处理数据。asyncData方法会在组件（限于页面组件）每次加载之前被调用。它可以在服务端或路由更新之前被调用。所以需要注意这个函数中不能使用`this`

<font color="red">注意：常规写法如果在created钩子中写异步，是在客户端渲染的而不是在服务端</font>

使用方法：asyncData(context, callback) {callback(null, data)}

context.route.params.xxx获取参数

callback(new Error(), data)渲染出错的页面

<font color="red">注意：这个方法在服务器端执行和在客户端执行的区别</font>

## axios的使用


安装`npm install --save axios`

```js
import axios from 'axios'

asyncData(context, callback) {

  axios.get('http://localhost:3301/in_theaters')

   .then(res => {

      console.log(res);

      callback(null, {list: res.data})

    })

}
```

为防止重复打包，在`nuxt.config.js`中配置 

```js
module.exports = {

  build: {

    vendor: ['axios']

  }

}

```



## 解决跨域问题

### 方法1：后台更改 header

```js
header('Access-Control-Allow-Origin:*');//允许所有来源访问 
header('Access-Control-Allow-Method:POST,GET');//允许访问的方式 　　
```



### 方法2：使用 JQuery 提供的 jsonp

```js
methods: { 
  getData () { 
    var self = this 
    $.ajax({ 
      url: 'http://f.apiplus.cn/bj11x5.json', 
      type: 'GET', 
      dataType: 'JSONP', 
      success: function (res) { 
        self.data = res.data.slice(0, 3) 
        self.opencode = res.data[0].opencode.split(',') 
      } 
    }) 
  } 
}
```

### 方法3：使用 http-proxy-middleware  代理解决（项目使用vue-cli脚手架搭建）

例如请求的url:“http://f.apiplus.cn/bj11x5.json”

1、打开config/index.js,在proxyTable中添写如下代码：

```js
proxyTable: { 
  '/api': {  //使用"/api"来代替"http://f.apiplus.c" 
    target: 'http://f.apiplus.cn', //源地址 
    changeOrigin: true, //改变源 
    pathRewrite: { 
      '^/api': 'http://f.apiplus.cn' //路径重写 
      } 
  } 
}
```

2、使用 `axios` 请求数据时直接使用“/api”：

```js
getData () { 
 axios.get('/api/bj11x5.json', function (res) { 
   console.log(res) 
 })
```

通过这中方法去解决跨域，打包部署时还按这种方法会出问题。解决方法如下：

```js
let serverUrl = '/api/'  //本地调试时 
// let serverUrl = 'http://f.apiplus.cn/'  //打包部署上线时 
export default { 
  dataUrl: serverUrl + 'bj11x5.json' 
}
```

附：

方法二引入jq

1.下载依赖

```
cnpm install jquery --save-dev
```

2.在 webpack.base.conf.js 文件中加入

```js
plugins: [
    new webpack.ProvidePlugin({
        $: "jquery",
        jQuery: "jquery"
    })
 ],
// 还有一种方法
    module.exports = {
    devServer: {
		host: 'localhost',
         port: 8808,
    	 proxy: {
             '/api': {
                 target: 'http://localhost:3000', // 要跨域的域名
                 changeOrigin: true,  // 是否开启跨域
             }，
             // 如果不是api路径为接口的话，可以多定义几个
             '/get': {
            	target: 'http://localhost:3000',
             	changeOrigin: true,
         	}
         }
    }
}
```

3.在需要的 temple 里引入也可以在 main.js 里全局引入

```js
import $ from 'jquery'
```

 

eg：

```html
<template>
  <div class="source">
      source{{data}}
  </div>
</template>

<script>
import $ from 'jquery'
  export default({
    name:"source",
    data(){
      return{
        data:""
      }
    },
    created(){
      this.getData()
    },
    methods:{
      getData () {
        var self = this
        $.ajax({
          url: '你要请求的url',
          type: 'GET',
          dataType: 'JSONP',
          success: function (res) {
            self.data = res.result
          }
        })
      }
    }
  })
</script>
<style>
</style>
```



## VUE打包项目

```bash
npm run build:prod --report
```

