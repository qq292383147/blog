---
title: jQuery学习笔记
date: 2019-03-23 12:42:39
tags: jQuery
type: jQuery
categories: jQuery
---

先加载文件，把引用的文件的逻辑写在body外面，优化性能

使用CDN加速---子节点

Content Delivery Network 内容分发网络

使用CDN好处：性能提高，加快下载速度

$(xxx)  :返回jQuery对象

 

<center>$(domObject)--------jQuery Object</center>

<center>$(xxx).get(0)---------DOM Object</center>

<center>$(xxx)[0]---------DOM Object</center>

 

### **jQuery对象和DOM对象的相互转换**

**jQuery对象转换成DOM对象：**   

​	jQuery对象.get(索引值); 

​	jQuery对象[索引值] 

​        jQuery对象是包装集(集合)，从集合中取数据可以使用索引的方式

**DOM对象转换成jQuery对象：**   

​	$(DOM对象) 只有这一种方法;

 

什么是jQuery对象？

> 1.是原生DOM对象的封装
>
> 2.jQuery对象和原生DOM对象不同
>
> 3.jQuery对象包含了很多方法，方便的操作DOM元素

 

在jq中如何**注册事件**

Jq对象.事件名(处理程序);

 

在jq里面为了更加彻底的贯彻 write less,do more 思想

有一个编程技巧 **链式编程**

在jq里面，极大部分的函数的返回值都是调用该函数的对象，所以有对象之后就可以直接再次调用jq的方法，形成一个极长的函数调用的链 - 链式编程

 

 

  链式语法 chaining

  $('#divTest').text('hello,world!!')......

 

  $(document).ready(function(){   //处理加载文件等待的操作

​    ...

  })

 

  例如：window.onload = function(){  //jquery优化等待操作(加载文件)

​    console.log('onload');

  }

 

**内容筛选器：**

```js
:empty					//匹配所有不包含子元素或者文本的空元素

<table>

  <tr>

	<td>Value 1</td>

	<td></td>

</tr>

  <tr>

	<td>Value 2</td>

	<td></td>

</tr>

</table>


$("td:empty")
 

[ <td></td>,<td></td> ]

:contains(text)			//匹配包含给定文本的元素

<div>John Resig</div>

<div>George Martin</div>

<div>Malcom John Sinclair</div>

<div>J. Ohn

$("div:contains('John')")


[ <div>John Resig</div>, <div>Malcom John Sinclair</div> ]

```


:has(selector)			//匹配含有选择器所匹配的元素的元素

```js
<div><p>Hello</p></div>

<div>Hello again!</div>

$("div:has(p)").addClass("test");

[ <div class="test"><p>Hello</p></div> ]

 

:parent  				//获取父元素，匹配含有子元素或者文本的元素

<table>

  <tr><td>Value 1</td><td></td></tr>

  <tr><td>Value 2</td><td></td></tr>

</table>

$("td:parent")

[ <td>Value 1</td>, <td>Value 2</td> ]
```

 

其他筛选器：

:lang(language)   //选择指定语言的所有元素

 

:hidden   //匹配所有不可见元素，或者type为hidden元素

查找隐藏的 tr

##### HTML 代码:

```html
<table>

  <tr style="display:none"><td>Value 1</td></tr>

  <tr><td>Value 2</td></tr>

</table>

```



##### jQuery 代码:

```js
$("tr:hidden")
```



##### 结果:

```html
[ <tr style="display:none"><td>Value 1</td></tr> ]
```

 

:not(selector)  //去掉所有与给定选择器匹配的元素

查找所有未选中的 input 元素

##### HTML 代码:

```html
<input name="apple" />

<input name="flower" checked="checked" />
```



##### jQuery 代码:

```js
$("input:not(:checked)")
```



##### 结果:

```html
[ <input name="apple" /> ]
```

 

:visible		//匹配所有的可见元素

查找所有可见的 tr 元素

##### HTML 代码:

```html
<table>

  <tr style="display:none"><td>Value 1</td></tr>

  <tr><td>Value 2</td></tr>

</table>

```



##### jQuery 代码:

```js
$("tr:visible")
```



##### 结果:

```html
[ <tr><td>Value 2</td></tr> ]
```

:root   //选择该文档的根元素。

设置`<html>`背景颜色为黄色 

```js
$(":root").css("background-color","yellow");
```

 

:header  //匹配如 h1, h2, h3之类的标题元素

##### HTML 代码:

```html
<h1>Header 1</h1>

<p>Contents 1</p>

<h2>Header 2</h2>

<p>Contents 2</p>

```



##### jQuery 代码:

```js
$(":header").css("background", "#EEE");
```



##### 结果:

```html
[ <h1 style="background:#EEE;">Header 1</h1>, <h2 style="background:#EEE;">Header 2</h2> ]
```

 

:target		 //选择由文档URI的格式化识别码表示的目标元素。

```js
$("p, button, h1, h2").click(function(event){
  $("div").html("Triggered by a " + event.target.nodeName + " element.");
});
```

 

:animated   //匹配所有正在执行动画效果的元素

只有对不在执行动画效果的元素执行一个动画特效

##### HTML 代码:

```html
<button id="run">Run</button><div></div>
```



##### jQuery 代码:

```js
$("#run").click(function(){

  $("div:not(:animated)").animate({ left: "+=20" }, 1000);

});
```

 

 

隔行变色：

li:odd		--得到满足selector的元素里面索引为奇数的部分

li:even		--得到满足selector的元素里面索引为偶数的部分

 

在jq里面如何获取获取样式的当前值

jq对象.css(属性名);

 

 

### 一.js对象和jquery对象的区别

   jquery对象是js中new Object生成的普通对象

 

### 二.js对象和jQuery对象中的方法不能共用！

 

### 三.jqeury对象和js对象的相互转换

### ​    1.jquery对象转js对象  

​1.1） `$(obj).get(i)`

`get([index])`

取得其中一个匹配的元素。 num 表示取得第几个匹配的元素。

这能够让你选择一个实际的 DOM 元素并且对他直接操作，而不是通过 jQuery 函数。`$(this).get(0)`与`$(this)[0]` 等价。

##### HTML 代码:

```html
<img src="test1.jpg"/> <img src="test2.jpg"/>
```




##### jQuery 代码:

```js
$("img").get(0);
```



##### 结果:

```html
[ <img src="test1.jpg"/> ]

```

1.2） `$(obj)[i]`

### 2.js对象转jQuery对象

```js
    var obj = document.getElmentById('id');
    $(obj);
```

### 四.核心方法：

1. `click([[data],fn])` ——鼠标点击事件函数

2. `hover()` ——鼠标移入移出函数

3. `each()` 方法——循环遍历

​	例：为每个 h1 添加 num 属性，值为数字索引。

```js
​	$('h1').each(function(i){

​		$('h1').get()[i].setAttribute('num',i+1);

​	})

```

4. `index()` 方法返回指定元素相对于其他指定元素的 index 位置。

例 

```js
  var idx = $(this).index('.menu li');
```


在 jq 里面可以得到某个元素在其集合里面的索引

`$(元素).index()`    得到的是元素在它的兄弟元素里面的索引

jq对象.index(元素); 相当于 indexOf


5. `mouseenter()` 当鼠标指针进入（穿过）元素时

    `mouseleave()` 当鼠标指针离开元素时

​例：

```js
$('.menu li').mouseenter(function(){}

```

6. `not()` 选中所有不包含的元素

​    例：选中div中除了p标签的其他标签
```js
​   $('div').not('p');
```

特性 `attributes`：值为 `string`

属性 properties：值为string\boolean\number\object

1.如果 `attributes` 是本来在 DOM 对象中就存在的，`attributes` 和 `properties` 的值会同步

2.如果 `attributes` 是本来在 DOM 对象中就存在的，但是类型为 `boolean`，那么 `attributes` 和 `properties` 的值不会同步

3.如果 `attributes` 不是 DOM 独享内建的属性，`attributes` 和 `properties` 的值不会同步



#### 操作元素的特性：

1.获取特性的值：`attr(name)`

2.设置特性的值：`attr(name,value) attr(attributes)`

3.删除特性：`removeAttr(name)`



#### 操作元素的属性：

1.获取属性的值：`prop(name)`

2.设置属性的值：`prop(name,value) prop(properties)`

3.删除属性：`removerProp(name)`


#### 在元素中存取数据

获取数据的值：`data([name])`

设置数据的值：`data(name,value) data(object)`

删除数据：`removeData([name])`

判断是否有数据：`jQuery.hasData(element)`



#### 添加或修改 class

addClass(names)

removeClass(names)

hasClass(name)

toggleClass(names][,switch])   switch 是否切换



```js
//延迟一秒筛选（挺有意思的,用的比较少）

setTimeout(function(){

  //在chrome、Firefox等浏览器中，获取url hash会延迟一会儿，所以直接document ready中获取会获取不到

  console.log($(':target').addClass('highlight'))

},1000);
```



```html
<button id="run">Run</button>

<div class="box"></div>

<div id="mover" class="box"></div>

<div class="box"></div>
```



```js
$(function(){

  $("#run").click(function(){

    //animated是对动画添加效果

    $("div:animated").toggleClass("colored");

  });

  function animateIt(){

    $("#mover").slideToggle("slow",animateIt);

  }
  animateIt();

})
```

 

## 动  画

- 显示(show)与隐藏(hide)是一组动画：

- **滑入**(slideUp)与**滑出**(slideDown)与**切换**(slideToggle)，效果与卷帘门类似

- **淡入**(fadeIn)与**淡出**(fadeOut)与**切换**(fadeToggle)



`slideUp`、`fadeIn`、`show`   显示

`slideDown`、`fadeOut`、`hide`    隐藏

 

语法：元素.动画(动画时间);

**Bug:有延迟的效果**

**动画队列与停止动画**

在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会被放到动画队列中，等前面的动画执行完成了才会执行（联想：火车进站）

 

<span class="greenTextColor">// stop方法：停止动画效果</span>

jq对象.stop(clearQueue, jumpToEnd);

<span class="greenTextColor">// 第一个参数：是否清除队列 `boolean` 类型</span>

<span class="greenTextColor">// 第二个参数：是否跳转到最终效果 `boolean` 类型</span>

<span class="greenTextColor">// 清空队列：后面的动画不执行了</span>

<span class="greenTextColor">// 跳到结尾：立刻到达目标效果</span>

 

jq对象.animate({目标键值对},speed,ease,fn);

jq对象.animate({css属性的键值对},动画的持续时间,速度曲线,动画结束的回调函数);



jQuery
    就是一个js文件，里面封装了很多到达函数

$()---$ 在jq里面称为： 顶级对象 $ === jQuery

怎么用：
    引入、入口函数、自己写代码

### api

选择器
$(css选择器); 基本选择器

$(li:odd)

$(li:even)

$(li:eq(索引))

$(selector).parent()  获取父元素

$(selector).children()  获取子元素

$(selector).siblings()  获取除了自己以外的所有兄弟元素

$(selector).eq(索引)  获取集合里面的指定索引的元素

获取索引

$(元素).index() 获取元素在它的兄弟元素之间的索引

$(selector).index(元素);获取元素在集合里面的索引

注册事件

jq对象.事件名称(事件处理程序);

操作样式

css

设置

jq对象.css(属性名,属性值);

jq对象.css({
属性名:属性值
属性名:属性值
属性名:属性值
});

获取

jq对象.css(属性名);

addClass

removeClass

toggleClass

hasClass

动画函数

animate

jq对象.animate({目标键值对},speed,ease,fn);

`show()`/`hide()`/`toggle()`

`fadeIn()`/`fadeOut()`/`fadeToggle()`
`fadeTo()`

`slideDown()`/`slideUp()`/`slideToggle()`





  需要获取滚动出去的距离：

  scrollTop()   垂直

  jq对象.scrollTop();

  scrollLeft();  水平的

  这两个方法，除了可以获取之外，还可以设置

  使用获取宽度和高度的快速的方式

  jq对象.width();

  jq对象.height();

  也是可以获取和可以设置的

  在jq中，封装了好多获取宽高的方式：

  `innerWidth`/`innerHeight`            得到的是 content + padding

  `outWidth`/`outerHeight`             content + padding + border

  `outWidth(true)`/`outerHeight(true) ` content + padding + border + margin

```js
  $(function(){
       $('input').click(function(){
           // 回到顶部： 滚动出去的距离是0
           $(window).scrollTop(0);
       });
  
     var b = $("#box");
     console.log(b.width());   //只是内容的宽度
     console.log(b.innerWidth()); // 包含了内容和padding
     console.log(b.outerWidth()); // 包含内容、padding、border
     console.log(b.outerWidth(true)); // 包含了内容宁、padding、border、margin
   });

```



#### 节点操作

##### 增

创建

`$('<标签名></标签名>');`

`html('<div></div>');`

追加

appendappendTo

prepend prependTo

beforeafter

##### 删

remove()

empty()

html('')

##### 改

改属性 
  
  `attr`: 操作非开关属性

  `prop`: 操作开关属性
 
  jq对象.attr(属性名,属性值)

改样式

   css:

`addClass`/`removeClass`/`toggleClass`


改内容

`val()`/`text()`/`html()`


  jq对象.val();

  jq对象.text(内容)

##### 查

选择器

滚动

获取和设置滚动出去的距离


scrollTop()   垂直

scrollLeft()  水平

位置

`offset()`: 得到的是元素距离页面的左上角的位移
 
`position`
    得到的是元素距离他的 `offsetParent` 的位移

大小

`width`/`height`  内容的大小

`innerWidth`/`innerHeight` 内容 + padding

`outerWidth`/`outerHeight` 内容 + padding + border

`outerWidth(true)`/`outerHeight(true)` 内容 + padding + border + margin

----------------------------------------------

## jQuery 选择器的性能优化

1.尽量使用css中有的选择器

2.避免过度约束

3.尽量以ID开头

4.让选择器的右边有更多特征

5.避免使用全局选择器

6.缓存选择器结果



### jQuery 事件


#### 筛  选


**1.过滤**

### eq()

其实在jq里面可以直接根据索引得到jq对象

jq对象.eq(索引)

$(jq对象[索引])

### first()

### last()

### not()

### slice() 之间的会被选中

 

## 2.查  找

1. children()  查找子元素

2. find()      查找后代元素

3. next()      查找下一个元素

4. nextAll()   查找下一个全部元素

5. parent()    查找上一级元素

6. prev()      查找父元素

7. prevAll()   查找上一级元素的所有元素

8. siblings()  查找前后所有元素（兄弟元素）


## 3.串 联

`add()`  在标签上追加元素

`andSelf()`  找到下一个标签然后追加样式到自己和下一个元素



选择器和筛选器的区别：

当 parent 不能使用 `+` 号连接 `this` 对象时，我们就使用筛选选择器：

```js
$(this).children('h1').css({"color","#00f"});
```



## 属 性

1.属性

```js
attr();  //设置值 可以设置多个值

attr({});  //获取值
```

例：

```js
$('img').click(function(){

    alert($(this).attr('src'));
 });   //得到完整的图片属性值
```

 

## 2.css类

`addClass()`;     //追加一个 css 类为 class

例：

```js
$('img').mouseenter(function(){

    $(this).addClass('img');

});
$('img').mouseleave(function(){

    $(this).removeClass('img');

});

removeClass();  //删除

toggleClass();  //切换类(色即是空，空即是色)

```



## 3.HTML代码

html();  元素里面所有的内容，取值

html(val); 赋值，然后复制内容到另一个元素

 

## 4.文本

text();  <span class="greenTextColor">//get 的意思</span>

text(val);  <span class="greenTextColor">//set 的意思</span>

 

## 5.值

val();    <span class="greenTextColor">
//get 的意思</span>

val(val); <span class="greenTextColor">
//set 的意思</span>



#### 文档处理：

##### 1.内部插入（节点操作）

append()  <span class="greenTextColor">//后追加插入</span>

appendTo() <span class="greenTextColor">//后追加插入</span>

prepend()  <span class="greenTextColor">//前追加插入</span>

propengTo()  <span class="greenTextColor">//前追加插入</span>

 

##### 2.外部插入

after() <span class="greenTextColor">//用来插在每个匹配元素的后面</span>

before() <span class="greenTextColor">//在匹配元素的前面插入内容</span>

insertAfter() <span class="greenTextColor">//在目标元素后面插入集合中每个匹配的元素</span>

insertBefore() <span class="greenTextColor">//在目标元素前面插入集合中每个匹配的元素</span>

 

##### 3.包围

wrap() <span class="greenTextColor">//在每个匹配的元素外层包上一个 html 元素</span>

wrapInner()  <span class="greenTextColor">//在匹配元素里的内容外包一层结构</span>

wrapAll()  <span class="greenTextColor">//在所有匹配元素外面包一层HTML结构</span>

##### 4.替换

replaceWith() <span class="greenTextColor">//用提供的内容替换集合中所有匹配的元素并且返回被删除元素的集合</span>

replaceAll() <span class="greenTextColor">//用集合的匹配元素替换每个目标元素</span>

 

##### 5.删除

empty() <span class="greenTextColor">//从 DOM 中移除集合中匹配元素的所有子节点</span>

remove() <span class="greenTextColor">//将匹配元素集合从 DOM 中删除</span>

detach() <span class="greenTextColor">//从DOM中去掉所有匹配的元素(带事件)</span>

 

##### 6.复制

clone() <span class="greenTextColor">//创建一个匹配的元素集合的深度拷贝副本</span>

clone(true) <span class="greenTextColor">//一个 `Boolean` 值，表示是否会复制元素上的事件处理函数</span>

 

## css处理

### 1.css样式

```css
jq对象.css(属性名，属性值);

Jq对象.css({

属性名：属性值

属性名：属性值

属性名：属性值

});
```

获取：

```js
jq对象.css(属性名);

cass({})
```

 

### **jq里面获取和修改样式**

jq对象.css()

获取样式

jq对象.css(属性名);

设置样式

jq对象.css(属性名,属性值);

 

说明：

如果是获取样式，获取的是最终作用在元素身上的样式

如果是设置样式，修改的是行内样式

 

### 2.位置

offset() <span class="greenTextColor">//在匹配的元素集合中，获取的第一个元素的当前坐标，或设置每一个元素的坐标，坐标相对于文档</span>

position() <span class="greenTextColor">//获取匹配元素中第一个元素的当前坐标，相对于offset parent的坐标</span>

scrollTop(val) <span class="greenTextColor">//获取匹配的元素集合中第一个元素的当前垂直滚动条的位置或设置每个匹配元素的垂直滚动条位置</span>

 

### 3.尺寸

height() <span class="greenTextColor">//获取匹配元素集合中的第一个元素的当前计算高度值或设置每一个匹配元素的高度值</span>

width()  <span class="greenTextColor">//为匹配的元素集合中获取第一个元素的当前计算宽度值或给每个匹配的元素设置宽度</span>

innerHeight() <span class="greenTextColor">//为匹配的元素集合中获取第一个元素的当前计算高度值,包括padding，但是不包括border</span>

innerWidth() <span class="greenTextColor">//为匹配的元素集合中获取第一个元素的当前计算宽度值,包括padding，但是不包括border</span>

outerHeight() <span class="greenTextColor">//获取元素集合中第一个元素的当前计算高度值,包括padding，border和选择性的margin。返回一个整数（不包含“px”）表示的值  ，或如果在一个空集合上调用该方法，则会返回 null</span>

outerWidth() <span class="greenTextColor">//获取元素集合中第一个元素的当前计算宽度值,包括padding，border和选择性的margin。（愚人码头注：返回一个整数（不包含“px”）表示的值，或如果在一个空集合上调用该方法，则会返回 null。）</span>

<center class="centerEnd">~end~</center>