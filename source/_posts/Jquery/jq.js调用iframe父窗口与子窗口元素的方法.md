---
title: jq.js调用iframe父窗口与子窗口元素的方法
date: 2021-07-29 11:40:57
tags: jQuery
type: jQuery
categories: jQuery
---

子页面获取父页面的 id=care 的子页面

```js
parent.care.location.reload();
```



父页面获取 id=imp 的子页面

```js
imp.location.reload();
```



1.jquery在 iframe 子页面获取父页面元素和方法代码如下:

```js
parent.$("selector");

parent.method();
```



2.jquery在父页面获取 iframe 子页面的元素和方法

代码如下:

```js
iframe.$("select");

iframe.method();
```

 

3.js在 iframe 子页面获取父页面元素代码如下:

```js
window.parent.document.getElementById("元素id");
```

 

4.js在父页面获取 iframe 子页面元素代码如下:

```js
window.frames["iframe_ID"].document.getElementById("元素id");
```



方法调用

父页面调用子页面方法：`FrameName.window.childMethod()`;

子页面调用父页面方法：`parent.window.parentMethod();`

 

DOM 元素访问

获取到页面的 `window.document` 对象后，即可访问 DOM 元素
