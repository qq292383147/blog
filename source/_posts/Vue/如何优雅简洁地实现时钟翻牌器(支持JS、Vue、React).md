---
title: 如何优雅简洁地实现时钟翻牌器(支持JS、Vue、React)
date: 2019-11-27 22:23:40
tags:  vue
categories: vue
---



![114](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/114.jpg)

相信很多人都已经自己独立实现过了，我也在网上看了一些demo，发现HTML结构大多比较复杂，用了4个并列的标签来放置前后两个“牌”。本文就来讲解下，如何进一步精简HTML，让结构简单，让JS方法封装得易使用。先来看看最终效果：

![115](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/115.gif)

每个翻牌的HTML结构（精简至2个并列标签）：

```html
<div class="flip down">
    <div class="digital front number0"></div>
    <div class="digital back number1"></div>
</div>
```

本次分享含有很多小技巧，灵活使用能够提升技术水平和工作效率，具体包括以下知识点：

知识点1：`:before :after`伪元素的使用

知识点2：line-height: 0的妙用

知识点3：transform-origin和perspective

知识点4：backface-visibility

知识点5：时间格式化函数的实现

Let's do it!

### 1 翻牌的构建

#### 1.1 基本结构

首先解释下HTML的结构：

```html
<!-- 翻牌的外框 -->
<div class="flip down">
    <!-- 位于前面的纸牌 -->
    <div class="digital front number0"></div>
    <!-- 位于后面的纸牌 -->
    <div class="digital back number1"></div>
</div>
```

【说明】

flip: 纸牌的外框

down：表示向下翻牌动效，还有对于的up。后面章节会具体讲解。

front: 表示位于前面的纸牌

back: 表示位于后面的纸牌

number*: 表示纸牌上的数字

flip的CSS代码如下：

```scss
.flip {
    display: inline-block;
    position: relative;
    width: 60px;
    height: 100px;
    line-height: 100px;
    border: solid 1px #000;
    border-radius: 10px;
    background: #fff;
    font-size: 66px;
    color: #fff;
    box-shadow: 0 0 6px rgba(0, 0, 0, .5);
    text-align: center;
    font-family: "Helvetica Neue"
}
```

这段代码很基础，就不再详细解释了。眼尖的同学可能发现了，为什么要设置background为#fff(白色)呢?最终效果明明是黑的。留个疑问，下一小节就会明白了。

基本结构的效果是这样的:

![116](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/116.jpg)

#### 1.2 构建纸牌并用伪元素拆分上下两部分

由于每个纸牌是上下对折、翻转的，所以每个纸牌要拆分成上下两部分。可是HTML中每个纸牌只有一个标签，怎么拆分成两个呢？这里就用到了before和after伪元素。

#### 知识点1： 伪元素的使用

先看代码：

```scss
.flip .digital:before,
.flip .digital:after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    background: #000;
    overflow: hidden;
}

.flip .digital:before {
    top: 0;
    bottom: 50%;
    border-radius: 10px 10px 0 0;
}

.flip .digital:after {
    top: 50%;
    bottom: 0;
    border-radius: 0 0 10px 10px;
}
```

:before和:after在digital内部生成了两个伪元素，其中，before用来生成纸牌的“上半张”，after用来生成纸牌的“下半张”。

因此，before“上半张”为从“顶部（`top: 0`）”到“距底一半(`bottom: 50%`)”的部分，顶部两侧为圆角。

同理，after“下半张”为“距顶一半（`top: 50%`）”到“底部（`bottom: 0`）”的部分，底部两侧为圆角。

注意代码中的`content: ""`不能省略，否则伪元素是不显示的。

效果如下：

![117](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/117.jpg)

> 回答上一章节的问题，为什么底层设置background为白色？
>
> 答案很简单，元素内部的纸片边角和外层边角之间会有一点点的缝隙，这个缝隙会露出底部的白色，从视觉效果上看，更加具有立体感。

然后，为上下部分中间添加一条水平折线。

```scss
    .flip .digital:before,
    .flip .digital:after {
        content: "";
        position: absolute;
        left: 0;
        right: 0;
        background: #000;
        overflow: hidden;
+       box-sizing: border-box; 
    }
    ...(略)
    .flip .digital:before {
        top: 0;
        bottom: 50%;
        border-radius: 10px 10px 0 0;
+       border-bottom: solid 1px #666;
    }
```

外层flip添加`box-sizing: border-box`保证了下边框不会影响元素的原有高度。

效果如下：

![118](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/118.jpg)

到这里，我们可以认为是4个小纸片，分别是：

1. 前上：.digital.front:before
2. 前下：.digital.front:after
3. 后上：.digital.back:before
4. 后下：.digital.back:after

由于重叠在一起，只能看到一张纸牌。而看到的这个纸牌是后面（back）的纸牌，为什么呢？因为back的HTML写在了front的后面。不过没关系，后面我们会通过z-index来重新调整层叠顺序，先不着急。

#### 1.3 为纸牌添加文字

还记的刚才的`content: ""`吗？纸牌的文字显示就用到了这个。

先通过CSS定义好0~9的数字：

```scss
.flip .number0:before,
.flip .number0:after {
    content: "0";
}

.flip .number1:before,
.flip .number1:after {
    content: "1";
}

.flip .number2:before,
.flip .number2:after {
    content: "2";
}
...(略)
.flip .number9:before,
.flip .number9:after {
    content: "9";
}
```

现在效果如下：

![119](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/119.jpg)

可以很明显的看到两个问题：

1. 本应该在后面的back纸牌跑到了前面(z-index问题)
2. 下半张纸牌的文字应该只显示下半部分。

先来解决问题2，这里就涉及到了第二个知识点。

#### 知识点2：line-height: 0的妙用

提到文字的显示，肯定会想到基线（baseline），可能你也曾经看过这个图：

![120](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/120.jpg)

关于基线(baseline)的计算，确实很麻烦，我也在这里绕了很久。其实理解line-height:0可以换个角度，会更容易理解，请看下图：

![121](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/121.jpg)

当line-height为200px，每行文字高度为200px，文字在200px高度的行间区域垂直居中；

当line-height为100px，每行文字高度为100px，文字在100px高度的行间区域垂直居中；

当line-height为0时，行间距为0，中线的位置也为0，所以文字只有下半部分留在容器内。

利用line-height:0的特性，就可以很轻易实现“下半张”纸牌只显示文字的下半部分，并且与“上半张”纸牌很好的衔接在一起。

在代码中设置line-height为0：

```scss
    .flip .digital:after {
        top: 50%;
        bottom: 0;
        border-radius: 0 0 10px 10px;
+       line-height: 0;
    }
```

效果如下：

![122](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/122.jpg)

#### 1.4 设置纸牌的层叠关系

首先，先看下“向下翻牌”的视频演示，直观感受下每个纸片的层级关系：

![123](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/123.gif)

按照实物图就可以确定每张纸片的z-index：

![124](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/124.jpg)

添加以下CSS代码：

```scss
/*向下翻*/
.flip.down .front:before {
    z-index: 3;
}

.flip.down .back:after {
    z-index: 2;
}

.flip.down .front:after,
.flip.down .back:before {
    z-index: 1;
}
```

现在效果如下：

![125](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/125.jpg)

咦？怎么不对？别着急，这是因为我们只设置了层级，但是没有把后面纸牌的下半部翻转上去。

添加翻转代码：

```scss
    .flip.down .back:after {
        z-index: 2;
+       transform-origin: 50% 0%;
+       transform: perspective(160px) rotateX(180deg);
    }
```

这里涉及到了知识点3。

#### 知识点3：transform-origin和perspective

`transform-origin`是元素旋转的基本点。

`transform-origin: 50% 0%;`表示将旋转基本点设置在横轴的中点，纵轴的顶点位置，如下图所示：

![126](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/126.jpg)

`perspective(160px)`可以理解为立体透视图的景深。在本次分享的效果中，我们的视角是正对牌面，并且纸牌位于视角中间。所以 transform-origin的第一个值（X轴位置）为50%。

`rotateX(180deg)`表示以X轴进行翻转，对应这里就是上下翻转。这里已经通过transform-origin的第二个参数（Y轴位置：0%）将X轴放在了元素顶部。

基于以上设置，已经可以正常显示了，如下图：

![127](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/127.jpg)

同理，“向上翻”也需要进行设置下。大家可以自己折两个纸片，参照上面的方法，应该很容易实现。这里不再重复讲解，直接放上代码，大家可以对比下哪里不同：

```scss
/*向上翻*/
.flip.up .front:after {
    z-index: 3;
}

.flip.up .back:before {
    z-index: 2;
    transform-origin: 50% 100%;
    transform: perspective(160px) rotateX(-180deg);
}

.flip.up .front:before,
.flip.up .back:after {
    z-index: 1;
}
```

### 2 翻牌动画的实现

现在纸片都已摆好了，剩下的就是实现CSS3动画，以及JS交互控制。

#### 2.1 CSS3翻牌动画

我们还是以“向下翻”为例，再来看下之前的实物翻牌视频：

![128](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/128.gif)

可以看到，“向下翻”主要涉及两个元素的动画：

1. 前面纸牌的上半部向下翻转180度。
2. 后面纸牌的下半部（目前已翻转上去）向下翻转180度恢复原状态。

![129](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/129.jpg)

直接上代码：

```scss
.flip.down.go .front:before {
    transform-origin: 50% 100%;
    animation: frontFlipDown 0.6s ease-in-out both;
    box-shadow: 0 -2px 6px rgba(255, 255, 255, 0.3);
}

.flip.down.go .back:after {
    animation: backFlipDown 0.6s ease-in-out both;
}

@keyframes frontFlipDown {
    0% {
        transform: perspective(160px) rotateX(0deg);
    }

    100% {
        transform: perspective(160px) rotateX(-180deg);
    }
}

@keyframes backFlipDown {
    0% {
        transform: perspective(160px) rotateX(180deg);
    }

    100% {
        transform: perspective(160px) rotateX(0deg);
    }
}
```

以上代码涉及的知识点和原理没有新的东西，都已经讲解过了，就不详述了。box-shadow是为了给纸片的上边缘加一点白光，视觉效果更好一点。否则在翻转的时候，跟后面元素都是黑色，融在一起了。看看现在的效果：

![130](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/130.gif)

显示不正常！为什么？因为前排上半部纸片的z-index最高，所以它在翻转到下半部的时候仍然遮挡住了其他纸片。怎么优雅的解决？超级简单，来看看第四个知识点：

#### 知识点4：backface-visibility

backface-visibility表示元素的背面是否可见，默认为visible（可见）。

这里的需求是，当前面上半部纸片翻转到一半的时候（90度）进入不可见状态。而纸牌翻转90度以后，正好是显露元素背面的开始，所以将backface-visibility设置为hidden即可完美解决！

修改代码如下：

```scss
    .flip.down.go .front:before {
        transform-origin: 50% 100%;
        animation: frontFlipDown 0.6s ease-in-out both;
        box-shadow: 0 -2px 6px rgba(255, 255, 255, 0.3);
+       backface-visibility: hidden;
    }
```

现在效果很完美！

![131](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/131.gif)

大家可以试着自己实现向上翻转效果，代码直接放出：

```scss
.flip.up.go .front:after {
    transform-origin: 50% 0;
    animation: frontFlipUp 0.6s ease-in-out both;
    box-shadow: 0 2px 6px rgba(255, 255, 255, 0.3);
    backface-visibility: hidden;
}

.flip.up.go .back:before {
    animation: backFlipUp 0.6s ease-in-out both;
}
@keyframes frontFlipUp {
    0% {
        transform: perspective(160px) rotateX(0deg);
    }

    100% {
        transform: perspective(160px) rotateX(180deg);
    }
}

@keyframes backFlipUp {
    0% {
        transform: perspective(160px) rotateX(-180deg);
    }

    100% {
        transform: perspective(160px) rotateX(0deg);
    }
}
```

#### 2.2 JS实现翻牌交互

现在我们来实现一个简单的交互。需求是：

1. 点击“+”，向下翻牌，数字+1
2. 点击“-”，向上翻牌，数字-1

首先，修改下HTML：

```html
+   <div class="single-demo">
M       <div class="flip down" id="flip">
            <div class="digital front number0"></div>
	        <div class="digital back number1"></div>
	    </div>
+	</div>
+   <div class="btn-con">
+       <button id="btn1">向下翻+1</button>
+       <button id="btn2">向上翻-1</button>
+   </div>
```

配套的CSS如下，仅为了demo好看，无实际作用:

```scss
.single-demo {
    margin: 50px auto;
    padding: 30px;
    width: 600px;
    text-align: center;
    border: solid 1px #999;
}
```

Javascript代码如下：

```js
var flip = document.getElementById('flip')
var backNode = document.querySelector('.back')
var frontNode = document.querySelector('.front')
var btn = document.getElementById('btn')
btn1.addEventListener('click', function() {
    flipDown();
})
btn2.addEventListener('click', function() {
    flipUp();
})
// 当前数字
var count = 0
// 是否正在翻转（防止翻转未结束就进行下一次翻转）
var isFlipping = false

// 向下翻转+1
function flipDown() {
    // 如果处于翻转中，则不执行
    if (isFlipping) {
        return false
    }
    // 设置前牌的文字
    frontNode.setAttribute('class', 'digital front number' + count)
    // 计算后牌文字（越界判断）
    var nextCount = count >= 9 ? 0 : (count + 1)
    // 设置后牌的文字
    backNode.setAttribute('class', 'digital back number' + nextCount)
    // 添加go，执行翻转动画
    flip.setAttribute('class', 'flip down go')
    // 将翻转态设置为true
    isFlipping = true
    // 翻转结束后，恢复状态
    setTimeout(function() {
        // 去掉go
        flip.setAttribute('class', 'flip down')
        // 将翻转态设置为false
        isFlipping = false
        // 设置前牌文字为+1后的数字
        frontNode.setAttribute('class', 'digital front number' + nextCount)
        // 更新当前文字
        count = nextCount
    }, 1000)
}
// 向上翻转-1（同理，注释略）
function flipUp() {
    if (isFlipping) {
        return false
    }
    frontNode.setAttribute('class', 'digital front number' + count)
    var nextCount = count <= 0 ? 9 : (count - 1)
    backNode.setAttribute('class', 'digital back number' + nextCount)
    flip.setAttribute('class', 'flip up go')
    isFlipping = true
    setTimeout(function() {
        flip.setAttribute('class', 'flip up')
        isFlipping = false
        frontNode.setAttribute('class', 'digital front number' + nextCount)
        count = nextCount
    }, 1000)
}
```

先看下交互效果：

![132](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/132.gif)

这段Javascript代码很冗余，重复代码很多。在实际产品中，都是多个数字牌，这种方式显然无法应对。下一章节，我们来说下如何优雅的封装，以不变应万变。

### 3 翻牌时钟的实现

先看下最终效果：

![133](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/133.gif)

#### 3.1 HTML构建

HTML代码如下：

```scss
<div class="clock" id="clock">
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
    <em>:</em>
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
    <em>:</em>
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
    <div class="flip down">
        <div class="digital front number0"></div>
        <div class="digital back number1"></div>
    </div>
</div>
```

CSS代码如下(之前章节的CSS代码请保留):

```scss
.clock {
    text-align: center;
}

.clock em {
    display: inline-block;
    line-height: 102px;
    font-size: 66px;
    font-style: normal;
    vertical-align: top;
}
```

效果如下，剩下的就是JS部分了。

![134](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/134.jpg)

#### 3.2 构建Flipper类

将每个翻牌封装成类，这样在应对多个翻牌的时候，可以方便的通过new Flipper()去独立控制每个翻牌对象。

类的实现代码如下：

```js
function Flipper(config) {
    // 默认配置
    this.config = {
        // 时钟模块的节点
        node: null,
        // 初始前牌文字
        frontText: 'number0',
        // 初始后牌文字
        backText: 'number1',
        // 翻转动画时间（毫秒，与翻转动画CSS 设置的animation-duration时间要一致）
        duration: 600,
    }
    // 节点的原本class，与html对应，方便后面添加/删除新的class
    this.nodeClass = {
        flip: 'flip',
        front: 'digital front',
        back: 'digital back'
    }
    // 覆盖默认配置
    Object.assign(this.config, config)
    // 定位前后两个牌的DOM节点
    this.frontNode = this.config.node.querySelector('.front')
    this.backNode = this.config.node.querySelector('.back')
    // 是否处于翻牌动画过程中（防止动画未完成就进入下一次翻牌）
    this.isFlipping = false
    // 初始化
    this._init()
}
Flipper.prototype = {
    constructor: Flipper,
    // 初始化
    _init: function() {
        // 设置初始牌面字符
        this._setFront(this.config.frontText)
        this._setBack(this.config.backText)
    },
    // 设置前牌文字
    _setFront: function(className) {
        this.frontNode.setAttribute('class', this.nodeClass.front + ' ' + className)
    },
    // 设置后牌文字
    _setBack: function(className) {
        this.backNode.setAttribute('class', this.nodeClass.back + ' ' + className)
    },
    _flip: function(type, front, back) {
        // 如果处于翻转中，则不执行
        if (this.isFlipping) {
            return false
        }
        // 设置翻转状态为true
        this.isFlipping = true
        // 设置前牌文字
        this._setFront(front)
        // 设置后牌文字
        this._setBack(back)
        // 根据传递过来的type设置翻转方向
        let flipClass = this.nodeClass.flip;
        if (type === 'down') {
            flipClass += ' down'
        } else {
            flipClass += ' up'
        }
        // 添加翻转方向和执行动画的class，执行翻转动画
        this.config.node.setAttribute('class', flipClass + ' go')
        // 根据设置的动画时间，在动画结束后，还原class并更新前牌文字
        setTimeout(() => {
            // 还原class
            this.config.node.setAttribute('class', flipClass)
            // 设置翻转状态为false
            this.isFlipping = false
            // 将前牌文字设置为当前新的数字，后牌因为被前牌挡住了，就不用设置了。
            this._setFront(back)
        }, this.config.duration)
    },
    // 下翻牌
    flipDown: function(front, back) {
        this._flip('down', front, back)
    },
    // 上翻牌
    flipUp: function(front, back) {
        this._flip('up', front, back)
    }
}
```

可以注意到，Flipper的传参只接受一个对象形式的参数config，使用对象的方式向函数传参有很多优点：

1. 参数语义化，方便理解
2. 不用在意参数顺序
3. 传参的增删和顺序调整不会影响业务代码的使用

使用Object.assign方法，可将传递进来的config参数覆盖默认参数。传递的config中没有的属性，则使用默认配置。当然，这种方式只适用于浅拷贝。

> 关于prototype，以及为什么要设置constructor，请阅读我的另一篇文章《一张刮刮卡竟包含这么多前端知识点》第4.1章节，已经讲解得很详细了。

代码逻辑请阅读注释。

#### 3.3 实现时钟业务逻辑

接下来的工作就是将js与dom进行绑定。

请看代码：

> 这段代码一定要放在Flipper类代码的下面，Flipper.prototype一定要在业务逻辑代码之前执行，否则会报错找不到Flipper内部方法。

```js
// 定位时钟模块
let clock = document.getElementById('clock')
// 定位6个翻板
let flips = clock.querySelectorAll('.flip')
// 获取当前时间
let now = new Date()
// 格式化当前时间，例如现在是20:30:10，则输出"203010"字符串
let nowTimeStr = formatDate(now, 'hhiiss')
// 格式化下一秒的时间
let nextTimeStr = formatDate(new Date(now.getTime() + 1000), 'hhiiss')
// 定义牌板数组，用来存储6个Flipper翻板对象
let flipObjs = []
for (let i = 0; i < flips.length; i++) {
    // 创建6个Flipper实例，初始化并存入flipObjs
    flipObjs.push(new Flipper({
        // 每个Flipper实例按数组顺序与翻板DOM的顺序一一对应
        node: flips[i],
        // 按数组顺序取时间字符串对应位置的数字
        frontText: 'number' + nowTimeStr[i],
        backText: 'number' + nextTimeStr[i]
    }))
}
```

代码逻辑不难，请阅读注释。比较值得分享的是其中的时间格式化函数formatDate。

#### 知识点5：时间格式化函数的实现

为了方便业务使用，实现一个时间格式化方法，这个方法在很多其他业务中都会使用到，具有很普遍的实用价值。

需求是通过输入日期时间格式要求，输出对应的字符串。

例如：

```js
yyyy-mm-dd hh:ii:ss` 输出：`2019-06-02 08:30:37
yy-m-d h:i:s` 输出：`19-6-2 8:30:37
```

先看代码：

```js
//正则格式化日期
function formatDate(date, dateFormat) {
    /* 单独格式化年份，根据y的字符数量输出年份
     * 例如：yyyy => 2019
            yy => 19
            y => 9
     */
    if (/(y+)/.test(dateFormat)) {
        dateFormat = dateFormat.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length));
    }
    // 格式化月、日、时、分、秒
    let o = {
        'm+': date.getMonth() + 1,
        'd+': date.getDate(),
        'h+': date.getHours(),
        'i+': date.getMinutes(),
        's+': date.getSeconds()
    };
    for (let k in o) {
        if (new RegExp(`(${k})`).test(dateFormat)) {
            // 取出对应的值
            let str = o[k] + '';
            /* 根据设置的格式，输出对应的字符
             * 例如: 早上8时，hh => 08，h => 8
             * 但是，当数字>=10时，无论格式为一位还是多位，不做截取，这是与年份格式化不一致的地方
             * 例如: 下午15时，hh => 15, h => 15
             */
            dateFormat = dateFormat.replace(RegExp.$1, (RegExp.$1.length === 1) ? str : padLeftZero(str));
        }
    }
    return dateFormat;
};

//日期时间补零
function padLeftZero(str) {
    return ('00' + str).substr(str.length);
}
```

代码逻辑请阅读注释，这里再补充下“日期时间补零padLeftZero”函数的说明。由于月、日、时、分、秒最多为2位数，所以这里只考虑最多补一个0的情况。

原理是：不管数字是几位，先在前面补两个0，再根据原数字的位数进行截取，最终输出固定为两位的补零数字

例如：数字"16"是两位数，先补两个0变成"0016"，再从该字符串的索引[2]开始截取（2=原数字的位数），由于字符串索引从[0]开始，所以[2]对应字符串的第3位，输出结果仍为"16。

同理，数字"8"是1位数，先补两个0变成"008",再从该字符串的索引[1]开始截取（1=原数字的位数），即从第2位开始截取，输出"08"。

这样就实现了补零的功能。

现在看下效果，已经可以正确显示当前时间了。

![135](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/135.jpg)

#### 3.4 运行时钟

万事俱备，只差加个定时器让时钟翻动起来。

```js
setInterval(function() {
    // 获取当前时间
    let now = new Date()
    // 格式化当前时间
    let nowTimeStr = formatDate(new Date(now.getTime() - 1000), 'hhiiss')
    // 格式化下一秒时间
    let nextTimeStr = formatDate(now, 'hhiiss')
    // 将当前时间和下一秒时间逐位对比
    for (let i = 0; i < flipObjs.length; i++) {
        // 如果前后数字没有变化，则直接跳过，不翻牌
        if (nowTimeStr[i] === nextTimeStr[i]) {
            continue
        }
        // 传递前后牌的数字，进行向下翻牌动画
        flipObjs[i].flipDown('number' + nowTimeStr[i], 'number' + nextTimeStr[i])
    }
}, 1000)
```

这段代码逻辑很简单了，主要就是进行前后时间字符串的对比，然后设置纸牌并翻转。最终效果：

![136](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/136.gif)

### 4 Vue & React封装

由于篇幅有限，这里不再详述，原理都是一样的，只是利用Vue和React的API和语法进行封装。

原生JavaScript、Vue、React三个版本的演示源码请到我的github下载:

[github.com/Yuezi32/fli…](https://github.com/Yuezi32/flipClock)