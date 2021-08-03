---
title: vue中css样式（补充）
date: 2021-08-03 09:55:26
tags: vue
categories: vue
---

### 一、动态使用样式

使用场景：根据不同的值使用不同的样式，或者给样式某个属性设置一个变量值

使用方法：

**使用不同的class**

```less
    :class=" {  'classA' : f，'classB'：g } "
	//条件f成立则使用style标签中定义好的classA样式，条件g成立则使用classB样式
```



使用style设置某个变量的值

```less
:style="{'width':widthLength+'px'}"   //给width一个变量值widthLength
```



使用计算属性 `calc(100% - 100px)`
一般只能计算宽度高度，注意中间的减号“-”，前后一定要加空格，并且父级的高度宽度一定要有，可以100%，否则使用无效。

 

#### 二、全局公共 `css` 样式文件

提醒：`vue` 工程中 `css` 文件和 `js` 文件最好都放在 `static` 文件夹下面，可以降低报错的概率。

2.1 `main.js` 中引入
在入口js文件 `main.js` 文件中引入。

```js
import Vue from 'vue'
import App from './App'
import router from './router'
import ElementUi from 'element-ui'
import '../common/mainStyle.css'   //引入全局样式

Vue.config.productionTip = false
Vue.use(ElementUi);
/* eslint-disable no-new */
new Vue({
    router,
    render: h => h(App)
}).$mount('#app');
```



2.2  `index.htm` l引入

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>styletest</title>
    <link rel="stylesheet" href="./static/css/global.css"> /*引入公共样式*/
  </head>
  <body>

    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```




#### 三、单个vue文件中引入样式

`vue` 文件 `style` 标签中 `import` 引入样式：

```less
@import "../assets/common/common.css";//自定义.css的样式路径
```



#### 四、样式作用范围控制

很多时候，我们希望样式只在当前组件生效，样式可以私有化，避免影响其他的组件，造成全局的样式污染。

4.1 `scoped` 私有作用域
在 `style` 标签中添加 `scoped` 属性，可以使样式只在当前的组件中生效，样式私有化。

```less
<style scoped>
.example {
  color: red;
}
</style>
```

原理：

其原理是在编译的时候，会给每个组件中的所有的 `dom` 节点样式添加一个唯一的data属性。



#### 4.2 混合使用

在一个组件中同时使用 `scoped` 和非 `scoped` 样式。特别是对第三方组件样式的修改，想修改第三方组件的样式，又不想去掉 `scoped` 属性，影响别的组件。

```less
<style>
/* 全局样式 */
/* 将修改第三方组件的样式写在这里 */
/* 组件的最外层标签定义一个唯一类，最好将样式都写在这个类名下，以防组件间互相影响 */
</style>

<style scoped>
/* 本地样式 */
</style>
```

#### 4.3 深度作用选择器
如果希望 `scoped` 样式中的一个选择器能够作用的更深，例如影响子组件，可以使用 `>>>` 操作符。


```css
<style scoped>
    .a >>> .b { /* ... */ }
</style>
```

### 备注1：别名

**/deep/是>>>的别名**

像sass之类的预处理器无法正确解析>>>。可以使用/deep/替代

```css
<style scoped>
    .a /deep/ .b { /* ... */ }
</style>
```

备注2：深度选择器修改第三方组件样式

在第三方组件内部类外面套个类，再利用深度选择器这样可以修改样式，且不影响其他组件

```css
<style scoped>
    外层组件类 >>> 第三方组件内部类 {
        样式
    }
</style>
```

#### 4.4 动态生成的 `dom` 的样式

通过 `v-html` 创建的 `DOM` 内容不受 `scoped` 样式影响，但是仍然可以通过深度作用选择器来设置样式。





原文链接：https://blog.csdn.net/happy81997/article/details/103582699
