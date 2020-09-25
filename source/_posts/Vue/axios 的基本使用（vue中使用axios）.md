---
title: axios 的基本使用（vue中使用axios）
date: 2020-06-27 11:38:15
tags: vue
categories: vue
---

axios就是一个基于Promise的，发送http请求的一个工具库。

#### 特点

1. 支持Promise API
2. 拦截请求和响应。拦截请求，可以过滤请求参数；拦截响应，可以处理响应异常
3. 取消请求。请求可以手动取消

#### vue中使用axios

1. 安装axios模块
    `npm install --save axios` 
2. 在index.js文件中引入axios

```js
import axios from 'axios'
new Vue({
  // el: '#app',
  // router,
  axios  // 加入axios
})
```

#### 基本API

##### 1.  执行get请求，有两种方式

```js
// 第一种方式  将参数直接写在url中
axios.get('/getMainInfo?id=123')
.then((res) => {
  console.log(res)
})
.catch((err) => {
  console.log(err)
})
// 第二种方式  将参数直接写在params中
axios.get('/getMainInfo', {
  params: {
    id: 123
  }
})
.then((res) => {
  console.log(res)
})
.catch((err) => {
  console.log(err)
})
```

##### 2. 执行post请求，注意执行post请求的入参，不需要写在params字段中，这个地方要注意与get请求的第二种方式进行区别。

```js
axios.post('/getMainInfo', {
  id: 123
})
.then((res) => {
  console.log(res)
})
.catch((err) => {
  console.log(err)
})
```

##### 3. 通过向axios传递的相关配置来创建请求`axios(config)` 

###### (1)下面是常用的配置字段：

- url：请求路径，**string类型** 
- method：请求方法，**string类型** 
- baseURL：baseURL会自动加在url前面，除非url是一个绝对URL，**string类型** 
- transformRequest：允许在向服务器发送请求之前，修改请求数据，只适用于**post，put，patch**请求，**数组类型，数组里面的最后一个函数必须返回一个字符串** 

```js
[fucntion(data) {
  // 对data进行更改
  return data
}]
```

- transformResponse：这里提前处理返回的数据
- headers：自定义请求头
- params：即将于请求一起发送的url参数（一般只用于get请求）**一般是对象类型** 
- data：作为请求主体被发送是数据（一般只用于post请求）**一般是对象类型** 
- timeout：超时时间，超过时间，请求将被中断
- withCredentials：表示跨域请求时是否需要使用凭证
- responseType：响应数据的类型，默认是'json'，可以是'text', 'json','document','arraybuffer','blob','stream'
- maxContentLength：响应数据的最大尺寸
- proxy：代理服务器主机名称和端口

```css
proxy: {
  host: '127.0.0.1',
  port: 9000,
  auth: : {
    username: 'mikeymike',
    password: 'rapunz3l'
  }
},
```

###### (2)下面是响应的数据接口

```kotlin
{
  data: // 服务器响应数据
  status: // http状态码
  statusText: // 服务器响应的http状态信息
  headers:  // 响应头
  config: // 请求配置数据
}
```

###### (3)举例

```jsx
// 发送 POST 请求
axios({
  method: 'post',
  url: '/getMainInfo',
  data: {
    id: 123
  }
}).then(res => {
  console.log(res.data)
  console.log(res.status)
  console.log(res.statusText)
  console.log(res.headers)
  console.log(res.config)
  
}).catch(err => {
  console.log(err)
})
```

##### 4. 配置默认值default

`axios.default.baseURL = ''`
 `axios.default.headers.common['Authorization'] = AUTH_TOKEN`
 ...等等默认配置

#### 5. 执行多个并发

`axios.all()`和Promise.all()执行机制是一样的，要么全部成功走then，要么就走catch

```jsx
function getUserName() {
  return axios.get('/getUseName?id=123')
}
function getUserAge() {
  return axios.get('getUserAge?id=123')
}
axios.all([getUserName(), getUserAge()]) .then(
  axios.spread(function(acct, perms) {  // 处理并发请求的助手函数
    console.log(acct, perms)  // 全部请求成功
  })).catch(err => {
  console.log(err)  // 只要任意一个请求出错
})
```

#### 6. 拦截器

##### (1)在请求之前拦截请求

```jsx
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  return config;
}, function (error) {
  // 对请求错误做些什么
  return Promise.reject(error);
})
```

##### (2)在被then，catch处理前拦截响应

```jsx
// 添加响应拦截器
axios.interceptors.response.use(function (response) {
  // 对响应数据做点什么
  return response;
}, function (error) {
  // 对响应错误做点什么
  return Promise.reject(error);
});
```

##### (3)可以为自定义 axios 实例添加拦截器

```jsx
var instance = axios.create([config]);
instance.interceptors.request.use(function () {/*...*/});
```

#### 7. 封装axios

在开发中，总会有很多的http请求，那我们就要封装好一个axios，使用更方便一些

##### (1)封装

```js
// request.js文件
import axios from 'axios'
import qs from 'qs'
// 引入基础参数文件  和  baseURL配置文件
import baseParams from './baseParams'  // 基本参数，比如一些登录信息之类的参数
import { BASE_URL } from './config'   // baseURL写在config.js文件中
// 默认的全局配置
axios.defaults.baseURL = BASE_URL
axios.defaults.timeout = 10000
// 请求发送之前拦截，进行处理（根据业务需求进行拦截处理）
axios.interceptors.request.use(success => {
  return success
}, error => {
  return reject(error)
})
// then,catch处理之前，进行拦截处理（根据业务需求进行拦截处理）
axios.interceptors.response.use(response => {
  return response
}, error => {
  return Promise.reject(error)
})
// 导出post请求
export function post (url, data, withBaseParams = false) {
  return new Promise((resolve, reject) => {
    axios({
      method: 'post',
      url,
      data: withBaseParams ? qs.stringify({...baseParams, data}) : qs.stringify(data),
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
      }
    })
      .then(res => successHandle(res, resolve))   // 将数据处理之后传给页面
      .catch(err => errorHandle(err, reject))
  })
}
// 导出get请求
export function get (url, params) {
  return new Promise((resolve, reject) => {
    axios({
      method: 'get',
      url,
      params,
      headers: {}
    })
      .then(res => successHandle(res, resolve))
      .catch(err => errorHandle(err, reject))
  })
}
// then处理执行了successHandle
function successHandle(data, resolve) {
  if (res.success && res.errorCode == '60000') {
    resolve(res)
  } else {
    // 弹出toast报错
    Toast({
      message: res.msg,
      duration: 2000
    })
  }
}
// catch处理执行了errorHandle
function errorHandle(err, reject) {
  reject(err)
}
```

##### (2)引入使用

```js
// 引入使用
import {get, post} from 'request.js'
post('/getMainInfo', {id: 123}, true)
.then(res => {
  console.log(res)
})
.catch(err => {
  console.log(err)  
})
```

