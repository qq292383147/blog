---
title: CSS第四级选择器
date: 2019-11-13 19:28:50
tags: css
categories: css
---



选择器是 CSS 的核心部分。你用来做一些操作比如说选择某种类型的所有元素，就像下面这样：

```less
div {/* 一些应用在所有 div 元素上的样式 */}
```

或者你可以选择一个在它的父元素下的最后一个子元素：

```less
ul li:last-child {/* 一些只应用在列表的最后一个子元素上的样式 */}
```

当然，你也可以去做一些更复杂的事情，比如说选择选择列表中除了最后一个子元素之外的所有子元素。

事实上，这样做的方法不止一种，一些方法甚至更复杂。

例如，比较以下这两个：

```less
ul li {/* 一些应用在所有子元素上的样式 */}
ul li:last-child {/* 一些样式用来重置上面生效的样式，因为上面的样式不适用于上面最后一个子元素 */}
ui li:nth-last-child(n+2) {/* 一些应用在除了最后一个子元素之外的所有子元素上面的样式 */}
```

ul li属于第一级选择器。

`last-child`和 `nth-last-child`属于第三级选择器。

你可以把级别看作是 CSS 选择器的版本，其中每个级别都会添加一些功能更强大的选择器。

在这篇文章中，我会根据截至 2019 年 1 月的草案规范，和你一起过一遍下一代选择器（第四级），主要有以下分类：

- 逻辑组合
- 属性选择器
- 语言伪类
- 位置伪类
- 用户操作伪类
- 输入伪类
- 树结构伪类
- 网格结构伪类

在我写这篇文章的时候，第四级选择器的规范还处于草案阶段。直到官方推荐之前，它可能还会改，而且你可能还会发现很多选择器甚至都还没有被一些浏览器支持或者需要添加一些前缀（ `:-moz-`或 `:-webkit-`）。

对于每一个选择器，我都会提供一个can I use的链接以便你可以看到哪些浏览器支持它（如果有的话）、一些简短的介绍、一个例子、和一个 Codepen 的链接，这样你就能自己去尝试一下（即使它暂时无法使用，因为将来可能会改）。

好了，让我们中逻辑组合选择器开始。

## 逻辑组合选择器

这个类别包括通过组合选择其他选择器而起作用的选择器。

```less
:not(selector1,selector2,...)

它选择那些与传入的参数不匹配的元素列表。例如：

p:not(.beginning, .middle){ color: red; }
```

这会给所有的没有 .beginning和 .middle类的p元素设置颜色为红色的样式。

这个选择器的第三级版本只能允许一个选择器，而不是两个或更多的的选择器。例如，上面的样式可以写成：

```less
p:not(.beginning):
not(.middle){  color: red; }

:is(selector1,selector2)
```



它选择那些与传入的参数匹配的元素列表。例如：

```less
p:is(.beginning, .middle){ color: blur; }
```



这会给所有的具有 `.beginning`和 `.middle`类的p元素设置颜色为蓝色的样式。

自从上一个工作草案版本以来最重大的变化之一就是 :matches()选择器被更名为 :is()并且已经被 Safari（唯一一个完全支持这个选择器的浏览器）弃用，因此它和与之相反的选择器 :not()可以更好的配对。

如果要向后兼容，可以用 :is()作为 :matches()的别名。

然而， `:matches()`以前叫做 `:any()`，因此大多数浏览器都支持带前缀的伪类：

```less
p:-webkit-any(.beginning, .middle){ color: blue; }

p:-moz-any(.beginning, .middle) { color: blue; }

:where(selector1,selector,...)
```



在我写这篇文章的时候，还没有任何一个浏览器支持这个选择器。

它具有和 `:is()`相同的语法和功能，但是不管这个选择器接受多少个参数，这个选择器的权重都是 0。

权重是 CSS 的应用规则。如果两个选择器同时应用在同一个元素上面，则权重高的那个生效。如果不同规则具有相同的权重，那么应用在这个元素上的最后一个规则将会生效。

这个选择器可以用来实现筛选和覆盖与之关联的元素的样式。

下面是一个权重的例子：

```less
a:not (:hover) { text-decoration: none; }

nav a { /* 不会生效 */
text-decoration: underline; }
/* 使用新的第四级选择器 :where */

a:where(:not(:hover)) { text-decoration: none; }

nav a { /* 生效 */
text-decoration: underline;}
:has(reslativeSelector1,reslativeSelector2,...)
```

浏览器支持（在写这篇文章的时候，还没有任何一个浏览器支持这个选择器）

这个选择器将一个相对选择器列表作为参数。它选择那些在指定范围内匹配相对选择器列表的元素。

例如：

```less
p:has(strong, em) { color: red; }
```



这会给所有的包含` <strong>`或者 `<em>`元素的p元素添加一个颜色为红色的样式。



## 属性选择器

这类选择器包含那些应用在元素属性上的选择器。

```less
[foo="bar"i]
```

它选择那些foo属性的值等于bar的元素，忽略大小写。

例如：

```less
p[class="text" i] {  color: green;}
```

这会给所有的class属性的值为Text、TEXT、或者是text、又或者是其他组合的p元素添加一个颜色为绿色的样式。

```less
[foo="bar"s]
```

在我写这篇文章的时候，还没有任何一个浏览器支持这个选择器。

它选择那些foo属性的值严格等于bar的元素。

例如：

```less
p[class="text" s]{  color: green;}
```

这会给所有class属性的值为text（例如，不是Text）的p元素添加一个颜色为绿色的样式。



## 语言伪类？

这类选择器包括那些使用语言相关设置的选择器。

```less
:dir(ltr)
```

它选择那些具有从左到右方向性的元素，其中文档语言指定如何确定方向性。与之对应的：`:dir(rtl)`表示具有从右到左方向性的元素。其他值是无效的也不会匹配任何元素。

例如：

```less
p:dir(rtl) {  background-color: red;}
```

这会给设置了从左到右方向的p元素添加一个背景色为红色的样式。

```less
:lang(zh,"*-hant")
```

在我写这篇文章的时候，还没有任何一个浏览器支持这个第四级选择器。

它选择那些被标记为中文的元素（或者选择其他语言标记的元素，只需要把zh改为其他的语言代码就可以了）或者用繁体字书写的元素（或者在其他字符的系统中，将-hant替换为其它字符代码）。

实际上，第二级选择器里面就有这个选择器，但是在第四级选择器里面新增了通配符和逗号分隔列表。

它接收一个或多个以逗号为分隔的语言代码作为参数。如果语言代码里面包含 `*，则必须对它们进行正确的转义（:lang(es-*)）或字符串引号（:lang("es-*")）`。

例如：

```less
p:lang("*-CH") {  background-color: red;}
```

这会给所有被标记为使用瑞士语言的p元素添加一个背景色为红色的背景色。



## 位置伪类

这类选择器包括那些与超链接有关得选择器。

```less
:any-link
```

在Can I use上并没有这个选择器的兼容性介绍，但是大多数主流浏览器都支持这个选择器。

它选择那些具有href属性的元素（例如 `<a>`或 `<link>`。或者说，所有与 `:link`或 `:visited`伪类匹配的元素。

例如：

```less
a:any-link {  color: red;}
```

这会给所有具有`href`属性的的所有a元素添加一个颜色为红色的样式。

```less
:local-link
```

在我写这篇文章的时候，还没有任何一个浏览器支持这个第四级选择器。

它选择那些链接到当前 URL 的元素。如果链接的指向包括 URL 片段，则 URL 片段和和当前 URL 也必须要匹配。比如不匹配，则在比较中不考虑当前 URL 的片段 URL 部分。

例如：

```less
a:local-link {  text-decoration: none;}
```

这会给所有的具有`href`属性的指向当前页面的a元素（也许它们是导航菜单的一部分）去掉下划线。

## 用户操作伪类

这类选择器包括那些用户正在操作的元素的选择器。

```less
:focus-within
```

它选择那些与 `:focus`伪类匹配的元素（当元素具有焦点时）或具有与 `:focus`匹配的子元素。

例如，使用如下的一个表单：

```html
<from><inputtype="text"id="name"placeholder="Enter your name"/></from>
```

当表单里的输入框获得焦点的时候，它会给表单添加一个边框。

```less
:focus-visible
```

它选择一个处于焦点状态的元素（与 `:focus`伪类匹配），浏览器通常会为了让获得焦点的元素清晰可见，给它添加一个焦点环。

和 `:focus`的区别和细微。

如果 `:focus-visible`匹配了， `:focus`一定会匹配，但是反过来就不一定了，它取决于浏览器（如果启用了聚焦环的绘制）和获取焦点的元素（通过鼠标点击或者 tab 键）。

Firefox 把这个选择器实现为 `:-moz-focusring`伪类。

例如，在某些场景下，有以下样式：

```less
/* 标准第四级选择器 */
:focus-visible {  background-color: lightgary;}
/* 基于 Firefox 的第四级选择器 */
:moz-focusring {  background-color: lightgary;}
```

只有在元素通过 tab 获得焦点的时候才会生效。

## 输入伪类

这类选择包括那些应用于接受用户输入的元素的选择器。

```less
:read-write and:read-only
```

`:read-write`选择可读可写的元素（例如那些不具有 readonly属性的 `<input>`的元素）。

`:read-only`选择那些只能读的元素（例如具有readonly属性的 `<input>`的元素）。

然而，这些选择器不仅仅选择 `<input>`或 `<textarea>`元素，它们也可以选择用户能输入的任何选择，例如将contenteditable属性设置为true的 `<p>`元素。

例如：

```less
:read-write {  background-color: lightyellow;}
:read-only {  background-color: lightgary;}
/* Firefox */
:-moz-read-write {  background-color: lightyellow;}
:moz-read-only {  background-color: lightgary;}
```

这会把页面上所有的不可编辑元素背景色设置为浅灰色，把可以编辑的元素的背景色设置为浅黄色。

```less
:placeholder-shown
```

它选择一个当前正在显示占位符文本的输入框元素。

例如：

```less
input:placeholder-shown {  color: red;}
```

这会给当前显示占位符文本的input元素设置一个颜色为红色的样式，注意这里设置的只是光标的颜色。

```less
:default
```

它选择那些在一组相关元素里面作为默认选项的元素。通常用于按钮和选择列表 / 菜单。

例如：

```less
input:default{  box-shadow: 002px2px green;}
input:defaut + lable {  color: green;}
```

这会给默认 `<input>`元素的标签设置绿色阴影和颜色。

```less
:indeterminate
```

它选择那些处于不确定状态的元素。例如，单选框组和复选框组里包含的那些未被选中的元素，或者进度百分比未知的进度条。

例如：

```less
input[type="radio"]:indeterminate + label {  color: red;}
```

如果组中还没有任何一个元素被选，。这会给这个组的标签添加一个颜色为红色的样式。

```less
:valid` 和 `:invalid
```

它选择那些根据有效性语义或值的有效或无效的元素。如果没有定义值的有效性规则，则这个元素既不满足 `:valid`也不满足 `:invalid`。

例如：对于一个输入类型为email的元素：

```less
input:invalid {  color: red;}input:valid {  color: green;}
```

这会根据元素里面输入的电子邮件是否有效为依据去为元素的文本设置不同颜色。

`:in-range` 和 `:out-of-range`

这些选择器只适用于那些具有范围限制的元素，例如，定义了最大最小值的元素。如果没有定义，则都不匹配。

例如：一个设置了最小只为 1 最大值为 5 的输入框。

```less
input:out-of-range {  color: red;}
input:in-range {  color: green;}
```

这会给依据输入的值设置不同的颜色样式。

在某些情况下，某些选择器会具有与 `:valid`和 `:invalid`相同的效果。

```less
:required`和 `:optional
```

这些选择器分别适用于在提交表单的之前必填的和选填的表单元素。那些非表单元素不会被匹配。

例如：

```less
input:optional {  color: gray;}input:required {  color: red;}
```

这会给那些必填的元素添加设置红色的样式，给非必填的元素添加灰色的样式。

## 树结构伪类

这类选择器包括那些允许基于文档树中的信息进行选择，但是不能由其它选择器表示的选择器，例如元素相对于其父元素的位置。

```less
:nth-child(n[of selector]?)`和 `:nth-last-child(n[of selector]?)
```

浏览器支持（在我写这篇文章的时候，还没有任何一个浏览器支持这个第四级选择器。）

`:nth-child`选择器匹配作为其父级的第 n 个子元素。`:nth-last-child`也一样的，只不过它是从最后一个元素开始计数的。你可以使用:nth测试来了解它们之间的区别，并进一步了解 An+B 表示法。

在这篇文章的开头，我举了一个 `:nth.last-child`的例子，我说这个第三级的选择器。然而，对于第四级选择器，这个选择器接收一个可选的of选择器用来筛选仅与该选择器匹配的子元素。

除了功能更加强大之外，它的声明方式也可以不同。例如：

```less
li.item:nth-child(-n+2)
```

复制代码选择前面两个具有item类的 `<li>`元素。

它和以下的不同：

```less
:nth-child(-n+2 of li.item)
```

复制代码这会选择前面两个带有item类的 `<li>`元素即使它们并不是列表的前两个元素。

尝试一下（在支持该选择器的浏览器中，例如 Safari）：

## 网格结构伪类

这类选择器包括使用表格的列的选择器。

```less
F || E
```

在我写这篇文章的时候，还没有任何一个浏览器支持这个选择器。

列组合器选择器（||）选择类型 E 的元素，该元素表示表中的单元格并属于由类型 F 的元素表示的列。

例如，有如下表：

![第四级选择器](F:\图片库blog/picture_images/picture/css/97.png)

对于以下样式

```less
col.selected || td {  background-color: lightyellow;}
```

这会给所选列（价格）的单元格（ `<td>`元素）设置浅黄色的背景色。 

```less
:nth-col(An+B)`和 `:nth-last-col(An+B)
```

在我写这篇文章的时候，这个选择器还没有被任何一个浏览器支持。

你可以把这些选择器看作是 `:nth-child`和 `:nth-last-child`的列版本。

`:nth-col(An+B)`选择网格或表格中的一个在该元素之间还有 An+B-1 个元素的元素（n 为 0 或任意一个整数）。

例如：

```less
col.nth-col(1) {  background-color: lightyellow; }
col.nth-last-col(1) {  background-color: lightgreen; }
```

这会给表格的第一列元素添加一个浅黄色背景色，。被最后一列元素添加一个浅绿色背景色。

## 结论

第四级选择器使您可以轻松声明复杂的选择规则。

我们涵盖了2019年1月《编辑器草案》规范中定义的大多数选择器，但是，我遗漏了一些可能会很快消失或很快改变的选择器，或者关于它们的信息不多（除了不受支持） 任何浏览器）：

- :target-within
- :scope（不要将它和作用域样式混淆）
- 时间伪类（你可以在这里了解更多信息）
- :blank
- :user-invalid

但绝对要注意这些以及第4级选择器的其余部分。