---
title: css隐藏元素的几种方法中可以触发点击事件
date: 2021-07-29 11:49:22
tags: css
type: css
categories: css
---



是 `opacity` 设置为0的方法。



## css 隐藏元素的方式：



### 1、display:none;


```css
　　.box {
  　　display:none;
　　}
```


最简单也最粗暴的方法就是设置元素的 `display` 属性为 `none`。


设置为 `display:none;` 的元素将不会再占用页面空间，其占用的空间会被其他元素所占有，从而会引起浏览器的重排和重汇。



### 2、visibility:hidden


```css
　　.box {
  　　visibility:hidden;
　　}
```


>这种做法虽然能够隐藏元素，但是该元素仍会占用页面空间，因此只会导致浏览器的重汇而不会引起重排。



>如果希望元素隐藏后不会引起页面布局的变化，则推荐使用visibility:hidden;方式。



### 3、opacity:0;（filter:alpha(opacity=0);考虑兼容性两种都要写）

>设置元素透明度opacity属性为0，也可以隐藏页面元素。


```css
　　.box {
  　　opacity:0;
　　}
```
 

在呈现上与 `visibility:hidden;` 方式一样，同样会占据页面空间。



事件绑定差异性：



`display:none;`的元素会直接从页面上消失，因此在该元素上绑定的事件不会生效。



`visibility:hidden;` 的元素不会触发绑定的事件。



`opacity:0;` 的元素会触发绑定的事件，例如点击会触发 `click` 函数。
