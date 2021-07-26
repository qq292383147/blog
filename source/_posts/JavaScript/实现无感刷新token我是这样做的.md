---
title: 实现无感刷新token我是这样做的
date: 2021-07-26 12:41:20
tags: JavaScript
categories: JavaScript
---

## 前言

最近在做需求的时候,涉及到登录token,产品提出一个问题:能不能让token过期时间长一点，我频繁的要去登录。

前端：后端，你能不能把token 过期时间设置的长一点。

后端：可以,但是那样做不安全，你可以用更好的方法。

前端：什么方法?

后端：给你刷新token的接口，定时去刷新token

前端：好，让我思考一下

## 需求

当token过期的时候，刷新token,前端需要做到无感刷新token,即刷token时要做到用户无感知，避免频繁登录。实现思路

- 方法一

后端返回过期时间，前端判断token过期时间,去调用刷新token接口

缺点：需要后端额外提供一个token过期时间的字段；使用了本地时间判断，若本地时间被篡改，特别是本地时间比服务器时间慢时，拦截会失败。

- 方法二

写个定时器，定时刷新token接口

缺点：浪费资源,消耗性能,不建议采用。

- 方法三

在响应拦截器中拦截，判断token 返回过期后，调用刷新token接口

## 实现

axios的基本骨架,利用service.interceptors.response 进行拦截

```js
import axios from 'axios'

service.interceptors.response.use(
  response => {
    if (response.data.code === 409) {
        return refreshToken({ refreshToken: localStorage.getItem('refreshToken'), token: getToken() }).then(res => {
          const { token } = res.data
          setToken(token)
          response.headers.Authorization = `${token}`
        }).catch(err => {
          removeToken()
          router.push('/login')
          return Promise.reject(err)
        })
    }
    return response && response.data
  },
  (error) => {
    Message.error(error.response.data.msg)
    return Promise.reject(error)
  }
)
```

## 问题解决

### 问题一：如何防止多次刷新token

我们通过一个变量isRefreshing 去控制是否在刷新token的状态。

```js
import axios from 'axios'

service.interceptors.response.use(
  response => {
    if (response.data.code === 409) {
      if (!isRefreshing) {
        isRefreshing = true
        return refreshToken({ refreshToken: localStorage.getItem('refreshToken'), token: getToken() }).then(res => {
          const { token } = res.data
          setToken(token)
          response.headers.Authorization = `${token}`
        }).catch(err => {
          removeToken()
          router.push('/login')
          return Promise.reject(err)
        }).finally(() => {
          isRefreshing = false
        })
      }
    }
    return response && response.data
  },
  (error) => {
    Message.error(error.response.data.msg)
    return Promise.reject(error)
  }
)
```

### 问题二：同时发起两个或者两个以上的请求时，其他接口怎么解决

当第二个过期的请求进来，token正在刷新，我们先将这个请求存到一个数组队列中，想办法让这个请求处于等待中，一直等到刷新token后再逐个重试清空请求队列。那么如何做到让这个请求处于等待中呢？为了解决这个问题，我们得借助Promise。将请求存进队列中后，同时返回一个Promise，让这个Promise一直处于Pending状态（即不调用resolve），此时这个请求就会一直等啊等，只要我们不执行resolve，这个请求就会一直在等待。当刷新请求的接口返回来后，我们再调用resolve，逐个重试。最终代码：

```js
import axios from 'axios'

// 是否正在刷新的标记
let isRefreshing = false
//重试队列
let requests = []
service.interceptors.response.use(
  response => {
  //约定code 409 token 过期
    if (response.data.code === 409) {
      if (!isRefreshing) {
        isRefreshing = true
        //调用刷新token的接口
        return refreshToken({ refreshToken: localStorage.getItem('refreshToken'), token: getToken() }).then(res => {
          const { token } = res.data
          // 替换token
          setToken(token)
          response.headers.Authorization = `${token}`
        }).catch(err => {
        //跳到登录页
          removeToken()
          router.push('/login')
          return Promise.reject(err)
        }).finally(() => {
          isRefreshing = false
        })
      } else {
        // 返回未执行 resolve 的 Promise
        return new Promise(resolve => {
          // 用函数形式将 resolve 存入，等待刷新后再执行
          requests.push(token => {
            response.headers.Authorization = `${token}`
            resolve(service(response.config))
          })
        })
      }
    }
    return response && response.data
  },
  (error) => {
    Message.error(error.response.data.msg)
    return Promise.reject(error)
  }
)
```

