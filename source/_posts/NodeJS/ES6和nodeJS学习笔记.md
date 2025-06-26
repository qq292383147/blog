---
title: ES6和nodeJS学习笔记
date: 2019-04-01 00:56:13
tags: 
- ES6
- nodeJS
categories: 
- ES6
- nodeJS
type: 
- ES6
- nodeJS
---





<center><font color="#6e75e4" size="4">ES6常用的几种方式</font></center>

## 1.变量声明const和let
在ES6之前，我们都是用var关键字声明变量。无论声明在何处，都会被视为声明在函数的最顶部(不在函数内即在全局作用域的最顶部)。这就是函数变量提升例如:
```js
  function aa() {
    if(flag) {
        var test = 'hello man'
    } else {
        console.log(test)
    }
  }
```
以上的代码实际上是：
```js
  function aa() {
    var test // 变量提升，函数最顶部
    if(flag) {
        test = 'hello man'
    } else {
        //此处访问 test 值为 undefined
        console.log(test)
    }
    //此处访问 test 值为 undefined
  }
```
所以不用关心flag是否为 true or false。实际上，无论如何 test 都会被创建声明。
接下来ES6主角登场：
我们通常用 let 和 const 来声明，let 表示变量、const 表示常量。let 和 const 都是块级作用域。怎么理解这个块级作用域？

>在一个函数内部
>在一个代码块内部

说白了只要在`{}`花括号内的代码块即可以认为 `let` 和 `const` 的作用域。
看以下代码：
```js
  function aa() {
    if(flag) {
       let test = 'hello man'
    } else {
        //test 在此处访问不到
        console.log(test)
    }
  }
```
let 的作用域是在它所在当前代码块，但不会被提升到当前函数的最顶部。
再来说说 const
const 声明的变量必须提供一个值，而且会被认为是常量，意思就是它的值被设置完成后就不能再修改了。
```js    
    const name = 'lux'
    name = 'joe' // 再次赋值此时会报错
```
还有，如果 const 的是一个对象，对象所包含的值是可以被修改的。抽象一点儿说，就是对象所指向的地址不能改变，而变量成员是可以修改的。
```js
    const student = { name: 'cc' }
    // 没毛病
    student.name = 'yy'
    // 如果这样子就会报错了
    student  = { name: 'yy' }
    //说说TDZ(暂时性死区)，想必你早有耳闻。
    {
        console.log(value) // 报错
        let value = 'lala'
    }
```
我们都知道，JS引擎扫描代码时，如果发现变量声明，用 var 声明变量时会将声明提升到函数或全局作用域的顶部。但是 let 或者 const，会将声明关进一个小黑屋也是TDZ(暂时性死区)，只有执行到变量声明这句语句时，变量才会从小黑屋被放出来，才能安全使用这个变量。
哦了，说一道面试题

```js
    var funcs = []
    for (var i = 0; i < 10; i++) {
        funcs.push(function() { console.log(i) })
    }
    funcs.forEach(function(func) {
        func()
    })
```
这样的面试题是大家很常见，很多同学一看就知道输出十次10
但是如果我们想依次输出0到9呢？
有两种解决方法，直接看一下代码：
```js
    // ES5知识，我们可以利用“立即调用函数”解决这个问题
    var funcs = []
    for (var i = 0; i < 10; i++) {
        funcs.push(
          (function(value) {
            return function() {
                console.log(value)
            }
        })(i)
      )
    }
    funcs.forEach(function(func) {
        func()
    })
  // 再来看看es6怎么处理的
    const funcs = []
    for (let i = 0; i < 10; i++) {
        funcs.push(function() {
            console.log(i)
        })
    }
    funcs.forEach(func => func())
```
达到相同的效果，ES6 简洁的解决方案是不是更让你心动！！！
2.字符串
先聊聊模板字符串
ES6模板字符简直是开发者的福音啊，解决了 ES5 在字符串功能上的痛点。
第一个用途，基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定。
```js
    //ES5 
    var name = 'lux'
    console.log('hello' + name)
    //es6
    const name = 'lux'
    console.log(`hello ${name}`) //hello lux
```
第二个用途，在ES5时我们通过反斜杠(\)来做多行字符串或者字符串一行行拼接。ES6反引号(``)直接搞定。
```js
    // ES5
    var msg = "Hi \
    man!
    "
    // ES6
    const template = `<div>
        <span>hello world</span>
    </div>`
```
对于字符串 ES6+ 当然也提供了很多厉害也很有意思的方法
```js
    // 1.includes：判断是否包含然后直接返回布尔值
    const str = 'hahay'
    console.log(str.includes('y')) // true

    // 2.repeat: 获取字符串重复n次
    const str = 'he'
    console.log(str.repeat(3)) // 'hehehe'
    //如果你带入小数, Math.floor(num) 来处理
    // s.repeat(3.1) 或者 s.repeat(3.9) 都当做成 s.repeat(3) 来处理
    
    // 3. startsWith 和 endsWith 判断是否以 给定文本 开始或者结束
    const str =  'hello world!'
    console.log(str.startsWith('hello')) // true
    console.log(str.endsWith('!')) // true
    
    // 4. padStart 和 padEnd 填充字符串，应用场景：时分秒
    setInterval(() => {
        const now = new Date()
        const hours = now.getHours().toString()
        const minutes = now.getMinutes().toString()
        const seconds = now.getSeconds().toString()
        console.log(`${hours.padStart(2, 0)}:${minutes.padStart(2, 0)}:${seconds.padStart(2, 0)}`)
    }, 1000)
```
关于模板字符串现在比较常出现的面试题有两道。同学们不妨写试试看？
模拟一个模板字符串的实现。
```js
    let address = '北京海淀区'
    let name = 'lala'
    let str = '${name}在${address}上班...'
    // 模拟一个方法 myTemplate(str) 最终输出 'lala在北京海淀区上班...'
    function myTemplate(str) {
        // try it
    }
    console.log(myTemplate(str)) // lala在北京海淀区上班...
```
实现标签化模板(自定义模板规则)。
```js
    const name = 'cc'
    const gender = 'male'
    const hobby = 'basketball'
    // 实现tag最终输出 '姓名：**cc**，性别：**male**，爱好：**basketball**'
    function tag(strings) {
        // do it
    }
    const str = tag`姓名：${name}，性别：${gender}，爱好：${hobby}`
    console.log(str) // '姓名：**cc**，性别：**male**，爱好：**basketball**'
```
### 3.函数
函数默认参数
在ES5我们给函数定义参数默认值是怎么样？
```js
    function action(num) {
        num = num || 200
        //当传入num时，num为传入的值
        //当没传入参数时，num即有了默认值200
        return num
    }
```
但细心观察的同学们肯定会发现，num传入为0的时候就是false，但是我们实际的需求就是要拿到num = 0，此时num = 200 明显与我们的实际想要的效果明显不一样
ES6为参数提供了默认值。在定义函数时便初始化了这个参数，以便在参数没有被传递进去时使用。
```js    
    function action(num = 200) {
        console.log(num)
    }
    action(0) // 0
    action() //200
    action(300) //300
```

### 箭头函数
ES6很有意思的一部分就是函数的快捷写法。也就是箭头函数。
箭头函数最直观的三个特点。
>不需要 function 关键字来创建函数
>省略 return 关键字
>继承当前上下文的 this 关键字

```js
//例如：
    [1,2,3].map(x => x + 1)
    //等同于：
    [1,2,3].map((function(x){
        return x + 1
    }).bind(this))
```
说个小细节。
当你的函数有且仅有一个参数的时候，是可以省略掉括号的。当你函数返回有且仅有一个表达式的时候可以省略`{}` 和 `return`；例如:

```js
    var people = name => 'hello' + name
    //参数name就没有括号
作为参考
    var people = (name, age) => {
        const fullName = 'hello' + name
        return fullName
    } 
    //如果缺少()或者{}就会报错
    //要不整一道笔试题？哈哈哈哈哈哈哈哈。我不管我先上代码了
    // 请使用ES6重构以下代码
    
    var calculate = function(x, y, z) {
      if (typeof x != 'number') { x = 0 }
      if (typeof y != 'number') { y = 6 }
    
      var dwt = x % y
      var result
    
      if (dwt == z) { result = true }
      if (dwt != z) { result = false }
      
      return result
    }
    const calculate = (x, y, z) => {
      x = typeof x !== 'number' ? 0 : x
      y = typeof y !== 'number' ? 6 : y
      return x % y === z
    }
```
### 4.拓展的对象功能
对象初始化简写
ES5我们对于对象都是以键值对的形式书写，是有可能出现键值对重名的。例如：
```js
    function people(name, age) {
        return {
            name: name,
            age: age
        };
    }
```
键值对重名，ES6可以简写如下：
```js
    function people(name, age) {
        return {
            name,
            age
        };
    }
```
ES6 同样改进了为对象字面量方法赋值的语法。ES5为对象添加方法：
```js
    const people = {
        name: 'lux',
        getName: function() {
            console.log(this.name)
        }
    }
```
ES6通过省略冒号与 function 关键字，将这个语法变得更简洁
```js
    const people = {
        name: 'lux',
        getName () {
            console.log(this.name)
        }
    }
```
ES6 对象提供了 Object.assign()这个方法来实现浅复制。
Object.assign() 可以把任意多个源对象自身可枚举的属性拷贝给目标对象，然后返回目标对象。第一参数即为目标对象。在实际项目中，我们为了不改变源对象。一般会把目标对象传为{}
```js
    const objA = { name: 'cc', age: 18 }
    const objB = { address: 'beijing' }
    const objC = {} // 这个为目标对象
    const obj = Object.assign(objC, objA, objB)

    // 我们将 objA objB objC obj 分别输出看看
    console.log(objA)   // { name: 'cc', age: 18 }
    console.log(objB) // { address: 'beijing' }
    console.log(objC) // { name: 'cc', age: 18, address: 'beijing' }
    console.log(obj) // { name: 'cc', age: 18, address: 'beijing' }
    
    // 是的，目标对象ObjC的值被改变了。
    // so，如果objC也是你的一个源对象的话。请在objC前面填在一个目标对象{}
    Object.assign({}, objC, objA, objB)
```
### 5.更方便的数据访问--解构
数组和对象是JS中最常用也是最重要表示形式。为了简化提取信息，ES6新增了解构，这是将一个数据结构分解为更小的部分的过程
ES5我们提取对象中的信息形式如下
```js
    const people = {
        name: 'lux',
        age: 20
    }
    const name = people.name
    const age = people.age
    console.log(name + ' --- ' + age)
```
是不是觉得很熟悉，没错，在ES6之前我们就是这样获取对象信息的，一个一个获取。现在，解构能让我们从对象或者数组里取出数据存为变量，例如
```js
    //对象
    const people = {
        name: 'lux',
        age: 20
    }
    const { name, age } = people
    console.log(`${name} --- ${age}`)
    //数组
    const color = ['red', 'blue']
    const [first, second] = color
    console.log(first) //'red'
    console.log(second) //'blue'
```
要不来点儿面试题，看看自己的掌握情况？
```js
    // 请使用 ES6 重构一下代码

    // 第一题
    var jsonParse = require('body-parser').jsonParse
    
    // 第二题
    var body = request.body
    var username = body.username
    var password = body.password
    
    // 1.
    import { jsonParse } from 'body-parser'
    // 2. 
    const { body, body: { username, password } } = request
```
### 6.Spread Operator 展开运算符
ES6中另外一个好玩的特性就是Spread Operator 也是三个点儿...接下来就展示一下它的用途。
组装对象或者数组
```js
    //数组
    const color = ['red', 'yellow']
    const colorful = [...color, 'green', 'pink']
    console.log(colorful) //[red, yellow, green, pink]
    
    //对象
    const alp = { fist: 'a', second: 'b'}
    const alphabets = { ...alp, third: 'c' }
    console.log(alphabets) //{ "fist": "a", "second": "b", "third": "c"
}
```
有时候我们想获取数组或者对象除了前几项或者除了某几项的其他项
```js
    //数组
    const number = [1,2,3,4,5]
    const [first, ...rest] = number
    console.log(rest) //2,3,4,5
    //对象
    const user = {
        username: 'lux',
        gender: 'female',
        age: 19,
        address: 'peking'
    }
    const { username, ...rest } = user
    console.log(rest) //{"address": "peking", "age": 19, "gender": "female"
}
```
对于 Object 而言，还可以用于组合成新的 Object 。(ES2017 stage-2 proposal) 当然如果有重复的属性名，右边覆盖左边
```js
    const first = {
        a: 1,
        b: 2,
        c: 6,
    }
    const second = {
        c: 3,
        d: 4
    }
    const total = { ...first, ...second }
    console.log(total) // { a: 1, b: 2, c: 3, d: 4 }
```
### 7.import 和 export
import导入模块、export导出模块
```js
//全部导入import people from './example'
//有一种特殊情况，即允许你将整个模块当作单一对象进行导入//该模块的所有导出都会作为对象的属性存在import * as example from "./example.js"console.log(example.name)console.log(example.age)console.log(example.getName())
//导入部分import {name, age} from './example'
// 导出默认, 有且只有一个默认export default App
// 部分导出export class App extend Component {};
```
以前有人问我，导入的时候有没有大括号的区别是什么。下面是我在工作中的总结：
>1.当用export default people导出时，就用 import people 导入（不带大括号）
>2.一个文件里，有且只能有一个export default。但可以有多个export。
>3.当用export name 时，就用import { name }导入（记得带上大括号）
>4.当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age } 
>5.当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example

### 8. Promise
在promise之前代码过多的回调或者嵌套，可读性差、耦合度高、扩展性低。通过Promise机制，扁平化的代码机构，大大提高了代码可读性；用同步编程的方式来编写异步代码，保存线性的代码逻辑，极大的降低了代码耦合性而提高了程序的可扩展性。
说白了就是用同步的方式去写异步代码。
发起异步请求
```js
    fetch('/api/todos')
      .then(res => res.json())
      .then(data => ({ data }))
      .catch(err => ({ err }));
```
今天看到一篇关于面试题的很有意思。
```js
    setTimeout(function() {
      console.log(1)
    }, 0);
    new Promise(function executor(resolve) {
      console.log(2);
      for( var i=0 ; i<10000 ; i++ ) {
        i == 9999 && resolve();
      }
      console.log(3);
    }).then(function() {
      console.log(4);
    });
    console.log(5);
```
Excuse me？这个前端面试在搞事！
当然以上promise的知识点，这个只是冰山一角。需要更多地去学习了解一下。

### 9.Generators
生成器（ generator）是能返回一个迭代器的函数。生成器函数也是一种函数，最直观的表现就是比普通的function多了个星号*，在其函数体内可以使用yield关键字,有意思的是函数会在每个yield后暂停。
这里生活中有一个比较形象的例子。咱们到银行办理业务时候都得向大厅的机器取一张排队号。你拿到你的排队号，机器并不会自动为你再出下一张票。也就是说取票机“暂停”住了，直到下一个人再次唤起才会继续吐票。
OK。说说迭代器。当你调用一个generator时，它将返回一个迭代器对象。这个迭代器对象拥有一个叫做next的方法来帮助你重启generator函数并得到下一个值。next方法不仅返回值，它返回的对象具有两个属性：done和value。value是你获得的值，done用来表明你的generator是否已经停止提供值。继续用刚刚取票的例子，每张排队号就是这里的value，打印票的纸是否用完就这是这里的done。
```js
    // 生成器
    function *createIterator() {
        yield 1;
        yield 2;
        yield 3;
    }
  
    // 生成器能像正规函数那样被调用，但会返回一个迭代器
    let iterator = createIterator();
  
    console.log(iterator.next().value); // 1
    console.log(iterator.next().value); // 2
    console.log(iterator.next().value); // 3
```
那生成器和迭代器又有什么用处呢？
围绕着生成器的许多兴奋点都与异步编程直接相关。异步调用对于我们来说是很困难的事，我们的函数并不会等待异步调用完再执行，你可能会想到用回调函数，（当然还有其他方案比如Promise比如Async/await）。
生成器可以让我们的代码进行等待。就不用嵌套的回调函数。使用generator可以确保当异步调用在我们的generator函数运行一下行代码之前完成时暂停函数的执行。
那么问题来了，咱们也不能手动一直调用next()方法，你需要一个能够调用生成器并启动迭代器的方法。就像这样子的
```js
    function run(taskDef) { //taskDef即一个生成器函数

        // 创建迭代器，让它在别处可用
        let task = taskDef();
        
        // 启动任务
        let result = task.next();
        
        // 递归使用函数来保持对 next() 的调用
        function step() {
        
            // 如果还有更多要做的
            if (!result.done) {
                result = task.next();
                step();
            }
        }
        
        // 开始处理过程
        step();
  
    }
```
生成器与迭代器最有趣、最令人激动的方面，或许就是可创建外观清晰的异步操作代码。你不必到处使用回调函数，而是可以建立貌似同步的代码，但实际上却使用 yield 来等待异步操作结束。

## 总结

ES6新特性远不止于此，但对于我们日常的开发来说。这算不上全部，但是能算得上是高频使用了。当然还有很有好玩有意思的特性。比如一些数组的新方法、class...等等。包括用set处理数组去重问题等等。我和我的小伙伴们都惊呆了!
<br>
<br>
<center><font color="#6e75e4" size="6">Node.JS</font></center>
<br>
process模块在使用的使用无需通过require()函数来加载该模块，可以直接使用。
Fs模块，在使用的时候，必须通过require()函数来加载该模块，方可使用。
原因：`process`模块是全局的模块，而`fs`模块不是全局模块，全局模块可以直接使用，而非全局模块需要先通过`require()`加载该模块。
根据用户的不同请求，服务器做出不同的响应

<h2>1.加载http模块</h2>

```js
Var http = require('http');
```



<h3>2.创建http服务</h3>

```js
http.createServer(function(req,res){
```

<h4>(1)获取用户请求的路径</h4>

```js
req.url
```
<h4>(2)结束响应</h4>

```js
res.end();
});
```
异步操作：`try-catch`  是无法扑抓异常
在请求服务器的时候，请求的`url`就是一个标识
创建一个`package.json`文件：

<blockquote>
    <p>1.通过npm init 命令或者npm init -y 或 npm init -yes命令</p>
    <p></p>
    <p>2.手动创建一个</p>
</blockquote>


创建的文件命名不能使用中文&&大写字母&&特殊符号
npm ----->  yarn(运行速度快)![](https://qq292383147.github.io/pictureLibrary/picture/es6_nodeJS/1.png) （下载最新版本的jQuery）
如果想下载其他版本的jquery，可以输入：![](https://qq292383147.github.io/pictureLibrary/picture/es6_nodeJS/2.png)
（shift +鼠标右键）
<br>
<h2>Node.js特点：</h2>
<blockquote>
<p>1、单线程</p>
<p>2、非阻塞I/O(异步I/O)</p>
<p>3、事件驱动</p>
</blockquote>

<h2>执行Node环境代码的方式：</h2>
<h3>1.直接在命令行中输入node,进入Node的REPL运行环境</h3>
<blockquote>
<p>(1)R：Read:读取</p>
<p></p>
<p>(2)E：Evaluate：执行</p>
<p></p>
<p>(3)P：Print：输出</p>
<p></p>
<p>(4)L：Loop：循环</p>
</blockquote>

2.将Node代码写入到一个js文件中，然后通过node要执行的JS文件路径去运行Node代码
<h2>模块</h2>
<h3>Javascript中的缺点：</h3>
<blockquote>
<p>1、在ES6之前没有模块系统</p>
<p>2、Javascript没有标准库，除了一些核心库以外，没有有文件系统API，没有IO流API</p>
<p>3、没有标准接口</p>
<p>4、没有包管理系统，不能自动下载和安装依赖</p>
<p>5、如果程序到达一定规模，必须将其模块化</p>
<p>Node.js正好补Javascript的缺点，出现了CommonJS规范</p>
</blockquote>

<h2>CommonJS模块的定义</h2>
模块引用 `require()` 方法， 这个方法接受模块标识，例如let math = require('math')
模块定义 `exports` 对象用于导出当前模块的方法或者变量，并且它是唯一导出的出口
模块标识 模块标识其实就是传递给`require()`方法的参数，它必须是符合小驼峰命名的字符串，或者以. .. 开头的相对路径，或者绝对路径。它可以没有文件名后缀.js

实际上每个模块内部都是匿名自调函数
`exports`对象是当前模块的导出对象，用于导出模块公有方法和属性。别的模块通过require函数使用当前模块时得到的就是当前模块的exports对象

`require`函数用于在当前模块中加载和使用别的模块，传入一个模块名，返回一个模块导出对象,模块名中的.js扩展名可以省略

module对象表示当前模块本身，exports只是module的属性，导出模块既可以通过exports导出，也可以通过module.exports导出 consle.log(exports) console.log(module.exports) console.log(exports === module.exports)

`__filename` 当前文件的绝对路径 `__dirname` 当前文件所在的目录

<h3>exports 和 module.exports的区别</h3>
exports = {}赋值新对象有问题
exports是对module.exports的引用。导出模块以module.exports为准
NPM包管理工具
先使用`npm init -y`初始化一下包管理文件`package.json`，将来所有安装的包，都会记录到这个文件中
使用`npm install 包名 --save`(默认)/--save-dev去安装包；其中，`install`可以简写成`i`;
`--save`表示把包安装到部署依赖中（在开发和部署上线都需要使用的包）； `--save-dev`表示安装到开发依赖（只在项目开发阶段需要用到的包）；
`--save`可以简写成`-S`；`--save-dev`可以简写成`-D`;
`npm uninstall 包名 --save/--save-dev`或者`npm remove 包名 --save/--save-dev`
```shell
npm i webpack -g,
```
其中，`-g`表示全局安装某些包，通过`-g`安装的包都在C:\Users\用户名\AppData\Roaming\npm下面
查看全局安装的包：
```shell
npm list -g --depth 0
```
如果需要下载指定版本，通过@符号指定版本号，npm i jquery@1.9 -S

```shell
npm cache clean --force 清除缓存命令
```

![](https://qq292383147.github.io/pictureLibrary/picture/es6_nodeJS/3.png)

网络环境（网速差）

```shell
npm i nrm -g      安装
nrm ls			 查询使用的默认网路
nrm use taobao    切换到NPM包托管网站为淘宝，可以设置cnrm(国内)
```


（重要）包描述文件`package.json`
`name`: 包名，需要在NPM上是唯一的。不能带有空格
`description`:包简介。通常会显示在一些列表中。
`version`:版本名。一个语义化的版本号，通常为x.y.z。该版本号十分重要，常常用于NPM中的分类搜索。
`maintrainers`:包维护者的数组。数组元素是一个包含name、email、web三个属性的json对象。
`contributors`:包贡献者的数组。第一个就是包作者本人。在开源社区，如果提交的`patch`被`merge`进`master`分支的话，就应当加上这个贡献patch的人，格式包含`name`和：`email`。
	
`bugs`:一个可以提交bug的URL地址。地址可以是邮件地址，也可以是网址

`licenses` : 包所使用的许可证。例如： "licenses": [{ "type": "GPLv2", "url": "http://www.example.com/licenses/gpl.html", }]

`repositories`:托管源代码的地址数组。

⭐`dependencies`:当前包需要的依赖。这个属性十分重要，NPM会通过这个属性，帮你自动记载依赖的包。

`homepage`:当前包的网站地址。

`os`:操作系统支持列表。

`cpu`:CPU架构的支持列表。

`engine`:支持的JavaScript引擎列表。

`builtin`:标志当前包是否是内建在底层系统的标准组件。

`drectories`:包目录说明。

`implements`:实现规范的列表。

⭐`scripts`:脚本说明对象。该对象指明了在进行操作时运行哪个文件，或者执行哪条命令。
author。包作者。

`bin`:一些包作者希望包可以作为命令行工具使用。

⭐`main`:模块引入方法`require()`在引入包时，会优先检查这个字段，并将其作为包中其余模块的入口，如果不存在这个字段，`require()`方法会查找包目录下的index.js、index.node、index.json文件作为默认入口。

⭐`devDependencies`:一些模块只有在开发时需要的依赖。

<font color="#e4l2">Node.JS</font>分为三种模块：

<blockquote>
<p>1、核心模块</p>
<p>2、用户模块</p>
</blockquote>
(1)含后缀名-按照相对路径或绝对路径根据文件名直接查找
(2)不含后缀名-先自动补全后缀名查找，如果没有找到，则把它当成一个文件夹，在该文件夹在找index.js文件
第三方模块
<br>

<h2>fs核心模块 file system</h2>

<h3>1、fs.readFile</h3>

模块是文件操作的封装，它提供了文件的读取、写入、更名、删除、遍历目录、链接等 POSIX 文件系统操作。

```js
let fs = require('fs')

fs.readFile('./files/01.txt', 'utf-8', (err, data) => {
  if (!err) {
    console.log(data);
  } else {
    console.log(err);
  }
})

```

<h3>2、fs.writeFile</h3>

```js
let fs = require('fs')

fs.writeFile('./01.txt', 'hello world', (err) => {
  if (err) throw err
  console.log('写入成功');
})

```



<h3>3、fs.appendFile</h3>

```js
let fs = require('fs');

// 追加文件内容
fs.appendFile('./files/01.txt', '我是追加内容', (err) => {
  if (err) throw err;
  console.log('内容追加成功');
})
回调函数callback
function wabao(map, callback) { 
  setTimeout(() => {
    if (map === 1) {
      callback()
    } else {
      console.log('没有找到宝藏！');
    }
  }, 1000);
}
// 比如你去挖宝藏，你带了一张地图（map）,经过一段时间后（setTimeout）
// 1. 你挖到了，然后你拿到这个宝藏，执行一些操作（callback）
// 2. 你没有挖到，就打印一个没有找到宝藏的提示信息
wabao(2, () => {
  console.log('挖到了，去换金币吧！')
})

```

<h2>http核心模块</h2>

`Node.js` 标准库提供了 http 模块，其中封装了一个高效的 HTTP 服务器和一个简易的HTTP 客户端。 http.Server 是一个基于事件的 HTTP 服务器对象， 它的核心由 Node.js 下层 C++部分实现，而接口由 JavaScript 封装，兼顾了高性能与简易性。 `http.request` 则是一个HTTP 客户端工具，用于向 HTTP 服务器发起请求
<font color="#4ca08f">// req 是 http.IncomingMessage的实例，表示请求消息；通过 request 对象，能够拿到客户端提交过来的数据、报文头、报文体；</font>
<font color="#4ca08f">// res 是  http.ServerResponse的实例，表示响应消息，可以通过 response 对象，把处理的结果返回给浏览器</font>

<br>

<center><font color="#8d8df0" size="9">模板引擎</font></center>

<h2>art-template</h2>

> 模板文件的路径不能是相对路径，应该是绝对路径

思路：
>  1. 首先我应该把服务器创建起来，能让客户端访问
>  2. 规定好客户端访问哪个路径 我的服务器才给他返回数据
>  3. 我返回的数据以什么样的形式返回？（我们这里是希望利用art-template返回处理完的数据）
>  4. 通过res.end()将处理好的数据返回给客户端

<br>

## express模块

### 安装

```shell
npm init -y
npm install express --save
```
### ejs渲染数据

```shell
安装 npm install ejs --save
```

### 设置

view engine, 模板引擎，比如： app.set('view engine', 'ejs')
views, 放模板文件的目录，比如： app.set('views', './views')
使用
基本使用
循环渲染数据
include其他模板
托管静态资源

```js
// 引入express模块
let express = require('express')
let fs = require('fs')

// 创建一个express实例
let app = express()

// 设置模板引擎为ejs
app.set('view engine', 'ejs')
// 设置模板文件的目录为 ./views
app.set('views', './views')

// 设置静态资源路径，注意此处的静态资源可以设置多个
app.use('/public', express.static('public'));

app.get('/', (req, res) => {
  // res.render('index.ejs', { title: 'hello world' })
  // 省略后缀名也可以
  res.render('index', {title: 'hello world', list: ['香蕉', 'banana', 'apple', 'pear']})
})

app.post('/', function (req, res) {
  console.log('post some data');
});

app.listen(3000, () => {
  console.log('server is running at localhost:3000');
})
```



```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <link rel="stylesheet" href="/public/css/index.css">
</head>
<body>
  <%- include('./layout/header.ejs') %>
  <h1><%= title %></h1>
  <ul>
  <% list.forEach( fruit => {%>
    <li><%= fruit %></li>
  <%})%>
  </ul>
  <%- include('./layout/footer.ejs') %>
</body>
</html>
```

## 中间件

```js
// 引入express模块
let express = require('express')

// 创建一个express实例
let app = express()

app.use('/', (req, res, next) => {
  console.log('调用第一个中间件，接着调用next（）');
  next()
}, (req, res, next) => {
  console.log('我还是第一个中间件，接着调用next（）');
  next()
})
app.use('/', function (req, res, next) {
  console.log('调用第二个中间件，接着调用next（）');
  next()
});
app.use('/', function (req, res) {
  console.log('调用第三个中间件，并结束');
  res.send('结束了')
});
app.listen(3000, () => {
  console.log('server is running at localhost:3000');
})
// 设置静态资源路径，注意此处的静态资源可以设置多个（静态托管）
app.use('/public', express.static('public'));

```
<br>
查询字符串（`req.query`）
<br>
提交数据（`req.body`）
<br>
处理原生get请求参数：通过url核心模块将路径转换成url对象（主要运用url.parse()方法）
处理原生的post请求参数：
>1、监听参数数据传输事件：data
>2、监听数据传输结束事件：end
>3、注意传输完成之后获取到的数据是字符串，需要利用querystring核心模块将其转换成对象

### Express

### 1、get请求参数

>(1)取查询参数，也就是url后面？的参数，通过req.query.xxxx
>(2)取路由参数，通过req.params.xxxx

### 2、post请求参数

>(1)使用第三方中间件body-parser处理post起求参数，它会在请求对象req上面绑定一个body属性，body属性里面放的就是参数
>(2)注意：body-parser必须使用路由中间件之前调用
<br>

### 3、使用ejs

>(1)下载`npm i ejs -S`
>(2)设置模板引擎文件存放目录
>(3)设置应用程序使用的模板引擎为`ejs`
>(4)渲染模板引擎文件使用`res.render()`方法
>(5)至于模板引擎中的动态数据，就按照`ejs`的语法去写

<br>

### 4、托管静态文件

> (1)App.use(express.static(‘assets’))
<br
>
### 5、中间件

>(1)中间件就是一些函数，这些函数里面可以执行任何代码，他可以去获取req或者res对象并修改他们，使用了一个中间件之后，注意调用next()进入下一个中间件，不然后面不会被执行

### 6、路由中间件

>(1)目的：为了实现模块化管理，方便代码维护
>(2)主要是利用express.Router()方法创建路由实例

```shell
监听命令：npm i nodemon -g

Node 自动下载包
package-lock.json\package.json
```

![](https://qq292383147.github.io/pictureLibrary/picture/es6_nodeJS/4.png)

![](https://qq292383147.github.io/pictureLibrary/picture/es6_nodeJS/5.png)

```js
//引入MD5
let md5 = require('blueimp-md5');
user.password = md5(user.password, config.PWDSALT)
module.exports = {
  PWDSALT: 'itcast'
}
```

## cookie-parser

### API

```js
var express = require('express')
var cookieParser = require('cookie-parser')
var app = express()app.use(cookieParser())
```

### express-session

会话数据不会保存在cookie本身中，只会保存在会话ID中。会话数据存储在服务器端。
API

```js
var session = require('express-session')
req.session
要存储或访问会话数据，只需使用Request属性req.session，它(通常)被存储区序列化为JSON，因此嵌套的对象通常是很好的。
      islogin:req.session.islogin, // 从 session 中获取用户是否登录
      user: req.session.user // 从 session 中获取用户信息
```

#### 错误优先回调函数

>通俗的讲，在node中，我们在设计一个回调函数的时候，要优先解决错误，然后再传参

<br>
Callback是个重点，callback函数是回调函数，在异步操作完成之后它才被调用的。一般情况下不需要返回值，只需要处理异步操作结束后的逻辑。为了规范其使用，我们约定callback的第一个参数为err（即异步操作内的异常错误等等），第二个为处理的结果，当err===null时，即没有在异步操作中发生错误（异常）。

## 工作中常用到的ES6语法

### 一、let和const

>在JavaScript中咱们以前主要用关键var来定义变量，ES6之后，新增了定义变量的两个关键字，分别是let和const。 对于变量来说，在ES5中var定义的变量会提升到作用域中所有的函数与语句前面，而ES6中let定义的变量则不会，let声明的变量会在其相应的代码块中建立一个暂时性死区，直至变量被声明。 let和const都能够声明块级作用域，用法和var是类似的，let的特点是不会变量提升，而是被锁在当前块中。

<br>

一个非常简单的例子：
```js
function test(){
if(true){
console.log(a)//TDZ，俗称临时死区，用来描述变量不提升的现象
let a =1
}
}
test()// a is not defined
function test(){
if(true){
let a =1
}
console.log(a)
}
test()// a is not defined
唯一正确的使用方法：先声明，再访问。

function test(){
if(true){
let a =1
console.log(a)
}
}
test()// 1
const 声明常量，一旦声明，不可更改，而且常量必须初始化赋值。 const虽然是常量，不允许修改默认赋值，但如果定义的是对象Object，那么可以修改对象内部的属性值。

const type ={
a:1
}
type.a =2//没有直接修改type的值，而是修改type.a的属性值，这是允许的。
console.log(type)// {a: 2}
```

`const`和`let`的异同点相同点：`const`和`let`都是在当前块内有效，执行到块外会被销毁，也不存在变量提升（TDZ），不能重复声明。 不同点：`const`不能再赋值，`let`声明的变量可以重复赋值。 `const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。
<br>

>块级作用域的使用场景除了上面提到的常用声明方式，我们还可以在循环中使用，最出名的一道面试题：循环中定时器闭包的考题 在for循环中使用var声明的循环变量，会跳出循环体污染当前的函数。

```js
for(var i =0; i <5; i++){
setTimeout(()=>{
console.log(i)//5, 5, 5, 5, 5
},0)
}
console.log(i)//5 i跳出循环体污染外部函数
//将var改成let之后
for(let i =0; i <5; i++){
setTimeout(()=>{
console.log(i)// 0,1,2,3,4
},0)
}
console.log(i)//i is not defined i无法污染外部函数
```

>在实际开发中，我们选择使用var、let还是const，取决于我们的变量是不是需要更新，通常我们希望变量保证不被恶意修改，而使用大量的const。使用const声明，声明一个对象的时候，也推荐使用const，当你需要修改声明的变量值时，使用let，var能用的场景都可以使用let替代。
<br>

>symbolES6 以前，我们知道5种基本数据类型分别是Undefined，Null，Boolean，Number以及String，然后加上一种引用类型Object构成了JavaScript中所有的数据类型，但是ES6出来之后，新增了一种数据类型，名叫symbol，像它的名字表露的一样，意味着独一无二，意思是每个 Symbol类型都是独一无二的，不与其它 Symbol 重复。 可以通过调用 Symbol() 方法将创建一个新的 Symbol 类型的值，这个值独一无二，不与任何值相等。

<br>

```js
var mySymbol=Symbol();
console.log(typeof mySymbol)//"symbol"
```

## 二、字符串

### ES6字符串新增的方法

UTF-16码位：ES6强制使用UTF-16字符串编码。关于UTF-16的解释请自行百度了解。
<br>
`codePointAt()`：该方法支持UTF-16，接受编码单元的位置而非字符串位置作为参数，返回与字符串中给定位置对应的码位，即一个整数值。
<br>
`String.fromCodePoiont()`：作用与codePointAt相反，检索字符串中某个字符的码位，也可以根据指定的码位生成一个字符。
<br>
`normalize()`：提供Unicode的标准形式，接受一个可选的字符串参数，指明应用某种Unicode标准形式。
<br>
在ES6中，新增了3个新方法。每个方法都接收2个参数，需要检测的子字符串，以及开始匹配的索引位置。
<br>
模板字符串字符串是JavaScript中基本类型之一，应该算是除了对象之外是使用最为频繁的类型吧，字符串中包含了例如substr，replace，indexOf,slice等等诸多方法，ES6引入了模板字符串的特性，用反引号来表示，可以表示多行字符串以及做到文本插值（利用模板占位符）。
<br>

```js
// 以前的多行字符串我们这么写：
console.log("hello world 1\n\
hello cala");
// "hello world
// hello cala"
//有了模板字符串之后
console.log(`hello world
string text line 2`);
// "hello world
// hello cala"
```

可以用${}来表示模板占位符，可以将你已经定义好的变量传进括弧中，例如：
```js
var name="cala";
var age=22;
console.log(`hello,I'am ${name},my age is ${age}`)
//hello,I'am cala,my age is 22
includes(str, index)：如果在字符串中检测到指定文本，返回true，否则false。

let t ='abcdefg'
if(t.includes('cde')){
console.log(2)
}
//true
startsWith(str, index)：如果在字符串起始部分检测到指定文本，返回true，否则返回false。

let t ='abcdefg'
if(t.startsWith('ab')){
console.log(2)
}
//true
endsWith(str, index)：如果在字符串的结束部分检测到指定文本，返回true，否则返回false。

let t ='abcdefg'
if(t.endsWith('fg')){
console.log(2)
}
//true
```

如果你只是需要匹配字符串中是否包含某子字符串，那么推荐使用新增的方法，如果需要找到匹配字符串的位置，使用`indexOf()`。

### 三、函数

函数的默认参数 在ES5中，我们给函数传参数，然后在函数体内设置默认值，如下面这种方式。
```js
function a(num, callback){
num = num ||6
callback = callback ||function(data){console.log('ES5: ', data)}
callback(num * num)
}
a()//ES5: 36，不传参输出默认值
//你还可以这样使用callback
a(10,function(data){
console.log(data *10)// 1000， 传参输出新数值
})
在ES6中，我们使用新的默认值写法

function a(num =6, callback =function(data){console.log('ES6: ', data)}){
callback(num * num)
}
a()//ES6: 36， 不传参输出默认值
a(10,function(data){
console.log(data *10)// 1000，传参输出新数值
})
```

### 四、箭头函数（<font color="#828dd4">=></font>）

（箭头函数比较重要，现在简单提一下，迟一点有空专门写一篇箭头函数的文章。）

```js
const arr =[5,10]
const s = arr.reduce((sum, item)=> sum + item)
console.log(s)// 15
```
箭头函数中this的使用跟普通函数也不一样，在JavaScript的普通函数中，都会有一个自己的this值，主要分为： 普通函数： 1、函数作为全局函数被调用时，this指向全局对象 2、函数作为对象中的方法被调用时，this指向该对象 3、函数作为构造函数的时候，this指向构造函数new出来的新对象 4、还可以通过call，apply，bind改变this的指向 箭头函数：1、箭头函数没有this，函数内部的this来自于父级最近的非箭头函数，并且不能改变this的指向。 2、箭头函数没有super 3、箭头函数没有arguments 4、箭头函数没有new.target绑定。 5、不能使用new 6、没有原型 7、不支持重复的命名参数。

箭头函数的简单理解

### 1、箭头函数的左边表示输入的参数，右边表示输出的结果。

```js
const s = a => a
console.log(s(2))// 2
```



### 2、在箭头函数中，this属于词法作用域，直接由上下文确定，对于普通函数中指向不定的this，箭头函数中处理this无疑更加简单，如下：

```js
//ES5普通函数
functionMan(){
this.age=22;
returnfunction(){
this.age+1;
}
}
var cala=newMan();
console.log(cala())//undefined
//ES6箭头函数
functionMan(){
this.age=22;
return()=>this.age+1;
}
var cala=newMan();
console.log(cala())//23
```


### 3、箭头函数中没有arguments(我们可以用rest参数替代),也没有原型，也不能使用new 关键字，例如：

```js
//没有arguments
var foo=(a,b)=>{return arguments[0]*arguments[1]}
console.log(foo(3,5))
//arguments is not defined
//没有原型
varObj=()=>{};
console.log(Obj.prototype);
// undefined
//不能使用new 关键字
varObj=()=>{"hello world"};
var o =newObj();
// TypeError: Obj is not a constructor
```



### 4、箭头函数给数组排序

```js
const arr =[10,50,30,40,20]
const s = arr.sort((a, b)=> a - b)
console.log(s)// [10,20,30,40,50]
```

尾调用优化 尾调用是指在函数return的时候调用一个新的函数，由于尾调用的实现需要存储到内存中，在一个循环体中，如果存在函数的尾调用，你的内存可能爆满或溢出。

ES6中，引擎会帮你做好尾调用的优化工作，你不需要自己优化，但需要满足下面3个要求： 
>1、函数不是闭包
>2、尾调用是函数最后一条语句
>3、尾调用结果作为函数返回

尾调用实际用途——递归函数优化在ES5时代，我们不推荐使用递归，因为递归会影响性能。 但是有了尾调用优化之后，递归函数的性能有了提升。

```js
//新型尾优化写法
"use strict";
function a(n, p =1){
if(n <=1){
return1* p
}
let s = n * p
return a(n -1, s)
}
//求 1 x 2 x 3的阶乘
let sum = a(3)
console.log(sum)// 6
```

### 五、ES6对象新增方法

`Object.assign()`方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。 
`Object.assign` 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的`[Get]`和目标对象的`[Set]`，所以它会调用相关 `getter` 和 `setter`。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含`getter`，这可能使其不适合将新属性合并到原型中。为了将属性定义（包括其可枚举性）复制到原型，应使用`Object.getOwnPropertyDescriptor()`和`Object.defineProperty()` 。 `String`类型和 `Symbol` 类型的属性都会被拷贝。 合并对象

```js
var o1 ={ a:1};
var o2 ={ b:2};
var o3 ={ c:3};
var obj =Object.assign(o1, o2, o3);
console.log(obj);// { a: 1, b: 2, c: 3 }
console.log(o1);// { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
//合并具有相同属性的对象

var o1 ={ a:1, b:1, c:1};
var o2 ={ b:2, c:2};
var o3 ={ c:3};
var obj =Object.assign({}, o1, o2, o3);
console.log(obj);// { a: 1, b: 2, c: 3 }
```

### 六、Map和Set

`Map`和`Set`都叫做集合，但是他们也有所不同。`Set`常被用来检查对象中是否存在某个键名，Map集合常被用来获取已存的信息。 `Set`是有序列表，含有相互独立的非重复值。`Array`和`Set`对比都是一个存储多值的容器，两者可以互相转换，但是在使用场景上有区别。
如下: 
<br>
`Array`的`indexOf`方法比`Set`的`has`方法效率低下 `Set`不含有重复值（可以利用这个特性实现对一个数组的去重） `Set`通过`delete`方法删除某个值，而`Array`只能通过`splice`。两者的使用方便程度前者更优 `Array`的很多新方法`map`、`filter`、`some`、`every`等是`Set`没有的（但是通过两者可以互相转换来使用） `Object`和`Map`对比`Object`是字符串-值，`Map`是值->值 `Object`键为`string`类型,`Map`的键是任意类型 手动计算`Object`尺寸,`Map.size`可以获取尺寸 `Map`的排序是插入顺序 `Object`有原型，所以映射中有一些缺省的键。可以理解为 <font color="#67d0e4">Map</font> = <font color="#e62b6f">Object</font>.create(`null`)

## Set操作集合
```js
let set = new Set()
// Set转化为数组
let arr = Array.from(set)
let arr = [...set]
// 实例属性（继承自Set）
set.constructor === Set
set.size
// 操作方法
set.add(1)// 添加一个值
set.delete(1)//删除一个值
set.has(1)//判断是否有这个值（Array中的indexOf）
set.clear()//清除所有值
// 获取用于遍历的成员方法(Set的遍历顺序就是插入顺序)
set.keys()// 返回键名的遍历器
set.values()// 返回键值得遍历器
set.entries()// 返回键值对的遍历器
set.forEach()// 循环遍历每个值(和Array的方法一致)
for(let key of set.keys()){}
for(let val of set.values()){}
for(let entry of set.entries()){}
// 使用数组方法来处理set值
    set = new Set(arr)
    set = new Set([...set].map((x)=> x = x *2))
    set = new Set([...set].filter((x)=> x >2))
Map的方法集合

let map =newMap()
// 实例属性(继承自Map)
map.constructor ===Map
map.size
// 操作方法
map.set(1,2)
map.get(1)
map.delete(1)
map.has(1)
map.clear()
// 遍历方法
map.keys()
map.values()
map.entries()
map.forEach()
// Map和数组的转换
map = new Map([['key','val'],[2,1]])// 要求双成员数组
let arr =[...map]
// 值得注意的是Map的键是跟内存绑定的
map.set([1],'s')
map.get([1])
let arr =[1]
let arr1 =[1]
map.set(arr,'s')
map.get(arr)
map.set(arr1,'s')
map.get(arr1)
```

### 七、迭代器（Iterator）

#### 1、entries() 返回迭代器：返回键值对
```js
//数组
const arr =['a','b','c'];
for(let v of arr.entries()){
console.log(v)
}
// [0, 'a'] [1, 'b'] [2, 'c']
//Set
const arr =newSet(['a','b','c']);
for(let v of arr.entries()){
console.log(v)
}
// ['a', 'a'] ['b', 'b'] ['c', 'c']
//Map
const arr = new Map();
arr.set('a','a');
arr.set('b','b');
for(let v of arr.entries()){
console.log(v)
}
// ['a', 'a'] ['b', 'b']
```

#### 2、values() 返回迭代器：返回键值对的value
```js
//数组
const arr =['a','b','c'];
for(let v of arr.values()){
    console.log(v)
}
//'a' 'b' 'c'
//Set
const arr = new Set(['a','b','c']);
for(let v of arr.values()){
console.log(v)
}
// 'a' 'b' 'c'
//Map
const arr = new Map();
arr.set('a','a');
arr.set('b','b');
for(let v of arr.values()){
console.log(v)
}
// 'a' 'b'
```

### 3、keys() 返回迭代器：返回键值对的key
```js
//数组
const arr =['a','b','c'];
for(let v of arr.keys()){
console.log(v)
}
// 0 1 2
//Set
const arr =new Set(['a','b','c']);
for(let v of arr.keys()){
console.log(v)
}
// 'a' 'b' 'c'
//Map
const arr =new Map();
arr.set('a','a');
arr.set('b','b');
for(let v of arr.keys()){
console.log(v)
}
// 'a' 'b'
```
虽然上面列举了3种内建的迭代器方法，但是不同集合的类型还有自己默认的迭代器，在`for of`中，数组和`Set`的默认迭代器是`values()`，`Map`的默认迭代器是`entries()`。

for of循环解构

对象本身不支持迭代，但是我们可以自己添加一个生成器，返回一个`key`，`value`的迭代器，然后使用`for of`循环解构`key`和`value`。

```js
const obj ={
a:1,
b:2,
*[Symbol.iterator](){
for(let i in obj){
yield[i, obj[i]]
}
}
}
for(let[key, value] of obj){
console.log(key, value)
}
// 'a' 1, 'b' 2
```
### 字符串迭代器
```js
const str ='abc';
for(let v of str){
console.log(v)
}
// 'a' 'b' 'c'
```
ES6给数组添加了几个新方法：`find()`、`findIndex()`、`fill()`、`copyWithin()`

1、`find()`：传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它，并且终止搜索。
<br>
<br>
```js
const arr =[1,"2",3,3,"2"]
console.log(arr.find(n =>typeof n ==="number"))// 1
```
2、`findIndex()`：传入一个回调函数，找到数组中符合当前搜索规则的第一个元素，返回它的下标，终止搜索。
<br>
```js
const arr =[1,"2",3,3,"2"]
console.log(arr.findIndex(n =>typeof n ==="number"))// 0
```
3、`fill()`：用新元素替换掉数组内的元素，可以指定替换下标范围。
<br>

```js
arr.fill(value, start,end)
```

4、`copyWithin()`：选择数组的某个下标，从该位置开始复制数组元素，默认从0开始复制。也可以指定要复制的元素范围。
<br>
```js
arr.copyWithin(target, start,end)
const arr =[1,2,3,4,5]
console.log(arr.copyWithin(3))// [1,2,3,1,2] 从下标为3的元素开始，复制数组，所以4, 5被替换成1, 2
const arr1 =[1,2,3,4,5]
console.log(arr1.copyWithin(3,1))// [1,2,3,2,3] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，所以4, 5被替换成2, 3
const arr2 =[1,2,3,4,5]
console.log(arr2.copyWithin(3,1,2))// [1,2,3,2,5] 从下标为3的元素开始，复制数组，指定复制的第一个元素下标为1，结束位置为2，所以4被替换成2
```
ES6中类class、Promise与异步编程、代理（Proxy）和反射（Reflection）API，这几块内容比较复杂，以后有机会再详细写。