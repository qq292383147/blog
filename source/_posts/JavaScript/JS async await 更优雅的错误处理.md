---
title: JavaScript async/await 更优雅的错误处理
date: 2021-10-18 09:21:24
tags: JavaScript
categories: JavaScript
---

## 背景

团队来了新的小伙伴，发现我们的团队代码规范中，要给 `async await` 添加 `try...catch`。他感觉很疑惑，假如有很多个(不集中)，那不是要加很多个地方？那不是很不优雅？

## 为什么要错误处理

`JavaScript` 是一个单线程的语言，假如不加 `try ...catch` ，会导致直接报错无法继续执行。当然不意味着你代码中一定要用 `try...catch` 包住，使用 `try...catch` 意味着你知道这个位置代码很可能出现报错，所以你使用了 `try...catch` 进行捕获处理，并让程序继续执行。

我理解我们一般在执行 `async await` 的时候，一般运行在异步的场景下，这种场景一般不应该阻塞流程的进行，所以推荐使用了 `try...catch` 的处理。

## async await 更优雅的错误处理

但确实如那位同事所说，加 `try...catch` 并不是一个很优雅的行为。所以我 `Google` 了一下，发现 **How to write async await without try-catch blocks in Javascript**[1] 这篇文章中提到了一种更优雅的方法处理，并封装成了一个库——**await-to-js**[2]。这个库只有一个 `function`，我们完全可以将这个函数运用到我们的业务中，如下所示：

```js
/**
 * @param { Promise } promise
 * @param { Object= } errorExt - Additional Information you can pass to the err object
 * @return { Promise }
 */
export function to<T, U = Error> (
  promise: Promise<T>,
  errorExt?: object  // 可选参数
): Promise<[U, undefined] | [null, T]> {
  return promise
    .then<[null, T]>((data: T) => [null, data]) // 执行成功，返回数组第一项为 null。第二个是结果。
    .catch<[U, undefined]>((err: U) => {
      if (errorExt) {
        Object.assign(err, errorExt);
      }

      return [err, undefined]; // 执行失败，返回数组第一项为错误信息，第二项为 undefined
    });
}

export default to;
```

这里需要有一个前置的知识点：**await 是在等待一个 Promise 的返回值**。

正常情况下，`await` 命令后面是一个 `Promise` 对象，返回该对象的结果。如果不是 `Promise` 对象，就直接返回对应的值。

所以我们只需要利用 `Promise` 的特性，分别在 `promise.then` 和 `promise.catch` 中返回不同的数组，其中 `fulfilled` 的时候返回数组第一项为 `null`，第二个是结果。`rejected` 的时候，返回数组第一项为错误信息，第二项为 `undefined`。使用的时候，判断第一项是否为空，即可知道是否有错误，具体使用如下：

```js
import to from 'await-to-js';
// If you use CommonJS (i.e NodeJS environment), it should be:
// const to = require('await-to-js').default;

async function asyncTaskWithCb(cb) {
     let err, user, savedTask, notification;

     [ err, user ] = await to(UserModel.findById(1));
     if(!user) return cb('No user found');

     [ err, savedTask ] = await to(TaskModel({userId: user.id, name: 'Demo Task'}));
     if(err) return cb('Error occurred while saving task');

    if(user.notificationsEnabled) {
       [ err ] = await to(NotificationService.sendNotification(user.id, 'Task Created'));
       if(err) return cb('Error while sending notification');
    }

    if(savedTask.assignedUser.id !== user.id) {
       [ err, notification ] = await to(NotificationService.sendNotification(savedTask.assignedUser.id, 'Task was created for you'));
       if(err) return cb('Error while sending notification');
    }

    cb(null, savedTask);
}
```

## 小结

`async await` 中添加错误处理个人认为是有必要的，但方案不仅仅只有 `try...catch`。利用 `async await` 和 `Promise` 的特性，我们可以更加优雅的处理 async await 的错误。



### 参考资料

[1]How to write async await without try-catch blocks in Javascript: *https://blog.grossman.io/how-to-write-async-await-without-try-catch-blocks-in-javascript/*

[2]await-to-js: *https://github.com/scopsy/await-to-js*





> 注：可选参数 ==> 是指给方法的特定参数指定默认值，在调用方法时可以省略掉这些参数。
>
> ​	但是注意：
>
> ​		1、可选参数不能为参数列表的第1个参数，必须位于所有的必选参数之后（除非没有必选参数）；
>
> ​		2、可选参数必须指定一个默认值，且默认值必须是一个常量表达式，不能为变量；
>
> ​		3、所有可选参数以后的参数都必须是可选参数。

