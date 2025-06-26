---
title: react-router 去中心化式路由
date: 2019-05-24 10:28:48
tags: React & React Native
categories: React & React Native
---

![](https://qq292383147.github.io/pictureLibrary/picture/React/React-router-logo.jpg)


## 1.静态路由 vs. 动态路由

在Web前端开发中，我们经常会需要处理页面路由问题。习惯上，路由信息会在一个地方集中配置好，我们可以称之为“`静态路由`”，或者叫“`中心化式路由`”。以react-router v3版本为例，代码类似下面这样：


```js
import { Router, Route, IndexRoute, browserHistory } from 'react-router'

const App = () => (
  <Router history={browserHistory}>
    <Route path="/" component={RootPage}>
      <IndexRoute component={HomePage} />
      <Route path="/users" component={UsersPage} />
    </Route>
  </Router>
)

render(<App />, document.getElementById('app'))


```

可以看到，在程序的顶层组件上配置好了所有路由信息，并通过嵌套关系体现不同的层次。但是，react-router v4版本进行了革命性的改动，使之更加符合React的“组件化”思想，我们可以称之为“`动态路由`”，或者借用区块链中的术语，称之为“`去中心化路由`”。用v4版本改写后的代码类似于下面这样：


```js
import { BrowserRouter, Route } from 'react-router-dom'

const App = () => (
  <BrowserRouter>
    <RootPage />
  </BrowserRouter>
)

const RootPage = () => (
  <div>
    <Route path="/" exact component={HomePage} />
    <Route path="/users" component={UsersPage} />
  </div>
)

render(<App />, document.getElementById('app'))

```

可以发现，路由的配置不再是全部位于顶层组件中了，而是分散在不同的组件中，通过组件的嵌套关系来实现路由的层次。另外，和静态路由事先定义好所有页面不同，动态路由可以在渲染时根据路径匹配结果，动态决定渲染哪些组件，这样就可以<font color="#f00">充分实现页面的复用，减少重复渲染</font>。下面依次介绍react-router v4的相关组件。


## 2.Router
react-router内部实际上是利用了浏览器的history API，因此在v3版本中我们需要在顶层的<Router>组件中传入一个history属性。在v4版本中为我们封装了一个<BrowserRouter>组件，我们需要把它包在所有组件的最外层：

```js
  import { BrowserRouter } from 'react-router-dom'
  const App = () => (
    <BrowserRouter>
      ... ...
    </BrowserRouter>
  )
```

另外还有一个<HashRouter>组件，是为了兼容以前版本的浏览器，已经不推荐使用了。

## 3.路由匹配

路由匹配主要涉及两个组件：`<Route>`和`<Switch>`，下面分别介绍。

### 3.1 <Route>

`<Route>`组件包含3类属性：<font color="#f00">匹配属性、渲染方法、路由属性。</font>


### 3.1.1 匹配属性

<font color="#f00">这些属性是为了设定url匹配规则。</font>

#### (1) path：路由匹配正则表达式

举例：

```
<Route path='/' />：匹配以/开头的路径，比如/，/login，/login/alice
<Route path='/login/:username' />：可以匹配/login/alice，参数可以通过props.match.params.username获得
```

#### (2) exact：精确匹配

举例：

```
<Route path='/' exact />：只能精确匹配/，不能匹配/login
在v4版本里取消了<IndexRoute>组件，因此如果你希望在根路径显示某个页面的话，可以用下面的方式：
```

```js
<div>
  <Route path="/" exact component={HomePage} />
  ... ...
</div>
```

### (3) strict：严格匹配

如果path的最后带有/，那么url必须也带有/才能匹配。举例：

<Route path='/login/' strict />：可以匹配/login/，不能匹配/login

### (4) sensitive：大小写敏感


## 3.1.2 渲染方法

<font color="#f00">这些属性指明在匹配上路由后如何渲染。</font>

#### (1) component：渲染组件
这是最常见的方式，路由匹配时渲染一个指定组件

```
<Route path='/users' component={UsersPage} />
```

#### (2) render：内联渲染

`component`方式会通过`React.createElement`创建新元素，然后`mount`到`DOM`上，如果需要频繁更新的话这种方式效率会比较低，这时候你可以选择内联渲染方式。

```js
  <Route path='/users' render={props => (
    <div>
      <Component {...props}/>
    </div>
  )}/>
```

### (3) children：根据path匹配结果渲染子元素
前面两种渲染方法都是只有path匹配时才渲染，`children`渲染方式则比较特殊，它是针对子元素的，并且只返回一个`match`结果，你可以根据`match`结果自行决定如何渲染子元素。举个例子，在一个列表中，我们希望高亮那些被匹配上的元素：
```js
  <ul>
    <ListItemLink to="/somewhere" />
    <ListItemLink to="/somewhere-else" />
  </ul>;

  const ListItemLink = ({ to, ...rest }) => (
    <Route
      path={to}
      children={({ match }) => (
        <li className={match ? "active" : ""}>
          <Link to={to} {...rest} />
        </li>
      )}
    />
  );
```

### 3.1.3 路由属性

这些属性可以在待渲染组件中通过`props`访问到。

#### (1) match
match属性中包含了路由匹配相关的参数：

params：参数键值对（比如前面的username）
isExact：是否精确匹配（是否指定了exact）
path：正则表达式（如/login/:username）
url：和path匹配上的部分（入/login/alice）

#### (2) location
location中包含了当前url相关的参数：

pathname：当前url
search：url中的查询字符串（如?username=a&sort=b）
state：携带的特定状态参数，是一个对象（如{ XXX: 'xxx' }）

#### (3) history
history就是浏览器提供的history API，提供了一些路由函数：

`push(path, [state])`：页面跳转
`replace(path, [state])`：重定向
`go(n)`：直接跳转到第n个页面
`goBack()`：等价于go(-1)
`goForward()`：等价于go(1)

### 3.2 Switch
如果我们希望设置一系列的路由匹配规则，只渲染第一个匹配上的组件，该如何实现呢？这时候你就需要用到<Switch>组件。<font color="#f00">`<Switch>`中包含一组`<Route>`或者`<Redirect>`，只渲染第一个匹配的路由。</font>


```js
  import { Switch, Route } from 'react-router'

  <Switch>
    <Route exact path="/" component={Home}/>
    <Route path="/about" component={About}/>
    <Route path="/:user" component={User}/>
    <Route component={NoMatch}/>
  </Switch>
```

### 4.导航

`react-router`提供了一系列的导航组件，基本上就是`<a>`标签的一个封装。主要包括3种：

`<Link>`：最终渲染为`<a>`
`<NavLink>`：path匹配时显示为高亮样式
`<Redirect>`：重定向

举例：

```js
import { Link, NavLink } from 'react-router-dom'

<Link to="/about">About</Link>
<NavLink to="/faq" activeClassName="selected">
  FAQs
</NavLink>
```

另外，`react-router`还提供了其他一些工具库，比如支持组件的动态`import`（下载）的`react-loadable`，支持CSS转场动画的`react-transition-group`

![](https://qq292383147.github.io/pictureLibrary/picture/React/react-router需要的组件.jpg)

