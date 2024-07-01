---
title: 使用CSS3开发同心圆弧旋转 loading 特效
date: 2019-03-17 14:28:13
tags: css
type: css
categories: css
---
好了，话不多说，先来看看今天的效果。

![](F:\图片库blog/picture_images/picture/css/1.gif)

今天还是不用JS，就用CSS3做一个循环动画就好了。

先定义DOM，写一个元素就行了

![](F:\图片库blog/picture_images/picture/css/2.jpg)

然后就是下样式了，先做个居中显示

![](F:\图片库blog/picture_images/picture/css/3.jpg)

我们今天做的一共画三层圆弧，先画最外一层的样式：

![](F:\图片库blog/picture_images/picture/css/4.jpg)

再用伪元素画中间一层的样式：

![](F:\图片库blog/picture_images/picture/css/5.jpg)

再用伪元素画最内一层的样式：

![](F:\图片库blog/picture_images/picture/css/6.jpg)

定义一个自动循环动画效果：

![](F:\图片库blog/picture_images/picture/css/7.jpg)

最后，应用动画效果到每层，每层都执行自动动画，时间差不一样，产生交叉效果：

![](F:\图片库blog/picture_images/picture/css/8.jpg)

运行，就完成了

![](F:\图片库blog/picture_images/picture/css/9.gif)

全部CSS源码展示：

![](F:\图片库blog/picture_images/picture/css/10.jpg)

这次的课程，难点不多，主要还是在画圆弧的地方，几个知识点：

border-left/right-color （左右框颜色）

border-top/bottom-color（上下框颜色）

animation-duration（执行动画一个周期的时间）
