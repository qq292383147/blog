---
title: SVG超简单实现豆瓣loading动画
date: 2019-11-02 19:02:50
tags: css
categories: css
---

这段时间在豆瓣上看有什么剧的时候，发现豆瓣的loading动画还挺棒的。所以决定模仿着来写一个。



![效果图](F:\图片库blog/picture_images/picture/css/88.gif)



我通过`CSS3`配合`SVG`来完成这次模仿豆瓣的loading动画。没用过`SVG`的也不用慌，我下面会写出相应的属性方便你去理解。因为这个真的超简单。那么我们就直奔主题吧

# 初始化svg

我们需要先完成一个静态的`笑脸`

始化SVG视图的大小

```svg
<svg width="100" height="100"></svg>
```

我指定了一个宽高都为`100px`的区域，`width=”100”`和`width=”100px”`是等价的。

# 画嘴巴

我们把`嘴巴`给画出来，在`svg`内先画一个圆

```svg
<circle class="mouth" cx="50" cy="50" r="14"></circle>
```

`cx` 和 `cy` 属性定义圆点的 `x` 和 `y` 坐标。

**看到浏览器上面多了一个填充的黑色圆点**



![原型](F:\图片库blog/picture_images/picture/css/89.png)



接下来我们给我们的嘴巴加上`css`样式

```less
.mouth {
    fill: none;
    stroke: #00B51D;
    stroke-width: 5;
    stroke-linecap: round;
    stroke-dasharray: 44, 44;
    transform-origin: center;   /* transform动画时以自身中心作为基点 */
}
```

对应的属性

| css属性          | 说明               | 此处             |
| ---------------- | ------------------ | ---------------- |
| fill             | 填充颜色           | none(不填充)     |
| stroke           | 轮廓的颜色         | #00B51D          |
| stroke-width     | 轮廓的宽度         | 5                |
| stroke-linecap   | 开放路径两端的形状 | round            |
| stroke-dasharray | 创建虚线           | 44, 44           |
| transform-origin | 旋转元素的基点位置 | center(自身中心) |

这里重点讲一下`stroke-dasharray`，它的属性值可为`none`、`<dasharray>`和`inherit`。

`<dasharray>`它是一个`<length>`和`<percentage>`数列，数与数之间用逗号或者空白隔开，指定短划线和缺口的长度。

> 一个参数时： 其实是表示虚线长度和每段虚线之间的间距  
>   两个参数或者多个参数时：一个表示长度，一个表示间距

- stroke-dasharray = '10' 表示：虚线长`10`，间距`10`，然后重复 虚线长`10`，间距`10`
- stroke-dasharray = '10, 5' 表示：虚线长`10`，间距`5`，然后重复 虚线长`10`，间距`5`
- stroke-dasharray = '20, 10, 5' 表示：虚线长`20`，间距`10`，虚线长`5`，接着是间距`20`，虚线`10`，间距`5`，之后开始如此循环

**根据圆的周长公式L=2πr，圆的半径r=14，所以L=87.96452≈88，那么我们取虚线长度为44，间距44做一条虚线，刚好就是圆周长的一半。**

可见此时我们的`嘴巴`部分已经完成了



![原型](F:\图片库blog/picture_images/picture/css/90.png)



# 画眼睛

接下来开始画`眼睛`，我又画了一个`circle`。

```svg
<circle class="eye" cx="50" cy="50" r="14"></circle>
```



![原型](F:\图片库blog/picture_images/picture/css/91.png)



**我们依然可以通过stroke-dasharray来画出一对眼睛**

先把`嘴巴`注释掉，避免影响我们调试。

**stroke-dasharray的虚线长度为0的时，则可以得到无数个点状的圆。根据上面圆的周长公式我们可以得到周长为88，那么我们每1/4个长度就为22，此时我们再把间距调整为66。此时两个点的垂直距离刚好为90度**

接下来我们给我们的眼睛加上`css`样式

```less
.eye {
    fill: none;
    stroke: #00B51D;
    stroke-width: 5;
    stroke-linecap: round;
    stroke-dasharray: 0, 66;
}
```



![原型](F:\图片库blog/picture_images/picture/css/92.png)



为了让嘴巴对齐，我们左旋转`45度`，给`eye`加上`transform`属性

```less
transform-origin: center;
transform: rotate(-45deg);
```



![原型](F:\图片库blog/picture_images/picture/css/93.png)



这样子我们就完成了`眼睛`了

# 加动画

经过我无数遍慢放（一帧一帧）的观察豆瓣的加载动画，终于找到了规律（哭）。

## 嘴巴动画

加动画效果，这也是最激动的一步，我们先来看下`嘴巴`部分



![原型](F:\图片库blog/picture_images/picture/css/94.gif)



通过动画我们可以看出`嘴巴`部分是旋转了`两圈`的，并且在旋转`第一圈`的时候，两边的间距缩小为`1/4`，在`第二圈`的时候，间距恢复为`1/2`，且最后有一段的`停留时间`。

**根据最后的一段停留时间和旋转两圈**

我们可以通过`transform`完成，简单

```less
@keyframes mounthAni {
    80%, 100% {
        transform: rotate(720deg);
    }
}
```

**第一圈的时候两边间距缩小为1/4，也就是此时stroke-dasharray的值为 44, 22，后续再恢复为1/2**

```less
@keyframes mounthAni {
    40% {
        stroke-dasharray: 44, 22;   /* 间距改为1/4 */
    }
    80%, 100% {
        stroke-dasharray: 44, 44;   /* 间距恢复为1/2 */
        transform: rotate(720deg);
    }
}
```

动画的运行速度为**开始快，结束慢**，所以我们使用`ease-out`作为**贝塞尔曲线函数值**

这样`嘴巴`的动画就完成了

## 眼睛动画



![原型](F:\图片库blog/picture_images/picture/css/95.gif)



同样的，通过动画我们可以看出`眼睛`部分同样是旋转了`两圈`，并且在旋转`第一圈`的时候，两边的间距增大为`7/8`，在`第二圈`的时候，间距恢复为`3/4`，且最后有一段的`停留时间`。

```less
@keyframes eyeAni {
    40% {
        stroke-dasharray: 0, 77;    /* 间距改为7/8 */
    }
    80%, 100% {
        transform: rotate(675deg);  /* 间距恢复为3/4 */
        stroke-dasharray: 0, 66;
    }
}
```

动画的运行速度为**开始和结束慢**，所以我们使用`ease-in-out`作为**贝塞尔曲线函数值**

至此我们的`眼睛`动画也就完成了

我们把两个动画整合起来，这样就完成了模仿豆瓣的loading动画了，特简单。



![效果图](F:\图片库blog/picture_images/picture/css/96.gif)



# 源码

*html*

```svg
<svg width="100" height="100">
    <circle class="mouth" cx="50" cy="50" r="14"></circle>
    <circle class="eye" cx="50" cy="50" r="14"></circle>
</svg>
```

*css*

```less
.mouth {
    fill: none;
    stroke: #00B51D;
    stroke-width: 5;
    stroke-linecap: round;
    stroke-dasharray: 44, 44;
    transform-origin: center;   /* transform动画时以自身中心作为基点 */
    animation: mounthAni 2.3s ease-out infinite;
}

.eye {
    fill: none;
    stroke: #00B51D;
    stroke-width: 5;
    stroke-linecap: round;
    stroke-dasharray: 0, 66;
    transform-origin: center;
    transform: rotate(-45deg);
    animation: eyeAni 2.3s ease-in-out infinite;
}

@keyframes mounthAni {
    40% {
        stroke-dasharray: 44, 22;   /* 间距改为1/4 */
    }
    80%, 100% {
        stroke-dasharray: 44, 44;   /* 间距恢复为1/2 */
        transform: rotate(720deg);
    }
}

@keyframes eyeAni {
    40% {
        stroke-dasharray: 0, 77;    /* 间距改为7/8 */
    }
    80%, 100% {
        transform: rotate(675deg);  /* 间距恢复为3/4 */
        stroke-dasharray: 0, 66;
    }
}
```

# 总结

`CSS3`动画已足够强大，但是如果要实现上面那种间距可`变大变小`的动画效果，只用`CSS`的话我还是没有想到怎么实现，如果各位有方法的话欢迎评论告诉我😀，所以使用了`SVG`加`CSS`来完成，`眼睛`部分原本想过使用`animateMotion`来完成，奈何看了半天还是不会用🤣，所以就想着只用`CSS`的动画效果完成了这次的动画，没想到意外的简单，所以把方法分享给大家。整个loading动画都围绕着`stroke-dasharray`展开，用到的`SVG`属性真的是冰山一角，上面的内容如果有什么错误的话还望各位多多指教。