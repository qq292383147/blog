---
title: 用async await 来处理异步
date: 2019-03-17 23:57:12
updated: 2019-05-24 15:20:22
tags: JavaScript
type: JavaScript
categories: JavaScript
---
## Async/await

有一种特殊的语法可以更舒适地与promise协同工作，它叫做`async/await`，它是非常的容易理解和使用。

### Async functions

让我们先从`async`关键字说起，它被放置在一个函数前面。就像下面这样：

```js
async function f() {
    return 1
}
```

函数前面的`async`一词意味着一个简单的事情：这个函数总是返回一个promise，如果代码中有`return <非promise>`语句，JavaScript会自动把返回的这个value值包装成promise的resolved值。

例如，上面的代码返回resolved值为1的promise，我们可以测试一下：

```js
async function f() {
    return 1
}
f().then(alert) // 1
```

我们也可以显式的返回一个promise，这个将会是同样的结果：

```js
async function f() {
    return Promise.resolve(1)
}
f().then(alert) // 1
```

所以，`async`确保了函数返回一个promise，即使其中包含非promise。够简单了吧？但是不仅仅只是如此，还有另一个关键词`await`，只能在`async`函数里使用，同样，它也很cool。

### Await

语法如下：

```js
// 只能在async函数内部使用
let value = await promise
```

关键词`await`可以让JavaScript进行等待，直到一个promise执行并返回它的结果，JavaScript才会继续往下执行。

以下是一个promise在1s之后resolve的例子：

```js
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve('done!'), 1000)
    })
    let result = await promise // 直到promise返回一个resolve值（*）
    alert(result) // 'done!' 
}
f()
```

函数执行到（*）行会‘暂停’，当`promise`处理完成后重新恢复运行， `resolve`的值成了最终的`result`，所以上面的代码会在1s后输出`'done!'`

我们强调一下：`await`字面上使得JavaScript等待，直到`promise`处理完成，
然后将结果继续下去。这并不会花费任何的cpu资源，因为引擎能够同时做其他工作：执行其他脚本，处理事件等等。

这只是一个更优雅的得到`promise`值的语句，它比`promise`更加容易阅读和书写。

> **不能在常规函数里使用await**
> 如果我们试图在非async函数里使用await，就会出现一个语法错误：

 ```js
 function f() {
    let promise = Promise.resolve(1)
    let result = await promise // syntax error
 }
 ```
>
> 如果我们忘记了在函数之前放置async，我们就会得到这样一个错误。如上所述，await只能在async函数中工作。

让我们来看[promise链式操作](https://javascript.info/promise-chaining)一章中提到的`showAvatar()`例子，并用`async/await`重写它。

1.我们需要将`.then()`替换为`await`
2.此外，我们应该让函数变成`async`，这样`await`才能够工作

```js
async function showAvatar() {
    // read our JSON
    let response = await fetch('/article/promise-chaining/user.json')
    let user = await response.json()
    
    // read github user
    let githubResponse = await fetch(`https://api.github.com/users/${user.name}`)
    let githubUser = await githubResponse.json()
    
    // 展示头像
    let img = document.createElement('img')
    img.src = githubUser.avatar_url
    img.className = 'promise-avatar-example'
    documenmt.body.append(img)
    
    // 等待3s
    await new Promise((resolve, reject) => {
        setTimeout(resolve, 3000)
    })
    
    img.remove()
    
    return githubUser
}
showAvatar()
```

相当的简洁和易读，比以前的要好得多。

> **await不能工作在顶级作用域**
> 那些刚开始使用await的人们老是忘记这一点，那就是我们不能将await放在代码的顶层，那样是行不通的：
>
 ```js
 // 顶层代码处syntax error
 let response = await fetch('/article/promise-chaining/user.json')
 let user = await response.json()
 ```
>
> 所以我们需要将await代码包裹在一个async函数中，就像上面的例子一样。

------

> **await接受thenables**（好吧我这个渣渣并不知道thenables该如何翻译，有人能告知吗？）
>
> 就像promise.then，await也允许使用thenable对象（那些具有可调用的then方法的对象）。同样，第三方对象可能不是一个promise，但是promise的兼容性表示，如果它支持.then方法，那么它就能用于await。
>
> 例如，这里await接受了new Thenable(1)
>
 ```js
 class Thenable {
    constructor(num) {
        this.num = num
    }
    then(resolve, reject) {
        alert(resolve) // function() {native code}
        // 1000ms后将this.num*2作为resolve值
        setTimeout(()=> {resolve(this.num * 2), 1000})
    }
 }
 async function(f) {
    // 等待1s，result变为2
    let result = await new Thenable(1)
    alert(result)
 }
 f()
 ```

> 如果await得到了一个带有then方法的非promise对象，它将会调用提供原生函数resolve、reject作为参数的方法，然后await一直等待，直到他们其中的一个被调用（在上面的例子它发生在（*）行）。

------

> **async方法**
> 一个class方法同样能够使用async，只需要将async放在它之前就可以
> 就像这样：
>
 ```js
 class Waiter {
    async wait () {
        return await Promise.resolve(1)
    }
 }
 new Waiter().wait().then(alert) // 1
 ```
>
> 这里的意思是一样的：它确保了返回值是一个promise，支持await

### 错误处理

如果一个promise正常resolve，那么`await`返回这个结果，但是在reject的情况下会抛出一个错误，就好像在那一行有一个throw语句一样。

```js
async function f() {
    await Promise.reject(new Error('whoops!'))
}
```

和下面一样

```js
async function f() {
    throw new Error('Whoops!')
}   
```

在真实的使用场景中，promise在reject抛出错误之前可能需要一段时间，所以`await`将会等待，然后才抛出一个错误。
我们可以使用try-catch语句捕获错误，就像在正常抛出中处理异常一样：

```js
async function f() {
    try {
        let response = await fetch('http://no-such-url')
    } catch (err) {
        alet(err) // TypeError: failed to fetch
    }
}
f()
```

如果发生了一个错误，控制会跳转到catch块。当然我们也能够捕获多行语句：

```js
async function f() {
    try {
        let response = await fetch('/no-user-here')
        let user = await response.json()
    } catch(err) {
        // 在fetch和response.json中都能捕获错误
        alert(err)
    }
}
f()
```

如果我们不使用try-catch，然后async函数f()的调用产生的promise变成reject状态的话，我们可以添加.catch去处理它：

```js
async function f() {
    let response = await fetch('http://no-such-url')
}
// f()变成了一个rejected的promise
f().catch(alert) // TypeError: failed to fetch
```

如果我们忘记添加.catch，我们就会得到一个未被处理的promise错误（能够在控制台里看到它），这时我们可以通过使用一个全局的事件处理器去捕获错误，就像在[Promise链式操作](https://javascript.info/promise-chaining)一章讲的那样。

> `async/await`和`promise.then/catch`
>
> 当我们使用async/await，我们很少需要`.then`，因为`await`总是等待着我们，而且我们能够使用常规的`try-catch`而不是`.catch`，这通常（并不总是）更方便。
>
> 但是在代码的顶层，当我们在async函数的外部时，我们在语法上是不能使用`await`的，所以通常添加`.then/catch`去处理最终结果或者错误。

------

> **async/await能够与Promise.all友好的协作**
> 当我们需要等待多个promise时，我们可以将他们包装在Promise.all中然后使用await：
>
 ```javascript
 // 直到数组全部返回结果
 let results = await Promise.all([
    fetch(url1),
    fetch(url2),
    ...
 ])
 ```
>
> 如果发生了一个错误，它就像普通情况一样：从一个失败状态的promise到Promise.all，然后变成了一个我们能够使用try-cathc去捕获的异常。

## 总结

放在一个函数前的async有两个作用：
1.使函数总是返回一个promise
2.允许在这其中使用await

promise前面的await关键字能够使JavaScript等待，直到promise处理结束。然后：
1.如果它是一个错误，异常就产生了，就像在那个地方调用了throw error一样。
2.否则，它会返回一个结果，我们可以将它分配给一个值

他们一起提供了一个很好的框架来编写易于读写的异步代码。

有了async/await，我们很少需要写promise.then/catch，但是我们仍然不应该忘记它们是基于promise的，因为有些时候（例如在最外面的范围内）我们不得不使用这些方法。Promise.all也是一个非常棒的东西，它能够同时等待很多任务。


## 以下是另一种理解

### 异步功能

异步功能函数包含`async`关键词。你可以在正常的函数声明中使用它：

```js

    async function functionName (arguments) {
        // Do something asynchronous
    }
```

你也可以使用箭头函数。

```js
    const functionName = async (arguments) => {
        // Do something asynchronous
    }

```

异步函数总是返回`promises`

（异步函数）它不管你返回什么。其返回值都是`promise`。


```js
    const getOne = async _ => { 
    return 1 
    } 

    const promise = getOne()
    console.log(promise) // Promise 

```

### await关键字

当你调用promise时，你会在then中处理下一步，如下：

```js
    const getOne = async _ => { 
    return 1 
    } 

    getOne()
    .then(value => {
        console.log(value) // 1
    })

```

`await`关键字允许你等待`promise`去解析。一旦解析完`promise`，它就会返回参数传递给`then`调用。

```js
    const test = async _ => {
    const one = await getOne()
    console.log(one) // 1
    }

    test()

```

返回await

在返回承诺（promise）之前没有必要等待（await）。你可以直接退回承诺。


>如果你return await些内容，则你首先是解决了原先promise。然后，你从已经解析的内容（resolved value）创建新的promise。return await真的没做什么有效的东西。无需额外的步骤。

```js
    // Don't need to do this 
    const test = async _ => {
    return await getOne()
    }

    test()
    .then(value => {
        console.log(value) // 1
    })


    // Do this instead
    const test = async _ => {
    return getOne()
    }

    test()
    .then(value => {
        console.log(value) // 1
    })
```

>注意：如果你不需要await，则不需要使用异步功能（async function）。上面的例子可以改写如下:

```js
    // Do this instead
    const test = _ => {
    return getOne()
    }

    test()
    .then(value => {
        console.log(value) // 1
    })
```

处理错误

如果一个promise出错了，你可以使用catch调用来处理它，如下所示:

```js
    const getOne = async (success = true) => { 
    if (success) return 1
    throw new Error('Failure!')
    } 

    getOne(false)
    .catch(error => console.log(error)) // Failure!
```

如果你想在一个异步函数中处理错误，你需要调用`try/catch`。

```js
    const test = async _ => {
        try {
            const one = await getOne(false)
        } catch (error) {
            console.log(error) // Failure!
        }
    }

    test()
```

如果你有多个`await`关键字，错误处理可能变得很难看...

```js
    const test = async _ => {
        try {
            const one = await getOne(false)
        } catch (error) {
            console.log(error) // Failure!
        }

        try {
            const two = await getTwo(false)
        } catch (error) {
            console.log(error) // Failure!
        }

        try {
            const three = await getThree(false)
        } catch (error) {
            console.log(error) // Failure!
        }
    }

    test()

```


还有更好的方法。

我们知道异步函数总是返回一个`promise`。当我们调用`promise`时，我们可以在`catch`调用中处理错误。这意味着我们可以通过添加`.catch`来处理异步函数中的任何错误。


```js
    const test = async _ => {
    const one = await getOne(false)
    const two = await getTwo(false)
    const three = await getThree(false)
    }

    test()
    .catch(error => console.log(error)))
```

>注意：`Promise`的`catch`方法只允许你捕获一个错误。

多个awaits

`await`阻止`JavaScript`执行下一行代码，直到`promise`解析为止。这可能会导致代码执行速度减慢的意外效果。

为了实际演示这点，我们需要在解析`promise`之前创建一个延迟。我们可以使用`sleep`功能来创建延迟。

```js
    const sleep = ms => {
    return new Promise(resolve => setTimeout(resolve, ms))
    }
```

`ms`是解析前等待的毫秒数。如果你传入1000到`sleep`函数，`JavaScript`将等待一秒才能解析`promise`。

```js
    // Using Sleep
    console.log('Now')
    sleep(1000)
    .then(v => { 
        console.log('After one second') 
    })

```

![](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/36.gif)

假设 `getOne` 需要一秒来解析。为了创建这个延迟，我们将1000（一秒）传入到`sleep`。一秒过后，`sleeppromise`解析后，我们返回值1。

```js
 const getOne = _ => {
   return sleep(1000).then(v => 1)
 }
```

如果你使用`await getOne()`，你会发现在`getOne`解析之前需要一秒钟。

```js
    const test = async _ => {
    console.log('Now')

    const one = await getOne()
    console.log(one)
    }

    test()
```


![](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/37.gif)


现在，假设你需要处理三个promises。每个promise都有一秒钟的延迟。

```js
    const getOne = _ => {
        return sleep(1000).then(v => 1)
    }

    const getTwo = _ => {
        return sleep(1000).then(v => 2)
    }

    const getThree = _ => {
        return sleep(1000).then(v => 3)
    }
```

如果你连续`await`这三个`promises`，你将要等待三秒才能解析完所有`promises`。这并不好，因为我们强迫JavaScript在做我们需要做的事情之前等待了两秒钟。


```js
    const test = async _ => {
    const one = await getOne()
    console.log(one)

    const two = await getTwo()
    console.log(two)

    const three = await getThree()
    console.log(three)

    console.log('Done')
    }

    test()
```

![](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/38.gif)


如果`getOne`，`getTwo`和`getThree`可以同时获取，你将节省两秒钟。你可以使用`Promise.all`同时获取这三个`promises`。

有三个步骤：

>1、创建三个`promises`
>2、将三个`promises`添加到一个数组中
>3、使用`Promise.all`来`awaitpromises`数组


如下所示：

```js
    const test = async _ => {
    const promises = [getOne(), getTwo(), getThree()]
    console.log('Now')

    const [one, two, three] = await Promise.all(promises)
    console.log(one)
    console.log(two)
    console.log(three)

    console.log('Done')
    }

    test()

```


![](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/39.gif)

