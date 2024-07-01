---
title: CSS实现各种图形
date: 2019-03-31 23:36:30
tags: css
type: css
categories: css
---

<center><font color="#B452CD" size="9">三角形</font></center>

![img](F:\图片库blog/picture_images/picture/css/13.jpg)

### css
```css
    .triangle {
      width: 0;
      height: 0;
      border: 50px solid blue;
      /* 通过改变边框颜色，可以改变三角形的方向 */
      border-color: blue transparent transparent transparent;
      margin: 0 auto;
    }
```

### html
```html
<div class="triangle"></div>
```


<center><font color="#B452CD" size="9">梯形</font></center>

![img](F:\图片库blog/picture_images/picture/css/14.jpg)

### css
```css
.trapzoid {
      width: 40px;
      height: 100px;
      border: 50px solid burlywood;
      border-color: transparent transparent burlywood transparent;
      margin: 0 auto;
    }
```

### html
```html
  <div class="trapzoid"></div>
```



<center><font color="#B452CD" size="9">椭圆</font></center>

![img](F:\图片库blog/picture_images/picture/css/15.jpg)

### css
```css
.ellipse {
   width: 200px;
   height: 100px;
   border-radius: 50%;
   background: rgb(122, 234, 200);
   margin: 30px auto;
  }
```

### html
```html
<div class="ellipse"></div>
```



<center><font color="#B452CD" size="9">球体</font></center>

![img](F:\图片库blog/picture_images/picture/css/16.jpg)

### css
```css
  .sphere {
    height: 200px;
    width: 200px;
    border-radius: 50%;
    background: radial-gradient(circle at 70px 70px, #5cabff, #000);
    margin: 20px auto;
  }
```

### html
```html
<div class="sphere"></div>
```



<center><font color="#B452CD" size="9">半圆</font></center>

![img](F:\图片库blog/picture_images/picture/css/17.jpg)

### css
```css
.semicircle {
      width: 10%;
      height: 100px;
      /* 前四个值表示圆角的水平半径，后四个值表示圆角的垂直半径 */
      border-radius: 200% 0 0 200% / 100% 0 0 100%;
      /* 效果和用%一样 */
      /* border-radius: 50px 0 0 50px; */
      background: rgb(170, 11, 149);
      margin: 0 auto;
    }
```

### html
```html
<div class="semicircle"></div>
```



<center><font color="#B452CD" size="9">菱形</font></center>

![img](F:\图片库blog/picture_images/picture/css/18.jpg)

### css
```css
  .rhombus {
    width: 100px;
    height: 100px;
    transform: rotateZ(45deg) skew(30deg, 30deg);
    background: rgb(23, 55, 52);
    margin: 100px auto;
  }
```

### html
```html
<div class="rhombus"></div>
```



<center><font color="#B452CD" size="9">扇形</font></center>

![img](F:\图片库blog/picture_images/picture/css/19.jpg)

### css
```css
  .sector {
    width: 142px;
    height: 142px;
    background: #fff;
    border-radius: 50%;
    background-image: linear-gradient(to right, transparent 50%, #655 0);
    margin: 0 auto;
  }

  .sector::before {
      content: "";
      display: block;
      margin-left: 50%;
      height: 142px;
      width: 100%;
      background-color: inherit;
      transform-origin: left;
      /* 调整角度，改变扇形大小 */
      transform: rotate(100deg);
    }
```

### html
```html
 <div class="sector"></div>
```



<center><font color="#B452CD" size="9">五边形</font></center>

![img](F:\图片库blog/picture_images/picture/css/20.jpg)

### css
```css
  .pentagonal {
    width: 100px;
    position: relative;
    border-width: 105px 50px 0;
    border-style: solid;
    border-color: blueviolet transparent;
    margin: 50px auto;
  }

  .pentagonal:before {
      content: "";
      position: absolute;
      width: 0;
      height: 0;
      top: -185px;
      left: -50px;
      border-width: 0px 100px 80px;
      border-style: solid;
      border-color: transparent transparent blueviolet;
    }
```

### html
```html
<div class="pentagonal"></div>
```



<center><font color="#B452CD" size="9">六边形</font></center>

![img](F:\图片库blog/picture_images/picture/css/21.jpg)

### css
```css
.hexagon {
      width: 200px;
      height: 100px;
      background-color: #000;
      position: relative;
      margin: 0 auto;
    }

    .hexagon:before {
      content: "";
      position: absolute;
      top: -60px;
      left: 0;
      width: 0;
      height: 0;
      border-left: 100px solid transparent;
      border-right: 100px solid transparent;
      border-bottom: 60px solid #000;
    }

    .hexagon::after {
      content: "";
      left: 0;
      width: 0;
      height: 0;
      bottom: -60px;
      position: absolute;
      border-left: 100px solid transparent;
      border-right: 100px solid transparent;
      border-top: 60px solid #000;
    }
```

### html
```html
  <div class="hexagon"></div>
```



<center><font color="red" size="9">心形</font></center>

![img](F:\图片库blog/picture_images/picture/css/22.jpg)

### css
```css
.heart {
      width: 100px;
      height: 100px;
      transform: rotateZ(45deg);
      background: red;
      margin: 100px auto;
    }

    /* 心形是由两个圆形和一个矩形进行组合得到的。 */
    .heart::after,
    .heart::before {
      content: "";
      width: 100%;
      height: 100%;
      border-radius: 50%;
      display: block;
      background: red;
      position: absolute;
      top: -50%;
      left: 0;
    }

    .heart::before {
      top: 0;
      left: -50%;
    }
```

### html
```html
<div class="heart"></div>
```



<center><font color="#B452CD" size="9">长方体</font></center>

![img](F:\图片库blog/picture_images/picture/css/23.jpg)

### css
```css
/* 长方体是由六个矩形进行组合得到的 */
    .cuboid {
      width: 200px;
      height: 200px;
      transform-style: preserve-3d;
      transform: rotateX(-30deg) rotateY(-80deg);
      margin: 100px auto;
    }

    .cuboid div {
      position: absolute;
      width: 200px;
      height: 200px;
      opacity: 0.8;
      transition: .4s;
    }

    .cuboid .front {
      transform: rotateY(0deg) translateZ(100px);
      background: #a3daff;
    }

    .cuboid .back {
      transform: translateZ(-100px) rotateY(180deg);
      background: #a3daff;
    }

    .cuboid .left {
      transform: rotateY(-90deg) translateZ(100px);
      background: #1ec0ff;
    }

    .cuboid .right {
      transform: rotateY(90deg) translateZ(100px);
      background: #1ec0ff;
    }

    .cuboid .top {
      transform: rotateX(90deg) translateZ(100px);
      background: #0080ff;
    }

    .cuboid .bottom {
      transform: rotateX(-90deg) translateZ(100px);
      background: #0080ff;
    }
```

### html
```html
<div class="cuboid">
    <!-- 前面 -->
    <div class="front"></div>
    <!-- 后面 -->
    <div class="back"></div>
    <!-- 左面 -->
    <div class="left"></div>
    <!-- 右面 -->
    <div class="right"></div>
    <!-- 上面 -->
    <div class="top"></div>
    <!-- 下面 -->
    <div class="bottom"></div>
  </div>
```



<center><font color="#B452CD" size="9">圆柱体</font></center>

![img](F:\图片库blog/picture_images/picture/css/24.jpg)

### css
```css
.cylinder {
      position: relative;
      transform: rotateX(70deg);
      margin: 0 auto;
    }

    .ellipse {
      width: 100px;
      height: 100px;
      background: deepskyblue;
      border-radius: 50px;
    }

    .rectangle {
      width: 100px;
      height: 400px;
      position: absolute;
      opacity: 0.6;
      background: deepskyblue;
      top: 0;
      left: 493px;
      border-radius: 50px;
      z-index: -1;
    }
```

### html
```html
<div class="cylinder">
    <div class="ellipse"></div>
    <div class="rectangle"></div>
  </div>
```



<center><font color="#B452CD" size="9">棱锥</font></center>

![img](F:\图片库blog/picture_images/picture/css/25.jpg)

### css
```css
.pyramid {
      width: 200px;
      height: 200px;
      transform-style: preserve-3d;
      transform: rotateX(-30deg) rotateY(-80deg);
      margin: 0 auto;
    }

    .pyramid div {
      position: absolute;
      top: -100px;
      width: 0px;
      height: 0px;
      border: 100px solid transparent;
      border-bottom-width: 200px;
      opacity: .8;

    }

    .pyramid .front {
      transform: translateZ(100px) rotateX(30deg);
      border-bottom-color: #a3daff;
      transform-origin: 0 100%;
    }

    .pyramid .back {
      transform: translateZ(-100px) rotateX(-30deg);
      border-bottom-color: #1ec0ff;
      transform-origin: 0 100%;
    }

    .pyramid .left {
      transform: translateX(-100px) rotateZ(30deg) rotateY(90deg);
      border-bottom-color: #0080ff;
      transform-origin: 50% 100%;
    }

    .pyramid .right {
      transform: translateX(100px) rotateZ(-30deg) rotateY(90deg);
      border-bottom-color: #03a6ff;
      transform-origin: 50% 100%;
    }

    .pyramid .bottom {
      transform: translateX(-100px) rotateZ(90deg) rotateY(90deg);
      background: cyan;
      width: 200px;
      height: 200px;
      border: 0;
      top: 0;
      transform-origin: 50% 100%;
    }
```

### html
```html
<!-- 棱锥是由四个三角形和一个矩形进行组合得到的 -->
  <div class="pyramid">
    <!-- 前面 -->
    <div class="front"></div>
    <!-- 后面 -->
    <div class="back"></div>
    <!-- 左面 -->
    <div class="left"></div>
    <!-- 右面 -->
    <div class="right"></div>
    <!-- 下面 -->
    <div class="bottom"></div>
  </div>
```

