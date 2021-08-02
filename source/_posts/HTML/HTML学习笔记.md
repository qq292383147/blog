---
title: HTML学习笔记
date: 2019-03-22 22:15:21
tags: HTML
type: html
categories: html
---

***属性选择器： E：元素  att：属性  val：值***

> 1.  E[attr] ：这个元素存在attr这个属性即可被选中
> 2.  E[attr = val]  表示E这个元素中的attr属性的值是val才能被选中
> 3.  E[attr^=val]  表示E这个元素的attr属性的值中是以val开头的
> 4.  E[attr$=val]  表示E这个元素的attr属性的值是以val结尾的
> 5.  E[attr*=val]   表示E这个元素的attr属性的值中存在val即可

类和id的命名规则：

> 1.  可以包含有数字，字母，下划线，短横线
> 2.  不能以数字开头
> 3.  不能以短横线+数字开头
> 4.  不能使用单个短横线

建议：

> 1.  命名尽可能给有意义
> 2.  驼峰命名法

结构伪类选择器：

> :first-child  	       表示选择第一个孩子
> :last-child  	       表示选择最后一个孩子
> :nth-child(n)  	       表示要选择的元素的是第几个孩子元素 从前往后算
> :nth-last-child(n)     表示要选择的元素的是第几个孩子元素 从后往前算

目标伪类选择器：

```css
:target  {
    属性:属性值;
}
```

**块级元素**：<font color="#EE1289" size=3 face="Comic Sans MS">display</font>：<font color="#3A5FCD" size=3 face="Comic Sans MS">block</font>

> 特点：<font color="#FFFFE0" size=3 face="楷体">1.独占一行</font>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#FFFFE0" size=3 face="楷体">2.可以设置有效宽高</font><br><br>
>
> 常见的块级元素：P h1-h6 ul li....(div)

**行内块级元素**：<font color="#EE1289" size=3 face="Comic Sans MS">display</font>：<font color="#3A5FCD" size=4 face="Comic Sans MS">inline-block</font>

> 特点：<font color="#FFFFE0" size=3 face="楷体">1.一行可以显示多个</font>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#FFFFE0" size=3 face="楷体">2.可以设置有效宽高</font><br><br>
>
> 常见行内块级元素：input img select

**行内元素**（<font color="#EE1289" size=4 face="Comic Sans MS">display</font>:<font color="#3A5FCD" size=3 face="Comic Sans MS">inline</font>）的特点：

>    <font color="#FFFFE0" size=3 face="楷体">1.   一行可以显示多个</font><br>
>
>    <font color="#FFFFE0" size=3 face="楷体">2.   大小由内容决定</font><br>
>
>    <font color="#FFFFE0" size=3 face="楷体">3.   不能设置有效宽高</font><br><br>
>
> 常见的行内元素：span a strong em ins del....

> <font color="#FF3030" size=3 face="楷体">*注意：一般不将行内块级元素转换成行内元素
> 对于块级元素和行内块级元素设置文本内容水平居中，直接在元素本身上text-align属性
> 但是对于行内元素，要设置文本水平居中，我们需要给其父元素设置text-align属性*</font>

##### 上间距、下间距默认2.5px

##### span{内容$}*5

行高：line-weight  一行的高度
行高：文字的大小+上间距+下间距  
css中定义行高：两条基线之间的距离

#### 注意：盒子高度=行高 盒子中的单行的文本内容垂直居中

## CSS三大特性

1.CSS层叠样式 {同一个元素的同一个属性后面的样式会覆盖前面的样式，优先级高的会覆盖优先级低的}
2.CSS继承性 {子元素获得父元素的样式}

注意：
> 1. <font color="#EEEE00" size=3 face="楷体">a标签</font>不继承颜色 
> 2. <font color="#EEEE00" size=3 face="楷体">h系列标签</font>不能继承font-size和font-weight
> 3. CSS优先级 { 继承 <font color="#00F5FF" size=4 face="楷体"><</font> 通配符选择器 <font color="#00F5FF" size=4 face="楷体"><</font> 标签选择器 <font color="#00F5FF" size=4 face="楷体"><</font> 类选择器 <font color="#00F5FF" size=4 face="楷体"><</font> id选择器 <font color="#00F5FF" size=4 face="楷体"><</font> 行内选择器 <font color="#00F5FF" size=4 face="楷体"><</font> <font color="#FF3030" size=3 face="Comic Sans MS">!important;</font>}
>
><font color="#FF3030" size=3 face="Comic Sans MS">注意：important;只能针对一个属性，而不能提高整个选择器的优先级</font>

优先级只针对基本选择器，复合选择器叫权重计算！！
权重计算：4个N算法（n n n n）
从左边开始：
>第一个n表示<font color="#EEEE00" size=3 face="楷体">important</font>的个数
>第二个表示<font color="#EEEE00" size=3 face="楷体">id选择器</font>的个数
>第三个表示<font color="#EEEE00" size=3 face="楷体">类选择器</font>的个数
>第四个表示<font color="#EEEE00" size=3 face="楷体">标签选择器</font>的个数
比较的时候：从左边开始，先比较第一个n的大小，如果第一个n大，那么就是n大的这个选择器的权重高，后面的n都不需要再比较，如果一个n相等，那么比较第二个n，如果第二个n大，那么就是n大的这个选择器的权重高，那么就使用这个选择器的样式，以此类推...
如果比较完后，4个n的大小相同，那么就考虑css的层叠性。
第一个n的值，它是表示important的个数，而important只能提升一个属性的权重，不能提升整个选择器。
<center><font color="#FF3030" size=3 face="楷体">注意：继承的权重几乎为0，可以忽略</font></center>
<font color="#EE1289" size=4 face="Comic Sans MS">background-position</font>可以设置的值：(背景位置)
1.可以设置表示方位的单词：上中下 左中右
                          {水平} {垂直}
2.一个表示方式单词的时候：设置的值就是你表示方位，另一个方位默认居中

第一种方式直接将图片设置给body
第二种方式：在页面中添加一个div盒子
背景图片不占位置

<font color="#EE1289" size=4 face="Comic Sans MS">background-repeat</font> : <font color="#3A5FCD" size=4 face="Comic Sans MS">no-repeat</font>; //背景不平铺
<font color="#EE1289" size=4 face="Comic Sans MS">baceground-attachment</font> : <font color="#3A5FCD" size=4 face="Comic Sans MS">fixed</font>; scroll：滚动  fixed：固定 （有浮动的效果）
<font color="#EE1289" size=4 face="Comic Sans MS">background</font>：<font color="#3A5FCD" size=4 face="Comic Sans MS">background-image background-repeat background-position</font>
背景简写的时候 <font color="#EE1289" size=4 face="Comic Sans MS">background-image</font>一定要写，其他随意
<font color="#EE1289" size=4 face="Comic Sans MS">background</font>：<font color="#3A5FCD" size=4 face="Comic Sans MS">[color]</font>
颜色透明度：<font color="#EE1289" size=4 face="Comic Sans MS">rgba(n,n,n,m)</font>; 
m透明度 0-1(范围)

设置边框的圆角：border-radius:[vaule][%或px]

盒子模型(组成)：
内容---------边框---------内边距--------外边距
content-----border-------padding-------margin
边框简写：border：border-width border-style border-color
必须属性：border-style 顺序无关
设置table：
border：1px solid pink；
border-collapse：collapse //合并
placeholder="请输入..."

## margin的合并问题
### 一、垂直塌陷
##### 尽可能避免
### 二、包含垂直塌陷
##### 解决方案：
> 1.给父盒子加border
> 2.给父盒子加overflow：hidden（推荐使用）
> 网页居中div(块级元素居中)
> margin：0px auto;
#### 影响盒子的大小的因素：
border边框会影响盒子的大小
padding在特殊情况下不影响盒子大小
<center>
<--继承宽度 不继承高度-->
盒子的真实宽度：width + 左右的border + 左右padding
盒子的真实高度：height + 上下的border + 上下padding
</center>
盒子的阴影box-shadow默认就是outset(外)，不需要设置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;intset(内)
设置多个阴影可以用逗号隔开
页面常见的三种布局机制：
> 1.标准流
> 2.浮动

## 3.定位

浮动的特点：
1.浮动的元素脱标（脱离标准流），不占标准流的位置
2.浮动的元素都是以顶部对齐
3.如果浮动的元素前面是标准流的块级元素，那么浮动的元素跟在标准元素的下面
4.如果浮动的元素前面也是浮动的元素，那么后面浮动的元素会跟在前面浮动的元素后面
5.如果元素有包含关系，子元素浮动，不会跑出父元素，而且不会占据父元素的border和padding的位置
6.浮动能改变元素的显示方式

常见的页面的三种布局方式：
1.版心布局
--版心：宽度超过页面的一半，并且在页面中水平居中(class="w")
2.通栏布局
--通栏：高度不到页面的一半，宽度和页面一样高
3.分栏布局

## 分栏：左右分类

><font color="#EE1289" size=4 face="Comic Sans MS">清除浮动【clear：both】</font>;
>清除浮动的方式：{清除浮动必须使用块级元素}
>清除浮动：元素有嵌套关系，子元素浮动，父元素没有设置高度，而父元素在布局的时候又需要有高度，这个时候就需要对这个父元素中的子元素来清除浮动
>>1.给父元素加overflow：hidden  触发BFC
>>2.额外标签法
>>3.伪元素清除浮动 -->使用这种方式，必须把这个类加给父元素

```css
.clearfix::after{
    content：“.”;
    display：block
    clear：both
    visibility：hidden  //隐藏content中的内容
    height：0  //为了去掉context的内容的高度
    line-height：0;
}
```

.clearfix{  *zoom:1；} 为了解决IE6-7的兼容问题
**伪元素**：在html结构中没有，在浏览器加载完页面后，在浏览器中显示的HTML结构中有。
**伪元素**： ::before(结构前)  ::after(结构后)  可以设置样式 必须加context，可以为空
因为清除浮动必须使用块级元素，而伪元素是一个行内元素

## 4.双元素清除浮动

```css
类::before,类::after{ 
    context:"";
    display:table;
}
类::after{
    clear:both;
}
```

## css中的几个高级样式

#### 1.鼠标样式：cursor

​    text
​    pointer

#### 2.元素的显示和隐藏

<font color="#EE1289" size=4 face="Comic Sans MS">visibility</font>:<font color="#3A5FCD" size=4 face="Comic Sans MS">hidden</font>  隐藏元素，隐藏的元素占原有的位置
<font color="#EE1289" size=4 face="Comic Sans MS">visibility</font>:<font color="#3A5FCD" size=4 face="Comic Sans MS">visible</font> 显示元素
<font color="#EE1289" size=4 face="Comic Sans MS">display</font>：<font color="#3A5FCD" size=4 face="Comic Sans MS">none</font>      隐藏元素，隐藏的元素不占原有的位置 
<font color="#EE1289" size=4 face="Comic Sans MS">display</font>: <font color="#3A5FCD" size=4 face="Comic Sans MS">block</font>     显示元素，并且显示出来的元素的显示方式会被转换成块级元素

#### 3.防止文本域拖拽：resize:none

#### 4.关于垂直对齐方式

vertical-align：baseline/top/middle;

行内块元素的垂直对齐方式默认是以基线对齐,值对行内元素和行内块级元素有效
一般使用在`<input><img>` 一般用在初始化！！

#### 5.精灵图(雪碧图)：将很多的小图片做成的大图称为精灵图

核心：使用背景图片  利用背景图片移动位置
background:url("精灵图图片路径") no-repeat -12px 0px
div:first-child{
    `background-position`:-389px -145px;
}
6.外轮廓线：`outline:none;` 去掉轮廓线

<font color="red" size=4 face="Comic Sans MS">注意：外轮廓线不占边框</font> `outline：1px solid #dd2321`;

### 定位:position
1.偏移量
对于在页面中定位的元素所移动的距离
    top:   距离顶部的距离
    left:  距离左边的距离
    bottom:距离下面的距离
    right: 距离右边的距离
定位模式：position

### 1.静态定位

​    html标准流中的元素的默认定位方式就是静态定位position
特点：
>(1)遵循HTML标准流
>(2)不能设置有效的偏移量 
>(3)HTML标准流中元素的默认定位方式

### 2.相对定位(postion：relative)

​    特点相对定位的元素不脱标，占原来的位置
​    可以设置有效偏移量
​    相对定位不能改变元素的显示方式
​    相对定位是参照自身原来的位置做位移

### 3.绝对定位(postion：absolute)

​    元素脱标，不占位置
​    改变元素的显示方式
​    如果元素有包含关系，子元素绝对定位，如果父辈元素都是静态定位，那么这个绝对定位的
子元素参照浏览器来做位移;

```
如果父辈元素中有非静态定位的元素，那么这个绝对定位的子元素参照这个非静态定位的父辈元素来做位移;

如果父辈元素中有多个非静态的定位的元素，那么这个绝对定位的元素参照离自身最近的父辈元素来做位置的移动（就近元素）

子绝父相：子元素绝对定位，父元素相对定位(重点)
relative 父
absolute 子
```

### 4.固定定位(postion：fixed)

特点：
    不管父辈元素的定位方式，只要是固定定位的元素都是参照浏览器来做位置移动
    固定定位的元素脱标，不占位置
    固定定位改变了元素的显示方式

### 层级(z-index:value)
特点：
1.层级只对非静态的元素有效
2.如果都是非静态的元素，后面的元素的层级比前面的层级高
3.非静态定位的默认层级为零

<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>:`visible`; 默认就是这个值，不做任何处理
<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>:`hidden`;  直接隐藏溢出的部分
<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>:`auto`;    当文本溢出的时候，加滚动条，没有溢出不加
<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>:`scroll`;  始终都有滚动条

<font color="#EE1289" size=4 face="Comic Sans MS">white-space</font>:`nowrap`;  让文本不换行
<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>:`hidden`;     隐藏溢出的文本
<font color="#EE1289" size=4 face="Comic Sans MS">text-overflow</font>:`ellipsis`; 让溢出的文本使用省略号代替



### 属性定义及使用说明

z-index 属性指定一个元素的堆叠顺序。

拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。

**注意：** `z-index` 进行定位元素(`position:absolute`, `position:relative`, or `position:fixed`)。



```css
.index {
   height: 100vh;
   width: 100vw;
}
```



##### CSS3引入的"vw"和"vh"基于宽度/高度相对于窗口大小 

#### "vw" = "view width"  "vh" = "view height"



<font color="#EE1289" size=4 face="Comic Sans MS">overflow</font>: `hidden`; *自动隐藏文字*
<font color="#EE1289" size=4 face="Comic Sans MS">text-overflow</font>: `ellipsis`; *文字隐藏后添加省略号*
<font color="#EE1289" size=4 face="Comic Sans MS">white-space</font>: `nowrap`; *强制不换行*
<font color="#EE1289" size=4 face="Comic Sans MS">width</font>: `20em`; *不允许出现半汉字截断*

```less
/*两行*/
.textview {
  display: -webkit-box;
  overflow: hidden;
  text-overflow: ellipsis;
  word-break: break-all;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}
////////////小字体///////////
    font-size: 10px;
```



##     vertical-align: text-bottom;

<font color="#EE1289" size=4 face="Comic Sans MS">letter-spacing</font>:`value`; 设置文本的字间距(中文)
<font color="#EE1289" size=4 face="Comic Sans MS">word-spacing</font>:`value`;    设置文本的字间距(英文)

引入icon图标
link rel=“shortcut icon” href=“./favicon.ico”
www.bitbug.com   在线制作ico图标

引入css文件：先引入兼容css，在引入初始化css，再引入第三方css文件，在引入公共的css
文件，在引入当前页面的css文件
<font color="#EE1289" size=4 face="Comic Sans MS">link</font> rel=“stylesheet” href=“../css/normalize.css”   --引入兼容css
<font color="#EE1289" size=4 face="Comic Sans MS">link</font> rel="stylesheet" href="../css/base.css"        --引入初始化css
<font color="#EE1289" size=4 face="Comic Sans MS">link</font> rel="stylesheet" href="../css/common.css"      --引入公共的css

字体图标：
icomoon.io
iconfont.cn
svg标签对电脑的性能消耗大

>1.先定义字体图标样式
>2.引入对应的字体图标的Unicode编码
>3.给对应的字体调用  --base.css

```less
.iconfont {
    font-family:
}
vertical-align:middle;  /*让行内元素对齐*/
```

水平行内元素才有效果

### 利用 CSS 的 content 属性 attr 抓取资料

想必大家都想到了伪元素 after ，但是文字怎么获得呢，又不能用 JavaScript 。

CSS 的伪元素是个很強大的东西，我们可以利用他做很多运用，通常为了做一些效果， content:" " 多半会留空，但其实可以在里面写上 attr 抓资料哦！

```html
<div data-msg="这里是获取content的内容">hover</div>
```



```css
div {
    width:100px;
    border:1px solid red;  
    position:relative;
}
div:hover:after {
    content:attr(data-msg);
    position:absolute;
    font-size: 12px;
    width:200%;
    line-height:30px;
    text-align:center;
    left:0;
    top:25px;
    border:1px solid green;
}
```





# **css3**

三角:border-right:20px solid transparent 透明的
`transition`过渡：一个物体从一个状态到另一个状态的过程
帧动画：
`transition`：all 2s[属性 过渡时间];

## 面包屑导航（表示网页中的位置）

> 导语：符合下面两个条件的网站才适合使用面包屑导航。
> 1、层级较深的网站，面包屑导航适合层级较深的网站，如果只有一级分类的话，通过主导航就可以起到快速定位的作用。
> 比如“豆瓣网”类型扁平构架的网站就没有使用面包屑导航。

> 2、独立不交叉的网站结构，由于面包屑网站导航路径是线性结构的，因此网站内容必须划分的非常清晰，且不存在交叉；
> 否则，面包屑导航的路径就不是唯一的，同一分类可能出现在不同的路径中，让用户感到困惑。

导航栏设置hover高度：
<font color="#EE1289" size=4 face="Comic Sans MS">height</font>：`40px`
<font color="#EE1289" size=4 face="Comic Sans MS">line-height</font>：`40px`
<font color="#EE1289" size=4 face="Comic Sans MS">margin-top</font>：`10px`

## 重点：margin-top/bottom...可以用负值，向相反方向移动

使用JQuery和JavaScript动画制作伸缩宽度：
JavaScript：

<script>
window.onload=function(){
    var aA=document.getElementsByTagName('a');
    for(var i=0; i<aA.length; i++){
        aA[i].onmouseover=function(){
            var This=this;
            clearInterval(This.time);
            This.time=setInterval(function(){
            This.style.width=This.offsetWidth+8+"px";
            if(This.offsetWidth>=160)
                clearInterval(This.time);
            },30)
        }
        aA[i].onmouseout=function(){
            clearInterval(this.time);
            var This=this;
            this.time=setInterval(function(){
                This.style.width=This.offsetWidth-8+"px";
                if(This.offsetWidth<=120){
                    This.style.width='120px';
                    clearInterval(This.time);
                }
            },30)
        }
    }
}
</script>

JQuery：

```js
$(function(){
    $('a').hover(
        function(){
            $(this).stop().animate({"width":"160px"}.200);
        },
        function(){
            $(this).stop().animate({"width":"160px"}.200);
        }
    )
})
```



### float智能自适应

display：table-cell   IE8

display：inline-block IE7

<script src="http://apps.bdimg.com/libs/jquery/1.11.1/jquery.js"></script>

## 这个是本地百度静态API库

### JSON 基本概念:
JSON javascript 对象表示法（JavaScript Object Notation）
JSON 是存储和交换文本信息的语法，类似 XML。它采用键值对的方式来组织，易于人们阅读和编写，同时也易于机器解析和生成
JSON 是独立于语言的，也就是说不管什么语言，都可以解析 json，只需要按照 json 的规则来就行。

### JSON 与 XML 比较：
json 的长度和 xml 格式比起来很短小
json 读写的速度更快
json 可以使用 javascript 内建的方法直接进行解析，转换成 JavaScript 对象，非常方便。

json 数据的书写格式是：名称/值对
名称/值对组合中的名称写在前面（在双引号中），值对写在后面（同样在引号中），中间用冒号隔开：比如："name"："郭靖"
json的值可以是下面这些类型：
数字（整数或浮点数），比如：123,1,23
    字符串（在双引号中）
    逻辑值（`true` 和 `false`）
    数组（在方括号中）
    对象（在花括号中）
    null
例如：
```js
{
    "staff":[
        {"name":"洪七","age":70},
        {"name":"郭靖","age":35},
        {"name":"黄蓉","age":30}
    ]
}
```

**推荐用 JSONLint 工具（在线）检验**

用 jQuery 实现 ajax
语法：jQuery.ajax([settings])

`type`：类型，“POST”或“GET”，默认为“GET”
`url`：发送请求的地址
`data`：是一个对象，连同请求发送到服务器的数据
`dataType`：预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 Http 包 MIME 信息来智能判断，一般我们采用json 格式，可以设置为“json”
`success`：是一个方法，请求成功后的回调函数。传入返回后的数据，以及包含成功代码的字符串
`error`：是一个方法，请求失败时调用此函数。传入XMLHttpRequest对象

`jsonp`： 可用于解决主流浏览器的跨域数据访问的问题，jsonp 不支持 psot 请求，只支持 GET 请求，而且 JSONP 返回的是一个数组
用“.”表示
`XMR2`：HTML5 提供的 XMLHttpRequest Level2 已经实现了跨域访问以及其他的一些新功能
在服务器端做一些小小的改造即可：
header('Access-Control-Allow-Origin:*');
header('Access-Control-Allow-Methods:POST,GET');