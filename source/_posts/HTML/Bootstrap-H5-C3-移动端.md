---
title: Bootstrap+H5+C3+移动端
date: 2019-03-23 14:49:51
tags: H5C3
categories: H5C3
---

## 内减模式



`box-sizing`: <font color="#99d02e">border-box</font>;

让盒子自动的计算内容的大小，以保障盒子的最终大小就是我们设定的高度

 

## 圆 角

 

`border-radius`: 左上 右上 右下 左下

 

## 过 渡

 

`transition`: <font color="#5cc4d8">all</font> 1s;

如果修改的属性比较多，可以使用all

但是如果修改的属性比较少，还是建议单独写属性的名字 - 效果会更高

 

`transition-property`: 指定要变换的属性

`transition-duration`: 过渡动画完成的时间

`transtion-timing-function`: 指定速度曲线

 

内置的速度曲线在短时间里面是没法区分

`transition-delay`: 延迟多少时间之后再进行过渡动画

 

当过渡动画结束的时候，会触发一个：`transitionend` 的事件

注意： 在注册事件的时候，不能使用 `on` 的方式，要是 `addEventListener` 的方式

 

## 渐 变

#### 线性渐变

`background-image`: <font color="#99d02e">linear-gradient</font>(方向, 多个颜色 [位置] );

 

#### 径向渐变

 

## 2d变换

transform

位移：translate（x，y）;

 

旋转：rotate（角度）;

正方向的角度：顺时针

 

## 缩 放

scale(x的倍数，y的倍数);

如果想放大： 给大于1的数字

如果想要缩小：给小于1的数字

 

## 变换中心点

`transfrom-origin`: 50% 50%;

`transfrom-origin`: x坐标 y坐标

 

## 动画的属性

定义动画：

@keyframes 动画的名称{

分段控制不同的样式即可

}	

 

Animation-name            ===>   设置动画的名称

animation-duration          ===>   设置动画执行所需的时间

animation-timing-function    ====>   设置速度曲线

animation-delay             ====>  设置动画的延迟

 

animation-iteration-count     ====>  动画可以设置执行的次数

Inifinite  无限次

 

## 设置动画的方向

#### Animation-direction:

 `normal`    正常对的从0%-100% 的执行

 `reverse`    反向，从100%-0%的执行

 `alternate`   正反向循环

 `alternate-reverse`  反正循环

还可以设置动画的模式

#### animation-fill-mode:

`forwards`:动画结束后，元素样式停留在100%的样式

`backwards`:在延迟等待的时间内，元素样式停留在0样式

`both`：同时设置了forwards和backwards两个属性值

 

## 暂 停

#### Animation-play-state

Running  继续

Paused   暂停

 

合写:`animation`: 动画的名字  持续时间  【速度曲线】 【延迟】 【次数】 【方向】 【模式】 【是否暂停】

 

## 3d 变换

 

### (1)位移

#### transform:

translateX / Y / Z

近大远小的效果

需要配合视距来完成

什么是视距？

`perspactive`: 距离

### (2)旋转

#### translate3d

`rotaeX()`   围绕X轴旋转

`rotateY()`   需要配合视距效果才明显

`rotateZ()`   根据 2d 是一样的


`rotate3d()`  `0-1`取值

 

## 缩 放

scaleX / Y / Z ()

必须是有厚度的元素，才可以在Z轴缩放

把元素形式立体效果之后    才有厚度

立体效果必备的属性：

`transform-style`:   <font color="#99d02e">perserve-3d</font>;

<font color="#5cc4d8">scale3d</font>(x, y, z);

所有的 `transform` 一起使用的时候，记得使用空格隔开即可

 

当我们把位移和旋转一起使用的时候，要注意：

最好先位移，在旋转

如果先旋转，旋转会导致元素自身的坐标系发生改变

 

## 什么是sass?

一种css的预处理技术，可以有效的提高 css 的书写效率


怎么用？

### 变量

1、 声明变量

### $变量名:值

Eg:   `$color`: red;

2、 使用变量

```css
div{

background-color: $color;

}
```

### 函 数

声明函数

```less
@mixin 函数名（参数）{

  //重复使用的css代码段

}

Eg:

@mixin bgColor ($color) {

     background-color: $color;

  }

调用函数：

@include  函数名(参数);

    div {

      @include bgColor(red);

    }
```

嵌套

```css
选择器1 {
	选择2 {
		选择器3 {

     	}
	}
}
```

保证选择与选择器之间前后代关系

 

引入：

>解决文件之间的依赖关系和一个页面中引入多个css文件的问提

 

@import 要引入的sass文件的路径;

 

## 注释：

```js
//  这种是不会编译到css文件里面的

/**/  如果希望把注释编译到css文件里面
```
 

## fullpage全屏插件

fullPage.js 是一个基于 jQuery 的插件，它能够帮你很方便、很轻松的制作出全屏网站。

github 官网 <https://github.com/alvarotrigo/fullPage.js> 

中文演示地址 <http://www.dowebok.com/demo/2014/77/> 

### 3.3.1. 引用文件

```html
<link rel="stylesheet" href="css/jquery.fullPage.css">

<script src="js/jquery.min.js"></script>

<script src="js/jquery.fullPage.js"></script>
```

 

### HTML 结构

```html
<div id="fullpage">

    <div class="section">第一屏</div>

    <div class="section">第二屏</div>

    <div class="section">

        <div class="slide">第三屏的第一屏</div>

        <div class="slide">第三屏的第二屏</div>

        <div class="slide">第三屏的第三屏</div>

        <div class="slide">第三屏的第四屏</div>

    </div>

    <div class="section">第四屏</div>

</div>
```

 

### JavaScript入口函数

```js
$(function(){

    $('#fullpage').fullpage();

});
```

 

### fullpage 详细参数

看Fullpage的插件文档

Css预处理器

1、less

2、sass

3、stylues

### sass 的文件后缀名是 scss!

sass 是技术的名称 scss 是 sass 文件的后缀名

### sass的执行过程

1、 编写符合 sass 语法的 scss 文件

2、 使用工具将 scss 文件编译成 css 文件

3、 页面中引用编译好的 css 文件

 

### sass语法

```scss
// 声明变量 $变量名:值;
$color:red;

// 使用变量
body{
  background: $color;
}
```

 

### 混合-函数

```less
// 声明函数 .函数名(@参数名)

@mixin changeColor($c){

  background-color: $c;

}

 

// 使用函数

body{

  @include changeColor(red);

}
```
 

### 导 入

```less
@import "xxx.scss";
```
 

 

### 嵌  套

```scss
#id{

  .c1{

    // 后代

    a{}

    // 子代

    >p{}

   // 伪元素

   &:before{}

  }

}
```

 

### 注 释

```js
// 不会被编译

/* 会被编译 */
```

 

弹性布局 操作方便 主要用于移动端

伸缩布局 = 弹性布局 = 伸缩盒子 = 弹性盒子 = flex布局

传统布局 兼容性好 但是繁琐

 

>1、 给父元素 div 设置 dislplay: flex;  即可将其变为弹性布局

>2、 子元素span 可以随意设置宽高不再受显示模式的限制（如行内 span 元素也可以设置宽高）

 

## 弹性布局

#### 父项属性

`display`: flex : 开启弹性布局，让子元素可以按照弹性布局的方式显示

 

> `flex-diretion`: 可以设置主轴的方向
> `row`	 默认-子项沿着主轴的小数字方向到大数字方向-主轴是 x 轴从左到右
> `row-reverse`	: 把主轴设置成 x 轴的负方向，从右到左
> `column`: 把 y 轴设置为主轴，从上到下
> `column-reverse`: 把 y 轴的负方向设置为主轴，从下到上

 

justify-content: 设置子项沿着主轴排列的方式

> `flex-start`:   侧轴的前端对齐
> `flex-end`:	 侧轴的末端对齐
> `center`:		 居中对齐
> `space-around`:平分对齐
> `space-between`:两端对齐

 

`flex-wrap`:     flex布局默认是不会换行的

`nowrap`   -----  默认不换行

`wrap`	  ------   让子项，一行上放不下的时候，可以换行

 

## 多 行

align-content	设置多行子项的排列方式-沿着侧轴排列

> `flex-start`    侧轴的前端对齐
> `flex-end`      侧轴的末端对齐
> `center`        居中对齐
> `space-around`  评分对齐
> `space-between` 两端对齐
 

## 单 行

align-items 设置单行子项在侧轴上的排列方式

> `flex-start`    侧轴的前端对齐
> `flex-end`      侧轴的末端对齐
> `center`        居中对齐

### 子项属性

align-self 设置某个子项自己的对齐方式

> `flex-start`    侧轴的前端对齐
> `flex-end`      侧轴的末端对齐
> `center`        居中对齐
> `space-around`  评分对齐
> `space-between` 两端对齐
> `flex`          设置子项占据父容器的主轴的比例

## 计算方式

把所有子项的flex的值加起来是n

就把父元素的宽度分成n份，每个子项按照他设定好的flex的值，获取响应的分数



order 设置子项的排列的顺序

order: 数字; 数字越小，就越在主轴的前方



## 详细理解flex的用法

父项：有6个属性是对父元素设置的

1、 `flex-direction` 设置主轴的方向

2、 `justify-conent` 设置主轴上的元素排列方式

3、 `flex-wrap` 设置子元素是否换行

4、 `align-conent` 设置侧轴上的子元素的排列方式（多行）

5、 `align-items` 设置侧轴上的子元素排列方式（单行）

6、 `flex-flow` 复合属性相同时设置了 flex-direction 和 flex-wrap

 

## flex-direction设置主轴的方向

1、 `flex-direction`: row;  row 就是默认值  --->  从左到右

2、 `flex-direction`: row-reverse; 从右到左

3、 `flex-direction`: column; 从上到下

 

## justify-conent设置主轴上的子元素排列方式

`justify-conent`: flex-start;   ------->  默认值

`Justify-conent`: flex-end;   从尾部开始排列

`justify-content`: center;  挤在一起居中

`justify-conent`: space-around;  平分剩余空间

`justify-content`: space-between; 先两边再平分剩余空间

 

 

## flex-wrap设置子元素是否换行

`flex-wrap`: no-wrap;  

`flex` 默认不换行

`flex-wrap`: wrap;   换行

 

 

#### align-content  设置侧轴上的子元素的排列方式（多行）

设置子项在侧轴上的排列方式并且只能用于子项出现换行的情况，在单行下是每页效果的！


`align-content`: flex-start;      在侧轴的头部开始排列

`align-conent`: flex-end;		 在侧轴的尾部开始排列

`align-content`: flex-center; 	 在侧轴中间显示

`align-content`: space-around;  子项在侧轴平分剩余空间

`align-content`: space-between：子项在侧轴先分布在两头，再平分剩余空间

`align-content`: stretch;		  设置子项元素高度平分父元素高度（当子项设了高度的时候 无效）

在 css 中先把子项的高度去掉

```less
/* 为了让 父项的align-content:stretch;有效 注释 子项的高度 */
/* height: 100px; */
```
 

在父项中加入

```less
/* 子项高度平分父元素的高度 */
 align-content: stretch;
```
 

#### align-items 设置侧轴上的元素排列方式（单行）

该属性是控制子项在侧轴（默认是y轴）上的排列方式，在子项为单项的时候使用

参数如下：

flex-start;

flex-end;

center;

stretch;

 

## Align-content 和 align-items 的区别

1、align-items 可以用于单行和多行，但是设置多行的参数每页 align-content 多

2、align-content 只能用于多行，不能用于单位

3、字母数少的事设置单行 align-items;字母数多的事设置多行 align-content

 

### 子项

 

align-self 控制子项自己在侧轴上的排列方式

注意：align-self 优先级比 align-items, align-content 高

 

参数跟 align-items 一样

 

order  设置子项之间的排列顺序

默认值都是0 谁的 order 值越小，谁就越靠前

 

flex 设置子项宽度占父元素宽度的比例

当子项指定了 width 时无效

 

## 计算方式

当设置子项的flex：1;  时    假如有n个子项，每一个子项的各占父元素的1/n

子项的宽度 = 父元素宽度 * （子项的flex/总的flex数）

↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓

>子项的宽度 = 父元素宽度 *（1 / n）

假设一共有3个子项，第一个子项设置 flex:2 其他都为 flex:1 

第一个子项的宽度应该是其他子项的两倍 

![img](https://qq292383147.github.io/pictureLibrary/picture/H5C3/1.jpg) 

 

## **弹性布局**

1、 子项可以直接设置宽度和高度

2、 子项不受浮动影响，但是受定位影响

3、 在移动端布局时，传统布局和弹性布局，哪种方便就使用哪种。

 

## 阴影

一种是盒子阴影，另一种是文字阴影

 

## 盒子阴影box-shadow

 

box-shadow: 盒子阴影  水平偏移 垂直偏移  模糊值 阴影外延值 内外阴影

 

1、 水平偏移      单位 px或者%

2、 垂直偏移     单位 px或者%

3、 模糊值  控制阴影的模糊程度，值越大越模糊 单位 px

4、 外延值 控制阴影向外延伸的值  单位px

5、 内外阴影  可以省略 省略值为 inset（内阴影）   outset|外阴影 

 

## 文本阴影 text-shadow

文字阴影 水平偏移 垂直偏移 模糊值 颜色

 

  

**HSLA:**

H： Hue(色调)。0(或360)表示红色，120表示绿色，240表示蓝色

S： Saturation(饱和度)。取值为：0.0% - 100.0%

L： Lightness(亮度)。取值为：0.0% - 100.0%

A： Alpha透明度。取值0~1之间。

`RGBA` 比 `RGB` 多了一个透明度 那么 RGBA 的效果 和 RGB + opacity 的效果 一样吗？

答案 ： 不一样

RGBA  中的透明度 只是背景透明 而内容不透明

而 opacity  会 把元素的所有都变成透明

 

背景就算了...去查百度....

### **backgorund-size**

(1) cover 等比放大到容器大小，直到最短边触底

(2) contain 等比放大到容器大小，直到最长边触底

 

### **字体图标**

1、 font-awesome 

2、 阿里巴巴

 

### **伪元素种类**

1、 E::before   在E元素前插入一个元素

2、 E::after  在E元素后插入一个元素

3、 E::first-letter 选择到了E容器内的第一个字母  

4、 E::first-line 选择到了E容器内的第一行文本

### **h5写法和传统写法区别**

 

1、 单冒号 E:before

2、 双冒号 E::before

 

 结论： 浏览器对以上写法都能识别 双冒号 是h5上语法的规范

 

## **语义化标签**

 header  头部标签

 nav 导航标签

 article 内容标签

 section 块级标签

 aside 侧边栏标签

 footer 尾部标签

 

### **4种操作class的方式**

1、 dom.classList.add('className') 添加

2、 dom.classList.remove('className') 移除

3、 dom.classList.toggle('className') 切换

4、 dom.classList.contains('className') 判断

 

### **h5自定义属性**

1 定义属性 data-

<div data-color='red'>div</div>

 

2 获取属性值 dom.dataset-*

​    var div=document.querySelector("div");

​    // 获取h5自定义属性  dataset是一个对象 里面的是h5自定义属性

​    var color=div.dataset.color; // red 

### **audio 音频标签**

```html
<audio src="小猪佩奇.mp3" autoplay> </audio>
```

 

目前只支持MP3、ogg、wav格式

 

### **video 视频标签**

```html
<video src="小猪佩奇.mp4" autoplay controls ></video>
```

目前只支持MP4、webM、ogg格式

 

video常用属性、方法、事件

 

Duration 视频播放时长		play播放   canplay视频加载完毕准备播放

currentTime当前播放进度	pause停止	  timeupdate播放时-持续触发

Volume 音量大小

 

## source标签

 

需知：可以通过在多媒体标签内加入**source**标签，用来指定多个播放路径，当第一个**source**标签的路径出错时，自动会切换到第二个**source**标签

 

object-fit属性

当**video**标签视频内容宽度没有铺满video标签时，可以在css写上 该属性即可

 

## 公共属性

Autoplay 如果出现该属性，则音频在就绪后马上播放。

 

controls 如果出现该属性，则向用户显示控件，比如播放按钮。

 

loop 如果出现该属性，则每当音频结束时重新开始播放。

 

muted 规定视频输出应该被静音。

 

preload 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。

 

src 要播放的音频的 URL。

 

获取 视频的长度 duration

 

var video=document.querySelector("video");

  
```js
  // 获取视频长度
  var duration=video.duration;
```
 

这些属性都很少用，在这里就不多说了，需要时可以去查

 

## **本地存储**

在h5中，本地存储有两个，一个是永久存储 localstorage和会话存储 sesstionStorage

 

localstorage 和sesstionStorage 两者的api都是一样的。 按照键值对的方式操作

 

setItem(key,val) 存入

```js
// 存入

  localStorage.setItem("movie","三毛流浪记");

 

getItem(key) 获取

// 获取

  var val=localStorage.getItem("movie")//  三毛流浪记

 

 

removeItem(key) 删除

 // 删除

  localStorage.removeItem("movie")  

  // 获取

  var val=localStorage.getItem("movie")//  为 undefined

  // 清空 

  localStorage.clear();
```
 

 

**当存入数据时，浏览器都会先调用该数据的 toString() 方法，因此**

 

**不管存入的是什么类型的数据，都会变成 字符串类型** 

 
```js
// 存入 bool 

  localStorage.setItem("test",true);

  var test=localStorage.getItem("test");

  console.log(typeof test);// string 类型

 

/*
  当存入复杂类型（数组，对象）时，需要先转为json字符串，再存入，否则数据丢失 

  使用 JSON.stringify 将对象转为json字符串

*/

// 复杂类型

  var obj={name:"小朱"}

  // 将对象转为json格式

  var jsonObj=JSON.stringify(obj);

  // 存入

  localStorage.setItem("test",jsonObj)

  // 类型是字符串

  console.log(typeof localStorage.getItem("test"));// string

  // 数据成功存入 

  console.log(localStorage.getItem("test"));// {"name":"小朱"}
```
 

那么取出数据的时候，当然也要解析字符串

使用 **JSON.parse** 将 json 字符串转为对象

 

 
```js
var obj={name:"小朱"}

  // 将对象转为json格式

  var jsonObj=JSON.stringify(obj);

  localStorage.setItem("test",jsonObj)

  // 取出数据

  var newJson=localStorage.getItem("test");

  // json转为对象

 var newObj=JSON.parse(newJson);

 console.log(typeof newObj);// object 类型 
```
 

### 拖拽事件

 

drogover 和 drop

允许拖拽 draggable= "true"

 
```js
  // 容器

  var div = document.querySelector("div");

  // 被拖拽元素

  var p = document.querySelector("p");

 

  // 1 当p标签出现在div上面的时候 触发

  div.ondragover = function (e) {

​  // 2 禁止浏览器默认行为 否则 无法触发 ondrop事件

​  e.preventDefault();

  }

  // 3 松开手指的时候触发

  div.ondrop = function () {

​  // 4 把p标签加入到div标签中

​  div.appendChild(p);

  }
```

#### **被拖拽的元素**

 dragstart 开始拖拽的时候

 drag 拖拽移动的时候

 dragleave 拖拽的时候 离开自身的范围

 dragend  拖拽松开手指的时候

 

#### **容器元素**

 ondragenter 被拖拽的元素进入舞台的时候

 ondragover 被拖拽的元素在舞台上移动的时候

 阻止浏览器默认事件 e.preventDefault

 ondragleave 被拖拽的元素离开舞台上的时候

 ondrop 被拖拽的元素在舞台上松开手指的时候

 e.dataTransfer.files 获取被拖拽的目标文件（图片-文件等）

 

## 地理位置 html5shiv.js

### 条件注释 （只为IE8兼容）

<!--[if IE 8]>用于 IE8 <![endif]-->

## css3兼容处理

 谷歌 -webkit

 火狐 -moz

 IE -ms

 
```less
  -webkit-border-radius: 30px 10px;

  -moz-border-radius: 30px 10px;

  -ms-border-radius: 30px 10px;

  // border-radius 一定要放在最后

  border-radius: 30px 10px;
```
 

 

## 移动WEB

 
Touch 事件中的 touches、targetTouches 和 changedTouches 详解

Touches：当前屏幕上所有触摸点的列表;

targetTouches：当前对象上所有触摸点的列表;

changedTouches：涉及当前（引发）事件的触摸点的列表;

可通过一个例子来区分触摸事件中的这三个属性：

1、用一个手指接触屏幕触发事件，此时这三个属性有相同的值。

2、用第二个手指接触屏幕时，此时，touches 有两个元素，每个手指触摸点为一个值，当两个手指触摸相同元素时，targetTouches 和 touches 值相同，否则 changedTouches 此时只有一个值，为第二个手指的触摸点，因为第二个是引发事件的原因。

3、用两个手指同时接触屏幕，此时 changedTouches 有两个值，每一个手指的触摸点都有一个值

4、手指滑动，三个值都会发生变化

5、一个手指离开屏幕，touches 和 targetTouches 中对应的元素会同时移除，而 changedTouches 依然会存在元素。

6、手指都离开屏幕后，touches 和 targetTouches 中将不会再有值，changedTouches 还会有一个值，此值为最后一个离开屏幕的手指的接触点

### 二、触点坐标获取

Touchstart 和 touchmove 使用：

e.targetTouches[0].pageX或者（jquery）

e.originalEvent.targetTouches[0].pageX

touchend 使用：e.targetTouches[0].pageX或（jquery）e.originalEvent.changedTouches[0].pageX


// touch事件：

// touchstart: 手指触摸开始--手指刚刚触摸到屏幕，一次触摸只会触发一次

// touchmove: 手指没有离开屏幕，同时在屏幕上滑动，它会持续的触发

// touchend: 手指离开屏幕瞬间触发，一次触发只会触发一次

// touchcancel: touch 意外中断


## 三、touchmove事件的获取

想要在touchmove:function(e, 参数一) {

var e = arguments[0];

e.preventDefault();

}
 

## 响应式布局

通过监听屏幕的宽度的变化，为元素添加不同的样式

如果是判断最小值，就从小到大进行判断

如果是判断最大值，就从大到小进行判断

向上兼容：如果为小屏幕添加了样式，这个样式在大屏幕下也有效

向下覆盖：如果为大屏幕下也设置了样式，那么在满足条件的情况下，大屏幕下面的样式会将小屏幕下面的样式覆盖

 

如果是IE浏览器，会调用最新的IE渲染模式进行页面的渲染

<meta http-equiv="X-UA-Compatible" content="IE=edge">



## viewport 配置

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```



注意：上述3个meta标签*必须放在最前面，任何其他内容都必须跟随其后！！

 

## Bootstrap：依赖于jquery

```html
<link href="./lib/bootstrap/css/bootstrap.css" rel="stylesheet">
```

 

## html5shiv

HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 IE8及以下不支持响应式和媒体查询，引入 html5shiv.min.js 是为了让 IE8 支持

 

## 添加媒体查询


```less
/* @media 媒体类型 条件

媒体类型：screen:    用于电脑屏幕，平板电脑，智能手机等

条件：使用and 连接，记得and 要添加空格*/

/* width: 监听视口大小的变化*/

/* device-width:监听当前设备的宽度的变化 */

 

@media screen and (min-device-width:768px) and (max-device-width:992px) {

   div {

     background-color: #0f0; 

     width:50%;

  }

}
```
 

## 移动端轮播图：插件（swiper.js）

 

```js
<script>

var mySwiper = new Swiper('.swiper-container', {

autoplay: 3000,

})

</script>

 

/*

swiper:  

1、常用于移动端网站的内容触摸滑动;

2、可以直接使用底部的圆点颜色切换

*/
```


属性的使用方法请去百度一下

 

## 移动端的滚动条（插件）：**iscroll.js**

 

```js
<script>

var myScroll = new IScroll('#wrapper', {

mouseWheel: true,

scrollbars: true

});

</script>
```

 

## 点透事件问题的解决：（使用插件：**fastclick.js**）

点透产生所需要的前提条件：

两个元素重叠，上面的元素添加touch事件，同时事件处理函数中将上面的元素隐藏，下面的元素添加click类似的pc端事件

点透的效果：响应上面元素的事件之后也会响应下面元素的事件

产生的原因：tap 事件优先触发，而click事件有300ms的延迟


```js
<script>

var click = document.querySelector('.click')

var tap = document.querySelector('.tap')

if ('addEventListener' in document) {

   document.addEventListener('DOMContentLoaded', function() {

   // document.body:说明document.body中所有元素都会使用fastclick来实现单击事件的触发

   FastClick.attach(document.body);

   }, false);

}

tap.addEventListener('click',function(){

   tap.style.visibility = 'hidden'

})

click.addEventListener('click',function(){

   console.log('click')

})

</script>

```


单击事件有什么特点：

1、 只能有一根手指触摸屏幕

2、 不能有滑动 - - 如果有滑动也只能指定的范围内

3、 手指松开和手指触摸的事件差异不能太长，一般行业规范在150ms-300ms（可以自定义）之内

 

布局容器:  container/container-fluid

一个栅格一列  /  内容row

 

栅格系统就是来描述设置当前子元素在制定屏幕下，占据当前屏幕默认12等分中的n(1-12)等分

 

1、 先添加容器 container/container-fluid w > 1200: large

2、 在容器中添加 row	w: 992~1200: md middle

3、 在row中添加子元素，设置栅格样式	    w:768~992 :sm small

4、 在子元素添加具体的内容	 w:768 : xs extra small

 

### Background-size 规定背景图像的尺寸：

 

Cover:  把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。背景图像的某些部分也许无法显示在背景定位区域中。（某一个方向包含）

Contain:  把图像扩展至最大尺寸，以使宽度和高度完全适应内容区域。（全包含）

 

公式的计算

1、设计的宽度(640) / 基础值 = 等宽的 媒体查询中的的html标签的fontsize的大小（100）= 要适配的屏幕的宽度 / 要计算的fontsize

 

2、设计的宽度(640) / 要适配的屏幕的宽度 = 基础值 / 要计算的fontsize的大小

3、要计算的fontsize的大小 = 基础值 * 要适配的屏幕的宽度 / 设计的宽度(640)

 

640 / 320 = 100 / 50

640 / 414 = 100 / ?

Fz = 100 * 414 / 640

 
```js
function setFont() {

// 要计算的fontsize的大小= 基础值 * 要适配的屏幕的宽度/ 设计稿的宽度 （640）

// 基础值 100px

var baseVal = 100;

// 设计稿的宽度 640px

var pageWidth = 640;

// 要适配的屏幕的宽度= 当前的屏幕的宽度

var screenWidth = document.querySelector("html").offsetWidth;

// 要设置的字体的大小

var fz = baseVal * screenWidth / pageWidth;

// 把字体的大小设置到 htm标签中

document.querySelector("html").style.fontSize = fz + "px";

}
```
 

 

 

 

### 单位rem

>px: 绝对长度单位 大小是固定 px 可以通过比例的转换 变成 cm mm dm

>em: 相对长度单位 相对于自身的 fontsize 的大小

>rem: 相对长度单位 相对于根元素 html 标签的 fontsize 的大小


## 字体fontsize

1、谷歌浏览器 默认的字体的大小16px  

2、谷歌浏览器 默认的最小字体是12px  假如font-size:1px；  即font-size:12px;

3、字体大小会继承


本地存储 cookie 4kb


存 	字符串	不是视频 图片

有2种本地存储

1、会话存储  sessionStroage

2、永久存储  localStorage

区别：

## 生命周期

1、会话存储  生命周期 关闭浏览器或者标签页之后就没有

2、永久存储  生命周期 除非手动删除 清除缓存，否则一直存在浏览器内部

共同点：

1、公共的api

① 设置添加seetItm(key,val)

1) 当存入数据的时候全部帮你转了类型 全部变成了字符串类型

2) 当存入一些复杂类型数组或者对象

3) 会导致数据丢失

4) 存之前，先把对象或者数组 转成json字符串的格式

​
```js
// 把对象转成json字符串

var jsonPerson=JSON.stringify(person);

sessionStorage.setItem("data",jsonPerson);

var strRetPerson=sessionStorage.getItem("data");
```
 

5) 获取之后，把json字符串重新解析成对象再去使用

```js
// 将json字符串重新解析成对象

var oldPerson=JSON.parse(strRetPerson);
```
 

② 获取getItem(key)

③ 删除一个removeItem(key)

④ 清空  clear();

 

2、容量大小  一般是5M 或者20M 具体看浏览器的版本

3、在同源的网站中 跨页面可以使用

① [www.baidu.com](http://www.baidu.com)

② [www.baidu.com/A.html](http://www.baidu.com/A.html)  在本地存储中存入了一些数据

③ [www.baidu.com/B.html](http://www.baidu.com/B.html)  本地存储 来获取在A中存储进去的数据

4、安全性
