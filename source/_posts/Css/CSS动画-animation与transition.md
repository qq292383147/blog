---
title: CSS动画 animation与transition
date: 2019-03-31 18:38:38
tags: css
type: css
categories: css
---

## 一、区分容易混淆的几个属性和值

　　先区分一下css中的几个属性：`animation`（动画）、`transition`（过渡）、`transform`（变形）、`translate`（移动）。<br>
<br>
　　CSS3中的`transform`(变形)属性用于内联元素和块级元素，可以旋转、扭曲、缩放、移动元素，它的属性值有以下五个：旋转`rotate`、扭曲`skew`、缩放`scale`和移动`translate`以及矩阵变形matrix；
<br>
　　`transform`(变形)是CSS3中的元素的属性，而translate只是`transform`的一个属性值；`transform`是transition（过渡动画）的transition-property的一个属性值。
<br>


　　`animation`（动画）、`transition`（过渡）是css3中的两种动画属性。animation强调流程与控制，对元素的一个或多个属性的变化进行控制，可以有多个关键帧（animation和@keyframes结合使用）；
<br>
　　`transition`强调过渡，是元素的一个或多个属性发生变化时产生的过渡效果，同一个元素通过两个不同的途径获取样式，而第二个途径当某种改变发生（例如hover）时才能获取样式，这样就会产生过渡动
<br>
画。可以认为它有两个关键帧（`transition` ＋ `transform` ＝ 两个关键帧的`Animation`）。<br>

 

transition示例：
<br>
(1)#box1，产生双边过渡效果
<br>
box1在hover后有两个属性改变了，改变前和改变后的属性值分别是:
<br>
　


>改变前：
>　
>background: green;
> 　　 transform:rotate(0deg);//这个可视为默认状态，即旋转度为0
>
>　改变后：
>　　　　background: red;
>　　　　transform:rotate(180deg);
>
>并且在#box1中设置了过渡动画 transition: background 2s ease,transform 2s ease-in 1s; 可知在background和transform属性变化时会产生动画效果，而这种效果的产生有两种途径：
>
>一种是从默认到hover触发了过渡效果； 一种是从hover回到默认这两种属性也变化了，因此也产生了过渡效果。


​    

<font color="red">注意点：这其中包括两个方向上的，当鼠标在div上悬停，div的样式从原始样式过渡到div：hover的样式；当鼠标离开div，样式又从div：hover过渡到div默认样式。这两个方向上的过渡都是平滑不突兀的</font>
<br>
<br>


```html
<style>
  #box1 {
     height: 100px;
     width: 100px;
      background: green;
      ransition: background 2s ease,transform 2s ease-in 1s;
      }
  #box1:hover{transform:rotate(180deg) scale(.5,.5);background:red;}
</style>
<body>
 <div id="box1">BOX1</div>
</body>
```

## （2）#box2 产生单边过渡效果

什么情况下只会产生单边过渡效果呢，看下面的例子，与#box1一样，#box2也有相同的两个属性发生了改变：
　


>　改变前：
>　
>background: blue;
>　　 transform:rotate(0deg);//这个可视为默认状态，即旋转度为0
>
>　改变后：
>　　　　background: red;
>　　　　transform:rotate(180deg);
><br>
>但是与#box1不同的是，#box2将过渡动画 transition放在了 #box2:hover中进行设置。这样情况下：只有在鼠标悬停时，才会触发过渡动画，过渡平滑；而鼠标离开时，不会产生过渡动画，background、transform将会生硬的回到最初的属性值上。

<font color="red">注意点：这个例子中的过渡动画是单一方向上的。当鼠标在div上悬停，div的样式从原始样式过渡到div：hover的样式；当鼠标离开div，样式会从div：hover的样式回到原始样式，但不是过渡动画的方式，而是直接回到原始样式，看上去比较突兀和生硬。</font>
<br>


```html
<style>     
   #box2 {
      height: 100px;
      width: 100px;
      background: blue;
  }
   #box2:hover {
      transform: rotate(180deg) scale(.5, .5);
      background: red;
      transition: background 2s ease, transform 2s ease-in 1s;}
</style>
</head>
<body>
 <div id="box1">BOX1</div>
 <div id="box2">BOX2</div>
</body>
```

 

## 二、transition

#### 1、语法

>　`transition`是一个复合属性，可设置四个过渡属性，简写方式如下：
>
> transition{ transition-property  transition-duration  transition-timing-function  transition-delay}

 　　

　　`transition-property`：是用来指定当元素其中一个属性改变时执行`transition`效果，值有none（没有属性改变）、all（默认值，所有属性改变），indent（某个属性名，一条`transition`规则，只能定义一个属性的变化，不能涉及多个属性，如果要设置多个属性时，需分别设置，中间以逗号隔开）【当其值为none时，`transition`马上停止执行，当指定为all时，则元素产生任何属性值变化时都将执行transition效果】。css中的能够产生动画的属性列表（`transition`动画和`animation`动画适用）
<br>
　　`transition-duration` ：过渡时间，是用来指定元素转换过程的持续时间，单位为s（秒）或ms（毫秒）
<br>
　　`transition-timing-function`：时间函数，允许你根据时间的推进去改变属性值的变换速率，值ease（逐渐变慢）、linear（匀速）、ease-in(加速) 、ease-out（减速）、ease-in-out：（加速,然后减速）、cubic-bezier：（该值允许你去自定义一个时间曲线）   贝塞尔曲线扫盲    工具网站
<br>
　　`transition-delay`：延迟，指定一个动画开始执行的时间，也就是说当改变元素属性值后多长时间开始执行transition效果，单位为s（秒）或ms（毫秒）
<br>


#### 2 、触发方式

>伪类触发：:hover : focus  :checked  :active
>
>js触发：toggleClass<br>

#### 3、以下情况下，属性值改变不能产生过渡效果

1. background-image，如url(a.jpg)到url(b.jpg)（与浏览器支持相关，有的浏览器不支持）等
2. float浮动元素
3. height或width使用auto值
4. display属性在none和其他值（block、inline-block、inline）之间变换
5. position在stativ和absolute之间变换

#### 4、transition属性浏览器兼容情况

 ![img](F:\图片库blog/picture_images/picture/css/11.jpg)

 

## 三、animation

　　`animation`属性结合@<font color="#cc2e67">keyframes</font>使用， `animation`中的animation-name需要设置成@<font color="#cc2e67">keyframes</font>的name一致。
<br>
animation示例
<br>


```html
<style>
    .box{height:100px;width:100px;border:15px solid black;
        animation: changebox 10s ease-in-out   3 alternate paused;
        }
    .box:hover{
        animation-play-state: running;
    }
    @keyframes changebox {
        10% {  background:red;  }
        50% {  width:80px;  }
        70% {  border:15px solid yellow;  }
        100% {  width:180px;  height:180px;  }
    }
</style>
<body>
 <div class="box"></div>
</body>
```



#### 1、@keyframes关键帧



```css
@keyframes changebox {
      10% {  background:red;  }
      50% {  width:80px;  }
      70% {  border:15px solid yellow;  }
      100% {  width:180px;  height:180px;  }
    }
```
<br>

　　设置方法如上，其中0%和100%还可以使用关键词`from`和`to`来代表，大括号中设置不同时间段的样式规则。
<br>
　　如上示例中，`animation`中设置`animation-duration`的值是10s，并通过`animation-name`为changebox引入@<font color="#cc2e67"keyframes</font> changebox中的样式，表示在10秒内执行动画，动画执行过程个人理解如下：
<br>


| 序号 | 执行时间（共10s）animation-duration：10s | 执行动画                                               | 对应@keyframes changebox中的规则 |
| -------- | ------------------------------------------------ | ---------------------------------------------------------- | ------------------------------------ |
| 1        | 0~1s                                             | 背景色由默认变为红色                               | 10%{  background:red;  }             |
| 2        | 0~5s                                             | 宽度由原始设定的100px变为80px(并不是1~5s之间执行） | 50% {  width:80px;  }                |
| 3        | 0~7s                                             | 边框由原始设定的无变为border:15px solid yellow;    | 70% {  border:15px solid yellow;  }  |
| 4        | 5~10s                                            | 宽度由在5s时的80px变为180px                       | 100%{  width:180px;height:180px;  }  |
| 5        | 0~10s                                            | 高度原始设定的100px变为180px                      | 无 |

<font color="#c82862">特别注意的是：每一个百分号后面的样式变化都是从`0s`开始的，除非有两个百分比设置了同一个样式的变化（上方的例子，50% {  <font color="#42a5f5">width</font>:80px;  }  100%{<font color="#42a5f5">width</font>:150px;}，那么宽度的整体情况会是`0~5s`中宽度由原始值变为80px；5~10s间，宽度由80px变为180px；），个人理解，在这个过程中，不是一个动画，而是多个小动画（自己起的名字，方便后面区分animation）按照设定好的百分比对应的时间正好执行完成结同一时间内有可能有多个小动画同时在执行，也有可能只有一个小动画在执行。</font>
<br>
<br>


#### 2、animation语法

　　设置好了关键帧，就可以设置animation属性了，animation也是一个符合属性，可以简写，语法如下：
<br>
```scss
animation { 
    animation-name  
    animation-duration
    animatino-timing-function
    animation-delay
    animation-iteration-count
    animation-direction
    animtion-play-state
    animation-fill-mode
}
```

　　`animation-name`：用来调用@<font color="#e1266f">keyframes</font>定义好的动画，与@keyframes定义的动画名称一致

　　`animation-duration` ：指定元素播放动画所持续的时间
<br>
　　`animatino-timing-function` ： 和`transition`中的`transition-timing-function` 中的值一样。根据上面@keframes中分析的animation中可能存在多个小动画，因此这里的值设置是针对每一个小动画所在时间范围内的属性变换速率。
<br>
　　`animation-delay`：定义在浏览器开始执行动画之前等待的时间，这里是指整个animation执行之前的等待时间，而不是上面说的多个小动画
<br>
　　`animation-iteration-count`：定义动画的播放次数，其通常为整数，默认是1,；取值为infinite，动画将无限次的播放。
<br>
　　`animation-direction`：主要用来设置动画播放方向，其主要有两个值：
<br>
normal 默认值，如果设置为normal时，动画每次循环都是向前（即按顺序）播放
alternate（轮流），动画播放在第偶数次向前播放，第奇数次向反方向播放（animation-iteration-count取值大于1时设置有效）
<br>
　　`animtion-play-state`：属性是用来控制元素动画的播放状态。其主要有两个值：
<br>
 running，可以通过该值将暂停的动画重新播放，这里的重新播放不是从元素动画的开始播放，而是从暂停的那个位置开始播放。
paused，暂停播放
<br>
​      注意：使用`animtion-play-state`属性，当元素动画结束后，元素的样式将回到最原始设置状态（这也是为什么要引入animation-fill-mode属性的原因）
<br>
　animation-fill-mod：默认情况下，动画结束后，元素的样式将回到起始状态，animation-fill-mode属性可以控制动画结束后元素的样式。主要具有四个属性值：
<br>
none（默认，回到动画没开始时的状态。）
forwards（动画结束后动画停留在结束状态）
backwords（动画回到第一帧的状态）
both（根据animation-direction轮流应用forwards和backwards规则）。
<br>

#### 3、animation属性浏览器兼容情况

 ![img](F:\图片库blog/picture_images/picture/css/12.jpg)