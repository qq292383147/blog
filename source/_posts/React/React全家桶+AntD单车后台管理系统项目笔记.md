---
title: React全家桶+AntD单车后台管理系统项目笔记
date: 2019-10-31 21:44:43
tags: React & React Native
categories: React & React Native
---

## React基本介绍

Facebook开源的一个JavaScript库

React结合生态构成的一个`MVVM`框架

### React特点

- Declarative(声明式编码)
- Component-Based(组件化编码)
- 高效-高效的Dom Diff算法，最小化页面重绘
- 单向数据流

### 生态介绍

Vue生态：

```
Vue + Vue-Router + Vuex + Axios + Babel + Webpack
```

React生态：

```
React + React-Router-Redux+Axios + Babel + Webpack
```

## React生命周期介绍

<font color="#f0f">**getDefaultProps**</font>

通过这个方法，来初始化一个Props属性，Props就来自于父组件

<font color="#f0f">**getInitialState**</font>

初始化state，可以直接在constructor中定义this.state

<font color="#f0f">**componentwillMount**</font>

组件加载时只调用，以后组件更新不调用，整个生命周期只调用一次，此时可以修改state

<font color="#f0f">**render**</font>

是一个React组件必须定义的生命周期，用来渲染dom，是使用最多，最重要的放方法

<font color="#f0f">**componetDidMount**</font>

组件渲染之后调用，只调用一次

<font color="#f0f">**componentwillReceiveProps**</font>

组件加载时不调用，组件接受新的props时调用

<font color="#f0f">**shouldComponentUpdate**</font>

组件接收新的props或者state时调用

<font color="#f0f">**componentwillUpdate**</font>

在组件接收新的props或者state但还没有render时被调用，在初始化时不会被调用

<font color="#f0f">**componentDidUpdate**</font>

组件完成更新后立即调用，在初始化时不会被调用

<font color="#f0f">**componentWillUnmount**</font>

在组件从DOM中移除之前立刻被调用

## Redux

### Redux基本介绍

<font color="#f0f">**单项数据流：**</font>

从父组件流向子组件，兄弟组件无法共享数据

<font color="#f0f">**state：**</font>

React中的状态，是只读对象，不可直接修改

<font color="#f0f">**Reducer：**</font>

基本函数，用于对state的业务处理

<font color="#f0f">**Action：**</font>

普通对象，用于描述事件行为，改变state

### Redux安装

```shell
yarn add redux --save
yarn add react-redux --save
```

### Redux集成

创建`Action`模块

创建`Reducer`模块

创建`Store`模块

通过`connect`方法将`React`组件和`Redux`连接起来

添加`Provider`作为项目的根组件，用于数据的存储

### Redux调试工具安装

在Chrome中安装Redux Devtools扩展

```shell
yarn add redux-devtools-extension
```

## React脚手架、Yarn介绍

### 安装React脚手架

```js
npm install -g create-react-app  //安装这个脚手架
create-react-app may-app    //初始化一个项目
cd my-app   //切换
npm start   //启动进入
```

### 什么是Yarn?

> Yarn是新一代的包管理工具

### 为什么使用Yarn?

- 速度快
- 安装版本统一，更安全
- 更简洁的输出
- 更好的语义化

### 如何使用Yarn？

```js
yarn init   //初始化一个项目
yarn add    //安装一个包
yarn remove     //删除一个包
yarn / yarn install     //安装依赖包
```

## 源码和课程教程

源码：[github.com/shifengming…](https://github.com/shifengming/imoocmanager)

课程地址：[coding.imooc.com/class/236.h…](https://coding.imooc.com/class/236.html)

## 效果图

### 项目主页面

![5](https://qq292383147.github.io/pictureLibrary/picture/React/单车/1.jpg)

### AntD的Button页面

![6](https://qq292383147.github.io/pictureLibrary/picture/React/单车/2.jpg)

### Echart图表页面

![7](https://qq292383147.github.io/pictureLibrary/picture/React/单车/3.jpg)

### 城市管理页面

![8](https://qq292383147.github.io/pictureLibrary/picture/React/单车/4.jpg)

### Echart饼形图页面

![9](https://qq292383147.github.io/pictureLibrary/picture/React/单车/5.jpg)

### UI轮播图，包含文字轮播和图片轮播

![10](https://qq292383147.github.io/pictureLibrary/picture/React/单车/6.jpg)

### 车辆地图页面

![11](https://qq292383147.github.io/pictureLibrary/picture/React/单车/7.jpg)

### 用户授权页面

![12](https://qq292383147.github.io/pictureLibrary/picture/React/单车/8.jpg)

### 高级表格页面

![14](https://qq292383147.github.io/pictureLibrary/picture/React/单车/9.jpg)

### 菜单权限页面

![15](https://qq292383147.github.io/pictureLibrary/picture/React/单车/10.jpg)

### 员工管理页面

![16](https://qq292383147.github.io/pictureLibrary/picture/React/单车/11.jpg)

### 表单页面

![17](https://qq292383147.github.io/pictureLibrary/picture/React/单车/12.jpg)

### 订单详情页面

![17](https://qq292383147.github.io/pictureLibrary/picture/React/单车/13.jpg)

## 搭建运行环境

<font color="#f0f">安装脚手架</font>

```shell
npm install -g create-react-app
```

<font color="#f0f">查看版本号，看是否安装成功</font>

```shell
create-react-app --version
```

<font color="#f0f">初始化这个项目</font>

```shell
create-react-app imoocmanager
```

<font color="#f0f">切换</font>

```shell
cd imoocmanager
```

<font color="#f0f">启动进入</font>

```shell
npm start
```

<font color="#f0f">安装yarn</font>

```shell
npm install -g yarn
```

<font color="#f0f">查看版本号，看是否安装好</font>

```shell
yarn --version
```

<font color="#f0f">**注：**</font>

这个项目没有webpack配置，这就是脚手架的特色，脚手架把webpack的配置全部给它封装起来了，所以只需要关心src的源码部分

## 项目所需要安装的插件

**引入antd(安装支付宝的UI框架)**

```shell
yarn add antd --save
```

**加入其它依赖**

```js
yarn add axios --save  //Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中
yarn add jsonp --save //跨域请求
yarn add less --save //(2.7.3的版本)，超过此版本，antd按需加载报错.bezierEasingMixin();
yarn add less-loader --save  //antd 用的是less预处理，所以也添加less,保持一致。
yarn add moment --save //日期处理
yarn add babel --svae  //转换react jsx语法和转换es6 语法后才能兼容智障浏览器
yarn add babel-polyfill --save 
yarn add babel-plugin-import --save //不添加的话 IE会报错TypeError: 对象不支持“startsWith”属性或方法
```

## 开发过程中重点问题总结

### 主页面架构设计

#### <font color="#1E90FF">页面结构定义</font>

- 左侧导航栏，右侧显示内容
- 右侧显示内容分别分为Header、中Content和下Footer部分

#### <font color="#1E90FF">目录结构定义</font>

- 定义components包，分别加入Footer、Header、NavLeft包，内部加入index.js文件，导入时可以导入到包的级别，系统会自动寻找包下的index.js文件
- 定义style包，内部加入common.less文件定义全局样式

#### <font color="#1E90FF">栅格系统使用</font>

- 栅格系统一共24列
- Antd中行用Row组件，列使用Col组件，列存在span属性(span={长度值}的方式写入span属性)，同一Row下的Col  span总和为24

#### <font color="#1E90FF">calc计算方法使用</font>

- clac()是less中动态计算长度值
- 任何长度值都可以用clac()函数进行计算
- calc(100vh):vh的含义相当于1%,100vh即是100%

**例子使用：**

```
width:clac(100%-50px)   //表示宽度属性是整个布局的100%减去50px的长度
```

#### <font color="#1E90FF">关于less</font>

- less是预编辑器
- 在div下有a标签，想设定a的样式和div的样式，在less中可以在定义时嵌套

```css
//css中
div{...}
div a{...}

//less中
div{
    ...
    a:{
      ...  
    }
}
```

- less可以使用定义的变量

```css
@colorA:'red'
div{
    color:@colorA
    a:{
        color:black  
    }
}
```

#### 实例公共代码

**admin.js**

```js
import React,{Component} from 'react'
import { Row,Col } from 'antd';
import Header from './components/Headers/index'
import Footer from './components/Footer/index'
import NavLeft from './components/NavLeft/index'
import './style/common.less'
// import Row from './components/NavLeft/index'
export default class Admin extends Component{
    render (){
        return(
           <Row className="container">
               <Col span="5" className="nav-left" >
                   <NavLeft />
               </Col>
               <Col span="19" className="main">
                   <Header />
                   <Row className="content">
                       {this.props.children}
                   </Row>
                   <Footer />
               </Col>
           </Row>
        )
    }
}

```

**src/style/commmon.less**

```css
.container{
    display: flex;
    .nav-left{
        background-color:#001529;
        color: #ffffff;
        height: calc(100vh);
    }
    .main{
        height: calc(100vh);
        background-color: @colorL;
        overflow: auto;
    }
    .content{
        position: relative;
        padding: 20px;
    }
}
```

#### 实例代码-左侧导航栏内容

**src/components/NavLeft/index.js**

```js
import React,{Component} from 'react'
import { Menu, Icon } from 'antd';
import MenuConfig from './../../config/menuConfig'
import './index.less'

const SubMenu = Menu.SubMenu;

export default class NavLeft extends Component{
    componentWillMount(){
        const menuTreeNode = this.renderMenu(MenuConfig);

        this.setState ({
            menuTreeNode
        })
    }
    //菜单渲染
    renderMenu =(data)=>{
        return data.map((item)=>{
            if(item.children){
                return (
                    <SubMenu title={item.title} key={item.key}>
                        {this.renderMenu(item.children)}
                    </SubMenu>
                )
            }
            return <Menu.Item title={item.title} key={item.key}>{item.title}</Menu.Item>
        })
    }
    render (){
        return(
            <div>
                <div className="logo">
                    <img src="/assets/logo-ant.svg" alt=""/>
                    <h1>BikeSharing</h1>
                </div>
                <Menu theme="dark">
                    { this.state.menuTreeNode }
                </Menu>

            </div>
        )
    }
}
```

在public文件夹下添加assets文件夹，放置logo-ant.svg图片

注意：public文件是build文件是build之后存储内容的文件，通常内部放置静态资源，public下的文件内容在访问时全是通过根目录直接访问文件地址

编写Navleft组件内容/src/Navleft/index.js，使用antd中的Menu和Icon组件，Menu组件的theme属性可以设置菜单样式。对应的SubMenu组件需要设置title和key属性值，Menu.Item组件需要设置title和key属性值和组件内容

**src/NavLeft/index.less**

> 编写Navleft组件样式

```css
.logo{
    line-height: 90px;
    padding-left: 20px;
    background-color: #002140;
    img{
        height: 35px;
    }
    h1{
        color: #ffffff;
        font-size: 20px;
        display: inline-block;
        vertical-align: middle;
        margin: 0 0 0 10px;
    }
}
```

**src/config/menuConfig.js**

```js
const menuList = [
    {
        title:'首页',
        key:'/admin/home'
    },
    {
        title:'UI',
        key:'/admin/ui',
        children:[
            {
                title:'按钮',
                key:'/admin/ui/buttons',
            },
            {
                title:'弹框',
                key:'/admin/ui/modals',
            },
            {
                title:'Loading',
                key:'/admin/ui/loadings',
            },
            {
                title:'通知提醒',
                key:'/admin/ui/notification',
            },
            {
                title:'全局Message',
                key:'/admin/ui/messages',
            },
            {
                title:'Tab页签',
                key:'/admin/ui/tabs',
            },
            {
                title:'图片画廊',
                key:'/admin/ui/gallery',
            },
            {
                title:'轮播图',
                key:'/admin/ui/carousel',
            }
        ]
    },
    {
        title:'表单',
        key:'/admin/form',
        children:[
            {
                title:'登录',
                key:'/admin/form/login',
            },
            {
                title:'注册',
                key:'/admin/form/reg',
            }
        ]
    },
    {
        title:'表格',
        key:'/admin/table',
        children:[
            {
                title:'基础表格',
                key:'/admin/table/basic',
            },
            {
                title:'高级表格',
                key:'/admin/table/high',
            }
        ]
    },
    {
        title:'富文本',
        key:'/admin/rich'
    },
    {
        title:'城市管理',
        key:'/admin/city'
    },
    {
        title:'订单管理',
        key:'/admin/order',
        btnList:[
            {
                title:'订单详情',
                key:'detail'
            },
            {
                title:'结束订单',
                key:'finish'
            }
        ]
    },
    {
        title:'员工管理',
        key:'/admin/user'
    },
    {
        title:'车辆地图',
        key:'/admin/bikeMap'
    },
    {
        title:'图标',
        key:'/admin/charts',
        children:[
            {
                title:'柱形图',
                key:'/admin/charts/bar'
            },
            {
                title:'饼图',
                key:'/admin/charts/pie'
            },
            {
                title:'折线图',
                key:'/admin/charts/line'
            },
        ]
    },
    {
        title:'权限设置',
        key:'/admin/permission'
    },
];
export default menuList;
```

在config下编写manuConfig.js返回导航栏内容title和key

效果如下：

![1](https://qq292383147.github.io/pictureLibrary/picture/React/单车/14.jpg)


#### <font color="#1E90FF"> 实例代码首页头部内容</font>

利用jsonp可以解决跨域问题（所谓跨域就是跨域名，跨端口，跨协议）

 

web页面上调用js文件时则不受跨域影响（且凡是有src属性的标签都具有跨域能力，如<\script> <\img> <\iframe>等）

<font color=red>**Promise最大好处**</font>

将回调函数的异步调用变成链式调用。函数返回的promise对象参数接受一个函数，参数1为成功resolve回调函数，参数2是失败的reject回调函数，函数体中返回对应函数调用。调用该返回Promise对象的函数的then方法参数为resolve函数传入的属性值为参数的函数，在方法体内写入回调成功返回的内容

**src/components/Header/index.js**

利用setInterval函数实时刷新时间信息，并调用axios包中的jsonp方法发送请求并根据promise进行回调

```js
import React,{Component} from 'react'
import { Row,Col } from 'antd';
import './index.less'
import Util from '../../utils/utils'
import axios from '../../axios/index'

export default class Header extends Component{
    componentWillMount(){
        this.setState({
            userName:'Dream_Lee'
        })
        setInterval(()=>{
            let sysTime = Util.formateDate(new Date().getTime());
            this.setState({
                sysTime
            })
        },1000)
        this.getWeatherAPIData();
    }

    getWeatherAPIData(){
        let city = '北京'
        axios.jsonp({
            url:'http://api.map.baidu.com/telematics/v3/weather?location='+encodeURIComponent(city)+'&output=json&ak=3p49MVra6urFRGOT9s8UBWr2'
        }).then((res)=>{
            // debugger;
            if(res.status == 'success'){
                let data = res.results[0].weather_data[0];
                this.setState({
                    dayPictureUrl:data.dayPictureUrl,
                    weather:data.weather
                })
            }
        })
    }

    render (){
        return(
            <div className="header" >
                <Row className="header-top">
                    <Col span="24" >
                        <span >欢迎</span>
                        <span className="welcome">{this.state.userName}</span>

                        <a href="">退出</a>
                    </Col>
                </Row>

                <Row className="breadcrumb">
                    <Col span="4" className="breadcrumb-title">
                        首页
                    </Col>
                    <Col span="20" className="weather">
                        <span className="date">{this.state.sysTime}</span>
                        <span className="weather-img">
                            <img src={this.state.dayPictureUrl} alt=""/>
                        </span>
                        <span className="weather-detail">
                            {this.state.weather}
                        </span>
                    </Col>
                </Row>
            </div>
        )
    }
}

```

**src/components/Header/index.less**

```less
.header{
    .header-top{
        height: 60px;
        line-height: 60px;
        padding: 0 20px;
        text-align: right;
        .welcome{
            margin-left: 5px;
        }
        a{
            margin-left: 20px;
        }
    }
    .breadcrumb{
        height: 40px;
        line-height: 40px;
        padding: 0 20px;
        border-top: 1px solid #f9c700;
        .breadcrumb-title{
            text-align: center;
        }
        .weather{
            text-align: right;
            .date{
                margin-right: 10px;
                vertical-align: middle;
            }
            .weather-detail{
                margin-left: 5px;
                vertical-align: middle;
            }
            .weather-img{
                img{
                    height: 15px;
                }
            }
        }
    }
}
```

**src/untils/untils.js**

- 封装时间

```js
import React,{Component} from 'react'
export default {
    formateDate(time){
        if(!time) return '';
        let date = new Date(time);
        return date.getFullYear()+'-'+(date.getMonth()+1)+'-'+date.getDate()+' '+date.getHours()+':'+date.getMinutes()+':'+date.getSeconds()+' ';
    }
}
```

**src/axios/index.js利用Jsonp**

- 模块发送请求获得jsonp数据，解决跨域问题：

```css
.header{
    .header-top{
        height: 60px;
        line-height: 60px;
        padding: 0 20px;
        text-align: right;
        .welcome{
            margin-left: 5px;
        }
        a{
            margin-left: 20px;
        }
    }
    .breadcrumb{
        height: 40px;
        line-height: 40px;
        padding: 0 20px;
        border-top: 1px solid #f9c700;
        .breadcrumb-title{
            text-align: center;
        }
        .weather{
            text-align: right;
            .date{
                margin-right: 10px;
                vertical-align: middle;
            }
            .weather-detail{
                margin-left: 5px;
                vertical-align: middle;
            }
            .weather-img{
                img{
                    height: 15px;
                }
            }
        }
    }
}
```

效果如下

![2](https://qq292383147.github.io/pictureLibrary/picture/React/单车/15.jpg)

**src/components/Footer/index.js**

```js
import React from 'react'
import './index.less'

export default class Footer extends React.Component{
    render(){
        return(
            <div className="footer">
                版权所有：慕课网&河畔一角（推荐使用谷歌浏览器,可以获得更佳操作页面体验） 技术支持：河畔一角
            </div>
        );
    }
}
```

**src/components/Footer/index.less**

```css
@import './../../style/default';
.footer{
    height: 100px;
    padding: 40px 0;
    text-align: center;
    color:@colorJ;
;
}
```

效果如下：

![3](https://qq292383147.github.io/pictureLibrary/picture/React/单车/16.jpg)

#### 整体页面效果

![4](https://qq292383147.github.io/pictureLibrary/picture/React/单车/17.jpg)

### Router 4.0

#### React Router4.0基本概念介绍

4.0版本已不需要路由配置，一切皆组件

- react-router：基础路由包

  提供了一些router的核心api,包括Router,Route,Switch等

- react-router-dom：基于浏览器端的路由（包含react-router)

  提供了BrowserRouter,HashRouter,Route,Link,NavLink

  安装：`npm install react-router-dom --save` 或 `yarn add react-router-dom`

- react-router-dom核心用法

  HashRouter和BrowserRouter

  Route：path、exact、component、render

  注：exact属性代表精准匹配，必须path完全匹配才可以加载对应组件

- NavLink应用于菜单里作为菜单导航、Link超链接导航

```js
eg1.
import {Link} from 'react-router-dom';
const Header=()=>{
    <header>
        <nav>
            <li><Link to='/'>Home</Link></li>
            <li><Link to='/about'>About</Link></li>
            <li><Link to='/three'>Three</Link></li>
        </nav>
    </header>
}
```

- 定义：取值：this.props.match.params.number

```js
<Link to={{pathname:'/three/7'}}>Three #7</Link>
```

- 同时在to属性中可以传递一个location对象，如：

```js
{pathname:'/',search:'',hash:'',key:'abc123',state:{}}
```

- Switch-选择符合要求的Route,自上至下找到第一个可以匹配的内容，则不继续加载其他

```
<Switch>
    <Route path='/admin/ui/buttons' component={Buttons}/>
    <Route path='/admin/ui/models' component={Models}/>
    <Route path='/admin/ui/loading' component={Loading}/>
</Switch>
```

- Redirect

```
路由重定向：<Redirect to="/admin/home">
```

#### React Router4.0 Demo介绍

- 4.0基本路由功能DEMO实现-混合组件化【将Route和Link放在同一页面】

  `HashRouter`将`Link`和R`outer`进行包裹，其内部必须只能有一个子节点

  通过Link组件的to属性设置路由地址；通过`Route`组件的`path`属性匹配路由地址，从而渲染对应`component`中的组件【注意：Route添加exact属性可以做到路径的精准匹配，否则/about既可以匹配/也可以匹配/about等路由地址】

- 实战代码

**Home.js**

> 用于显示整个页面内容

```js
import React from 'react';
import {HashRouter,Route,Link,Switch} from 'react-router-dom'
import Main from './Main';
import About from './About';
import Topics from './Topics';
class Home extends React.Component{
  render(){
      return(
          <HashRouter>
              <div>
                  <ul>
                      <li>
                          <Link to="/">Home</Link>
                      </li>
                      <li>
                          <Link to="/about">About</Link>
                      </li>
                      <li>
                          <Link to="/topics">Topics</Link>
                      </li>
                  </ul>
                  <hr></hr>
                  <Route path="/" exact={true} component={Main}></Route>
                  <Route path="/about" component={About}></Route>
                  <Route path="/topics" component={Topics}></Route>
              </div>   
          </HashRouter>
      );
  }
}
export default Home;
```

**Main.js组件**

```js
import React,{Component} from 'react';
class Main extends Component{
  render(){
      return(
          <div>
              this is Main.
          </div>
      );
  }
}
export default Main;
```

**Topic.js组件**

```js
import React,{Component} from 'react';
class Topics extends Component{
  render(){
      return(
          <div>
              this is Topics.
          </div>
      );
  }
}
export default Topics;
```

**About.js组件**

```js
import React,{Component} from 'react';
class About extends Component{
  render(){
      return(
          <div>
              this is About.
          </div>
      );
  }
}
export default About;
```

- 4.0基本路由功能DEMO实现-配置化【将Route路由提取到一个单独的JS文件中】

  <font color="#f0f">配置化实现路由功能</font>

  创建Home.js内部写上ul->li->Link导航组件，并在想要显示对应路由内容的区域写上`{this.props.children}`即会加载调用Home.js组建时内部传递的信息

  创建router.js，最外层用HashRouter包裹，第二级用Home组件包裹，内部写对应路由Route(path路由路径匹配、及component属性渲染的组件)

  执行流程，index.js渲染Router组件时，由于最外层是HashRouter，内部是Home组件故加载Home组件内容，并通过`{this.props.children}`得到在调用Home组件时内部的信息

  <font color="#f0f">嵌套路由</font>

  如想实现在Main组件中的嵌套路由，需要在Main组件中添加`{this.props.children}`从而渲染对应的内部信息，还需要添加Link组件以进行跳转

  之后在router.js中对应调用该组件的Route组件中，删除component属性，添加render属性进行页面渲染，render属性内应是一个函数，返回Main组件（内部带有Route属性以进行路由渲染）

  <font color=red>注意点：</font>

  调用Main组件的`Route`不能添加`exact`属性，因为如果添加`exact`属性，当点击内部组件路由到对应url时由于与外部`Route`的`path`不是完全匹配，故将不会显示

  调用Main组件的Route内部render函数如果添加()=>{}则需要在函数体内写return，因为{}表示函数体，内部的函数将被执行，返回组件需要写return；如果不添加大括号则直接写返回的组件即可，ES6箭头函数默认箭头后面的内容是return的

  调用Main组件的Route内部Main里的Route组件的path需要包含外部Route的path作为一级路由，如外部是/main内部需要是/main/xxx，如果不以外部Route作为一级路由则不会走外部的Route到内部Route内容

- 实战代码

**/src/pages/router-demo/router2/router.js**

```js
import React from 'react';
import {HashRouter as Router,Route,Link}from 'react-router-dom';
import Main from './../router1/Main';
import About from './../router1/About';
import Topics from './../router1/Topics';
import Home from './Home';
class IRoute extends React.Component{
  render(){
      return(
          <Router>
              <Home>
                  <Route path="/main" render={()=>{
                      return(
                      <Main>
                          <Route path="/main/a" component={About}></Route>
                      </Main>
                      );}}></Route>
                  <Route path="/about" component={About}></Route>
                  <Route path="/topics" component={Topics}></Route>
              </Home>
          </Router>
      );
  }
}
export default IRoute;
```

**/src/pages/router-demo/router2/Home.js**

```js
import React from 'react';
import {Link} from 'react-router-dom'

class Home extends React.Component{
  render(){
      return(
          <div>
              <ul>
                  <li>
                      <Link to="/main">Home1</Link>
                  </li>
                  <li>
                      <Link to="/about">About1</Link>
                  </li>
                  <li>
                      <Link to="/topics">Topics1</Link>
                  </li>
              </ul>
              <hr></hr>
              {this.props.children}
          </div>
      );
  }
}
export default Home;
```

**/src/pages/router-demo/router2/Main.js**

```js
import React,{Component} from 'react';
import {Link} from 'react-router-dom';
class Main extends Component{
  render(){
      return(
          <div>
              this is Main.
              <Link to="/main/a">To start a</Link>
              <hr></hr>
              {this.props.children}
          </div>
      );
  }
}
export default Main;
```

- 获取动态路由的值

**在main.js中设置跳转的路由链接**

```js
import React,{Component} from 'react';
import {Link} from 'react-router-dom';
class Main extends Component{
    render(){
        return(
            <div>
                this is Main.<br/>
                <Link to="/main/test-id">嵌套路由1</Link><br/>
                <Link to="/main/456">嵌套路由2</Link>
                <hr></hr>
                {this.props.children}
            </div>
        );
    }
}
export default Main;
```

**在router.js中添加动态路由即path:"/main/:value"用冒号定义的路由内容**

```js
import React from 'react';
import {HashRouter as Router,Route,Link,Switch}from 'react-router-dom';
import Main from './Main';
import About from './../router1/About';
import Topics from './../router1/Topics';
import Home from './Home';
import Info from './Info';
import NoMatch from './NoMatch';
class IRoute extends React.Component{
    render(){
        return(
            <Router>
                <Home>
                    <Switch>
                        <Route path="/main" render={()=>{
                            return(
                            <Main>
                                <Route path="/main/:value" component={Info}></Route>
                            </Main>
                            );}}></Route>
                        <Route path="/about" component={About}></Route>
                        <Route path="/topics" component={Topics}></Route>
                        <Route component={NoMatch}></Route>
                    </Switch>
                </Home>
            </Router>
        );
    }
}
export default IRoute;
```

**在Info.js中获取定义的动态路由内容信息，通过{this.props.match.params.路由的名称}**

```js
import React,{Component} from 'react';
class Info extends Component{
    render(){
        return(
            <div>
                这里是测试动态路由功能
                动态路由的值是{this.props.match.params.value}
            </div>
        );
    }
}
export default Info;
```

- 添加默认路由

  添加react-router-dom的Switch组件包裹Route组件用于设置自上自下只匹配一个路由

  添加没有path属性的Route组件放置Switch组件内部的最后位置，作为默认路由

**NoMath.js**

```js
import React from 'react';
class NoMatch extends React.Component{
    render(){
        return(
            <div>
                404 Not Found
            </div>
        );
    }
}
export default NoMatch;
```

#### <font color="#1E90FF">项目路由实战开发</font>

由于用户访问项目时输入url需要有对应的输出，而作为整个文件输出时，一共有三种情况：登录、详情页、首页。故需要编写项目的入口文件router.js并在index.js中引入

router文件中定义使用路由的方式为HashRouter

由于我们要访问完整路由时有登录页面、详情页面和首页，router文件需要定义根组件App，App.js内部什么都没有只有`{this.props.children}`，主要用来存放子组件（即上述三个页面）。【如果没有用App进行包裹，即没有地方设置`{this.props.children}`显示路由的页面内容，即上述三个页面没法显示】

总结：想利用Route显示组件信息，则必须调用`{this.props.children}`显示其页面的组件

有三个页面就需要有三个路由path分别为`/login`渲染登录组件、`/admin`渲染首页（其中里用render函数返回子路由Admin组件，并定义嵌套路由`/admin/ui/buttons`显示组件按钮;无path显示404页面，外层用Switch包裹保证只显示其中第一个匹配的Route）、和`/order/detail`渲染详情页 

**/src/router.js**

```js
import React,{Component} from 'react';
import {HashRouter,Route,Switch} from 'react-router-dom';
import App from './App';
import Login from './pages/login';
import Admin from './admin';
import Buttons from './pages/ui/buttons';
import NoMatch from './pages/nomatch';
class IRouter extends Component{
  render(){
      return(
          <HashRouter>
              <App>
                  <Route path="/login" component={Login}></Route>
                  <Route path="/admin" render={()=>{
                      return(
                          <Admin>
                              <Switch>
                                  <Route path="/admin/ui/buttons" component={Buttons}></Route>
                                  <Route component={NoMatch}></Route>
                              </Switch>
                          </Admin>
                      );
                  }}></Route>
                  <Route path="/order/detail" component={Login}></Route>
              </App>
          </HashRouter>
      );
  }
}
export default IRouter;
```

**将Admin组件中的content部分使用{this.props.children}显示在router.js中的Route得到的页面**

**/src/admin.js**

```js
import React from 'react';
import { Row, Col } from 'antd';
import Header from './components/Header';
import Footer from './components/Footer';
import NavLeft from './components/NavLeft';
import Home from './pages/home';
import './style/common.less'
class Admin extends React.Component{
  render(){
      return(
          <Row className="container">
              <Col span={6} className="nav-left">
                  <NavLeft/>
              </Col>
              <Col span={18} className="main">
                  <Header/>
                  <Row className="content">
                      {/* <Home></Home> */}
                      {this.props.children}
                  </Row>
                  <Footer/>
              </Col>
          </Row>
      );
  }
}
export default Admin;
```

<font color="#1E90FF">**有Route就一定要有Link指定路由地址，我们在首页中通过左侧导航栏进行跳转，故需要在NavLeft组件中利用react-router-dom的NavLink设置路由地址，NavLink组件显示的内容为`{item.title}`，to跳转的地址为`{item.key}`**</font>

**/src/components/Navleft/index.js**

```js
import React from 'react';
import {Menu,Icon} from 'antd';
import MenuConfig from './../../config/menuConfig';
import './index.less';
import MenuItem from 'antd/lib/menu/MenuItem';
import {NavLink} from 'react-router-dom';
const SubMenu = Menu.SubMenu;
class NavLeft extends React.Component{
  componentWillMount(){
      const menuTreeNode = this.renderMenu(MenuConfig);
      this.setState({
          menuTreeNode
      })
  }
  //菜单渲染
  renderMenu=(data)=>{
      return data.map((item,index)=>{
          if(item.children){
              return(
                  <SubMenu title={item.title} key={item.key}>
                      {this.renderMenu(item.children)}
                  </SubMenu>
              )
          }
          return <Menu.Item title={item.title} key={item.key}>
              <NavLink to={item.key}>{item.title}</NavLink>
          </Menu.Item>
      })
  }
  render(){
      return(
          <div>
              <div className="logo">
                  <img src="/assets/logo-ant.svg"  alt=""></img>
                  <h1>Imooc MS</h1>
              </div>
              <Menu theme="dark">
                  {this.state.menuTreeNode}
              </Menu>
          </div>
      );
  }
}  
export default NavLeft;
```

**在router.js中可以看到如果匹配的是`/admin/ui/buttons`则将Button组件渲染到Admin组件的content中；如没有写对应的路由匹配则将404页面渲染到Admin组件的content中，对应代码如下**

**/src/pages/ui/buttons.js**

```js
import React,{Component} from 'react';
class Buttons extends Component{
  render(){
      return(
          <div>
              This is Buttons Page.
          </div>
      )
  }
}
export default Buttons;
//[/src/pages/nomatch/index.js]
import React from 'react';
class NoMatch extends React.Component{
  render(){
      return(
          <div style={{textAlign:'center',fontSize:'24'}}>
              404 Not Found!!!
          </div>
      );
  }
}
export default NoMatch;
```

### UI菜单各个组件使用(Andt UI组件)

#### 按钮组件

- 引入Card组件

```js
import {Card} from 'antd'
```

- title属性用于标注卡片上方标题

```js
<Card title="基础组件"></Card>
```

![5-0](https://qq292383147.github.io/pictureLibrary/picture/React/单车/18.jpg)



#### Button组件

- 引入Button组件：

```js
import {Button} from 'antd'
```

- type属性值

  `primary`表示主按钮

  不写`type`表示默认样式按钮

  `dashed`表示虚线按钮

  `danger`表示危险按钮

- disable属性值表示禁用按钮

- icon属性值表示按钮图标样式

  `plus`表示加号

  `danger`表示危险按钮

  `delete`表示删除

  `search`表示搜索

  `download`表示下载

- shape属性表示按钮形状

  `circle`表示圆形

- loading属性为{true}表示加载中（此时按钮不能点击）

- 按钮组为Button.Group组件，用于表示包含的Button组件是一个组

- size属性表示组件大小

  `small`小按钮组件

  `default`默认大小按钮组件

  `large`大按钮组件

#### Radio组件

- 引入Rodio组件：

```js
import {Radio} from 'antd'
```

- Radio组件外部需要用Radio.Group组件包裹，并通过外部组件对象可以获得内部Radio组件的value值(通过e.target.value)

#### 应用实例

**button.js及对应添加的样式如下所示**

```js
//[/src/pages/ui/button.js]
import React,{Component} from 'react';
import {Card,Button,Radio} from 'antd';
import './ui.less';
class Buttons extends Component{
  constructor(props){
      super(props);
      this.state={
          loading:true,
          size:'default'
      }
  }
  render(){
      return(
          <div>
              <Card title="基础按钮" className="card-wrap">
                  {/*主按钮*/}
                  <Button type="primary">Imooc</Button>
                  <Button>Imooc</Button>
                  {/* 虚线按钮 */}
                  <Button type="dashed">Imooc</Button>
                  {/* 危险按钮 */}
                  <Button type="danger">Imooc</Button>
                  {/* 禁用按钮 */}
                  <Button disabled>Imooc</Button>
              </Card>
              <Card title="图形按钮" className="card-wrap">
                  {/*通过icon设定图标,shape设置形状*/}
                  <Button icon="plus">创建</Button>
                  <Button icon="edit">编辑</Button>
                  <Button icon="delete">删除</Button>
                  <Button icon="search" shape="circle"></Button>
                  <Button type="primary" icon="search">搜索</Button>
                  <Button type="primary" icon="download">下载</Button>
              </Card>
              <Card title="Loading按钮" className="card-wrap">
                  {/*通过loading属性为{true}表示加载中图标(此时按钮不能点)*/}
                  <Button type="primary" loading={this.state.loading}>确定</Button>
                  <Button type="primary" shape="circle" loading={this.state.loading} ></Button>
                  <Button loading={this.state.loading} >点击加载</Button>
                  <Button shape="circle" loading={this.state.loading} ></Button>
                  <Button type="primary" onClick={this.handleCloseLoading}>关闭</Button>
              </Card>
              <Card title="按钮组">
                  <Button.Group>
                      <Button type="primary" icon="left">返回</Button>
                      <Button type="primary" icon="right">前进</Button>
                  </Button.Group>
              </Card>
              <Card title="按钮尺寸" className="card-wrap">
                  <Radio.Group value={this.state.size} onChange={this.handleChange}>
                      <Radio value="small">小</Radio>
                      <Radio value="default">中</Radio>
                      <Radio value="large">大</Radio>
                  </Radio.Group>
                  <Button type="primary" size={this.state.size}>Imooc</Button>
                  <Button size={this.state.size}>Imooc</Button>
                  <Button type="dashed" size={this.state.size}>Imooc</Button>
                  <Button type="danger" size={this.state.size}>imooc</Button>
              </Card>
          </div>
      )
  }
  handleCloseLoading=()=>{
      this.setState({
          loading:false
      });
  }
  handleChange=(e)=>{
      this.setState({
          size:e.target.value
      });
  }
}
export default Buttons;

//[/src/pages/ui/ui.less]
.card-wrap{
  button{
      margin-right: 10px;
  }
}
```

**效果图**

![5](https://qq292383147.github.io/pictureLibrary/picture/React/单车/19.jpg)

<font color="#f0f">**补充知识点**</font>

当Route页面内部信息超过当前页面大小时，会出现滚动条，左侧导航栏会跟着一起滚动，导航栏下方为空包

**解决方案**

当common.less中的main的定义添加overflow:auto，表示当渲染页面高度超过当前屏幕时，自动滚动

#### 弹框组件-Modal基本组件

- 引入Modal:

```js
import {Modal} from 'antd';
```

- Model组件属性

  title属性作为标题显示

  `visible`属性参数为`{true|false}`,为true则显示，为false则不显示

  `onCancel`属性值为一个函数，执行当点击模态框的×或cancel选项时执行的方法

- Model内部填写的内容将作为模板框的正文内容

- 知识点

  组件的onClick值为`this.handleName`（即函数名）时，表示一开始就会自动调用，无法传参；当需要传参时，需要将onClick中的内容变为箭头函数，返回代参的调用方法从而实现点击时执行函数并传参调用方法

  传递的参数如果想作为对象的键时，需要用[]进行包裹，如果没包裹直接放置键的位置则视为变量而报错

**src/pages/ui/modal.js**

```js
import React from 'react'
import { Card, Button, Modal } from 'antd'
import './ui.less'
export default class Buttons extends React.Component {

    state = {
        showModal1: false,
        showModal2: false,
        showModal3: false,
        showModal4: false
    }

    handleOpen = (type)=>{
        this.setState({
            [type]:true
        })
    }

    handleConfirm = (type)=>{
        Modal[type]({
            title:'确认？',
            content:'你确定你学会了React了吗？',
            onOk(){
                console.log('Ok')
            },
            onCancel(){
                console.log('Cancel')
            }
        })
    }
    render(){
        return (
            <div>
                <Card title="基础模态框" className="card-wrap">
                    <Button type="primary" onClick={() =>this.handleOpen('showModal1')}>Open</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal2')}>自定义页脚</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal3')}>顶部20px弹框</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal4')}>水平垂直居中</Button>
                </Card>
                <Card title="信息确认框" className="card-wrap">
                    <Button type="primary" onClick={() => this.handleConfirm('confirm')}>Confirm</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('info')}>Info</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('success')}>Success</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('warning')}>Warning</Button>
                </Card>
                <Modal
                    title="React"
                    visible={this.state.showModal1}
                    onCancel={()=>{
                        this.setState({
                            showModal1:false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    visible={this.state.showModal2}
                    okText="好的"
                    cancelText="算了"
                    onCancel={() => {
                        this.setState({
                            showModal2: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    style={{top:20}}
                    visible={this.state.showModal3}
                    onCancel={() => {
                        this.setState({
                            showModal3: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    wrapClassName="vertical-center-modal"
                    visible={this.state.showModal4}
                    onCancel={() => {
                        this.setState({
                            showModal4: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
            </div>
        );
    }
}
```

**效果图** 

![6](https://qq292383147.github.io/pictureLibrary/picture/React/单车/20.jpg)

- Model自定义页脚实现方式

```
  Model组件的visible属性{true}或{false}实现是否显示

  Model组件的okText属性设置OK选项的显示内容

  Model组件的cancelText属性设置Cancel选项显示内容

- Model顶部20px弹框实现方式

  利用style属性值为{{top:20}}设定距顶部20px

- Model水平居中实现方式

  利用Model组件的wrapClassName设定样式名称
```

**实例代码**

```js
import React from 'react'
import { Card, Button, Modal } from 'antd'
import './ui.less'
export default class Buttons extends React.Component {

    state = {
        showModal1: false,
        showModal2: false,
        showModal3: false,
        showModal4: false
    }

    handleOpen = (type)=>{
        this.setState({
            [type]:true
        })
    }

    handleConfirm = (type)=>{
        Modal[type]({
            title:'确认？',
            content:'你确定你学会了React了吗？',
            onOk(){
                console.log('Ok')
            },
            onCancel(){
                console.log('Cancel')
            }
        })
    }
    render(){
        return (
            <div>
                <Card title="基础模态框" className="card-wrap">
                    <Button type="primary" onClick={() =>this.handleOpen('showModal1')}>Open</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal2')}>自定义页脚</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal3')}>顶部20px弹框</Button>
                    <Button type="primary" onClick={() =>this.handleOpen('showModal4')}>水平垂直居中</Button>
                </Card>
                <Card title="信息确认框" className="card-wrap">
                    <Button type="primary" onClick={() => this.handleConfirm('confirm')}>Confirm</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('info')}>Info</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('success')}>Success</Button>
                    <Button type="primary" onClick={() => this.handleConfirm('warning')}>Warning</Button>
                </Card>
                <Modal
                    title="React"
                    visible={this.state.showModal1}
                    onCancel={()=>{
                        this.setState({
                            showModal1:false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    visible={this.state.showModal2}
                    okText="好的"
                    cancelText="算了"
                    onCancel={() => {
                        this.setState({
                            showModal2: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    style={{top:20}}
                    visible={this.state.showModal3}
                    onCancel={() => {
                        this.setState({
                            showModal3: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
                <Modal
                    title="React"
                    wrapClassName="vertical-center-modal"
                    visible={this.state.showModal4}
                    onCancel={() => {
                        this.setState({
                            showModal4: false
                        })
                    }}
                >
                    <p>欢迎学习慕课新推出的React高级课程</p>
                </Modal>
            </div>
        );
    }
}
```

### 登录

#### 源代码

**src/pages/form/login.js**

```js
import React from "react";
import { Card, Form, Input, Button, message, Icon, Checkbox } from "antd";
const FormItem = Form.Item;
class FormLogin extends React.Component{

    handleSubmit = ()=>{
        let userInfo = this.props.form.getFieldsValue();
        this.props.form.validateFields((err,values)=>{
            if(!err){
                message.success(`${userInfo.userName} 恭喜你，您通过本次表单组件学习，当前密码为：${userInfo.userPwd}`)
            }
        })
    }

    render(){
        const { getFieldDecorator } = this.props.form;
        return (
            <div>
                <Card title="登录行内表单">
                    <Form layout="inline">
                        <FormItem>
                            <Input placeholder="请输入用户名"/>
                        </FormItem>
                        <FormItem>
                            <Input placeholder="请输入密码" />
                        </FormItem>
                        <FormItem>
                            <Button type="primary">登录</Button>
                        </FormItem>
                    </Form>
                </Card>
                <Card title="登录水平表单" style={{marginTop:10}}>
                    <Form style={{width:300}}>
                        <FormItem>
                            {
                                getFieldDecorator('userName',{
                                    initialValue:'',
                                    rules:[
                                        {
                                            required:true,
                                            message:'用户名不能为空'
                                        },
                                        {
                                            min:5,max:10,
                                            message:'长度不在范围内'
                                        },
                                        {
                                            pattern:new RegExp('^\\w+$','g'),
                                            message:'用户名必须为字母或者数字'
                                        }
                                    ]
                                })(
                                    <Input prefix={<Icon type="user"/>} placeholder="请输入用户名" />
                                )
                            }
                        </FormItem>
                        <FormItem>
                            {
                                getFieldDecorator('userPwd', {
                                    initialValue: '',
                                    rules: []
                                })(
                                    <Input prefix={<Icon type="lock" />} type="password" placeholder="请输入密码" />
                                )
                            }
                        </FormItem>
                        <FormItem>
                            {
                                getFieldDecorator('remember', {
                                    valuePropName:'checked',
                                    initialValue: true
                                })(
                                    <Checkbox>记住密码</Checkbox>
                                )
                            }
                            <a href="#" style={{float:'right'}}>忘记密码</a>
                        </FormItem>
                        <FormItem>
                            <Button type="primary" onClick={this.handleSubmit}>登录</Button>
                        </FormItem>
                    </Form>
                </Card>
            </div>
        );
    }
}
export default Form.create()(FormLogin);
```

#### <font color="#1E90FF"> 取出用户名及密码的值</font>

如果不使用AntD封装好的方法来或许，常规的`react` 是先绑定`onClick`或`onChange`事件，通过事件里的方法获取`target`目标源，在获取目标源里的value值，然后把value值存起来，才能使用

AntD 通过`getFieldDecorator` 属性，来读取用户名及密码，直接进行使用，且使用之前必须通过`Form.create()`创建一个对象/表单，之后我们才能使用`getFieldDecorator`

`this.props.form.getFieldDecorator`是AntD已经封装好的，固定语法，要记住

```js
const { getFieldDecorator } = this.props.form;
```

**getFieldDecorator用法如下，其中在rules内定义规则**

```js
<FormItem>
	{
	     getFieldDecorator('userName',{
	         initialValue:'',
	         rules:[
	             {
	                 required:true,
	                 message:'用户名不能为空'
	             },
	             {
	                 min:5,max:10,
	                 message:'长度不在范围内'
	             },
	             {
	                 pattern:new RegExp('^\\w+$','g'),
	                 message:'用户名必须为字母或数字',
	             }
	         ]
	     })(
	     <Input prefix={<Icon type="user"/>} placeholder="请输入用户名"/>
	     )
	 }
</FormItem>
```

**必须要有下面这句话。通过Form.create()创建表单，将组件传递进去，这样才能识别 getFieldDecorator，否则会报错**

```js
//关键，一定要通过Form.create()创建一个对象/表单，将组件传递进去，这样才能识别 getFieldDecorator
export default Form.create()(FormLogin);
```

#### 效验输入的信息

- `/getFieldValue`是`object`对象，form的一个方法，用于获取表单下所有的值
- `validateFields`方法是校验信息是否符合要求，校验下是一个循环，用()=>

```js
handleSubmit = () =>{
        //getFieldsValue是object对象，form的一个方法，用于获取表单下所有的值
        let userInfo = this.props.form.getFieldsValue();
        //validateFields方法是校验信息是否符合要求，校验下是一个循环，用()=>
        this.props.form.validateFields((err,values)=>{
            if(!err){
                message.success(`${userInfo.userName}恭喜你，登陆成功!当前密码为：${userInfo.userPwd}`)
            }
        })
    }
```

**效果如图**

![7](https://qq292383147.github.io/pictureLibrary/picture/React/单车/21.jpg)

#### CheckBox记住密码

<font color="#ffe090">**一定要在getFieldDecorator里声明valuePropName:'checked',才能默认勾选Checkbox 的按钮**</font>

```js
<FormItem>
	{
		getFieldDecorator('remember',{
			valuePropName:'checked',
			 	initialValue:true
			 })(
				 <Checkbox >记住密码</Checkbox>
			 )
		 }
	 <a href="#" style={{float:'right'}}>忘记密码</a>
</FormItem>
```

#### 增加图标

<font color="#ffe090">**使用prefix={}**</font>

```js
<Input prefix={<Icon type="user"/>} placeholder="请输入用户名"/>
<Input prefix={<Icon type="lock"/>} placeholder="请输入密码"/>
```

**整体效果如图：**

![8](https://qq292383147.github.io/pictureLibrary/picture/React/单车/22.jpg)

### 注册

#### 源代码

```js
import React from 'react'
import {Card,Form,Button,Input,Checkbox,Radio,Select,Switch,DatePicker,TimePicker,Upload,Icon,message, InputNumber} from 'antd'
import moment from 'moment';
const FormItem = Form.Item;
const RadioGroup = Radio.Group;
const Option = Select.Option;
const TextArea = Input.TextArea;
class FormRegister extends React.Component{

    state={}

    handleSubmit = ()=>{
        let userInfo = this.props.form.getFieldsValue();
        console.log(JSON.stringify(userInfo))
        message.success(`${userInfo.userName} 恭喜你，您通过本次表单组件学习，当前密码为：${userInfo.userPwd}`)
    }

    getBase64 = (img, callback)=>{
        const reader = new FileReader();
        reader.addEventListener('load', () => callback(reader.result));
        reader.readAsDataURL(img);
    }

    handleChange = (info) => {
        if (info.file.status === 'uploading') {
            this.setState({ loading: true });
            return;
        }
        if (info.file.status === 'done') {
            // Get this url from response in real world.
            this.getBase64(info.file.originFileObj, imageUrl => this.setState({
                userImg:imageUrl,
                loading: false,
            }));
        }
    }

    render(){
        const { getFieldDecorator } = this.props.form;
        const formItemLayout = {
            labelCol:{
                xs:24,
                sm:4
            },
            wrapperCol:{
                xs:24,
                sm:12
            }
        }
        const offsetLayout = {
            wrapperCol:{
                xs:24,
                sm:{
                    span:12,
                    offset:4
                }
            }
        }
        const rowObject = {
            minRows: 4, maxRows: 6
        }
        return (
            <div>
                <Card title="注册表单">
                    <Form layout="horizontal">
                        <FormItem label="用户名" {...formItemLayout}>
                            {
                                getFieldDecorator('userName', {
                                    initialValue: '',
                                    rules: [
                                        {
                                            required: true,
                                            message: '用户名不能为空'
                                        }
                                    ]
                                })(
                                    <Input placeholder="请输入用户名" />
                                )
                            }
                        </FormItem>
                        <FormItem label="密码" {...formItemLayout}>
                            {
                                getFieldDecorator('userPwd', {
                                    initialValue: ''
                                })(
                                    <Input type="password" placeholder="请输入密码" />
                                )
                            }
                        </FormItem>
                        <FormItem label="性别" {...formItemLayout}>
                            {
                                getFieldDecorator('sex', {
                                    initialValue: '1'
                                })(
                                    <RadioGroup>
                                        <Radio value="1">男</Radio>
                                        <Radio value="2">女</Radio>
                                    </RadioGroup>
                                )
                            }
                        </FormItem>
                        <FormItem label="年龄" {...formItemLayout}>
                            {
                                getFieldDecorator('age', {
                                    initialValue: 18
                                })(
                                    <InputNumber  />
                                )
                            }
                        </FormItem>
                        <FormItem label="当前状态" {...formItemLayout}>
                            {
                                getFieldDecorator('state', {
                                    initialValue: '2'
                                })(
                                    <Select>
                                        <Option value="1">咸鱼一条</Option>
                                        <Option value="2">风华浪子</Option>
                                        <Option value="3">北大才子一枚</Option>
                                        <Option value="4">百度FE</Option>
                                        <Option value="5">创业者</Option>
                                    </Select>
                                )
                            }
                        </FormItem>
                        <FormItem label="爱好" {...formItemLayout}>
                            {
                                getFieldDecorator('interest', {
                                    initialValue: ['2','5']
                                })(
                                    <Select mode="multiple">
                                        <Option value="1">游泳</Option>
                                        <Option value="2">打篮球</Option>
                                        <Option value="3">踢足球</Option>
                                        <Option value="4">跑步</Option>
                                        <Option value="5">爬山</Option>
                                        <Option value="6">骑行</Option>
                                        <Option value="7">桌球</Option>
                                        <Option value="8">麦霸</Option>
                                    </Select>
                                )
                            }
                        </FormItem>
                        <FormItem label="是否已婚" {...formItemLayout}>
                            {
                                getFieldDecorator('isMarried', {
                                    valuePropName:'checked',
                                    initialValue: true
                                })(
                                    <Switch/>
                                )
                            }
                        </FormItem>
                        <FormItem label="生日" {...formItemLayout}>
                            {
                                getFieldDecorator('birthday',{
                                    initialValue:moment('2018-08-08')
                                })(
                                    <DatePicker
                                        showTime
                                        format="YYYY-MM-DD HH:mm:ss"
                                    />
                                )
                            }
                        </FormItem>
                        <FormItem label="联系地址" {...formItemLayout}>
                            {
                                getFieldDecorator('address',{
                                    initialValue:'北京市海淀区奥林匹克公园'
                                })(
                                    <TextArea
                                        autosize={rowObject}
                                    />
                                )
                            }
                        </FormItem>
                        <FormItem label="早起时间" {...formItemLayout}>
                            {
                                getFieldDecorator('time')(
                                    <TimePicker/>
                                )
                            }
                        </FormItem>
                        <FormItem label="头像" {...formItemLayout}>
                            {
                                getFieldDecorator('userImg')(
                                    <Upload
                                        listType="picture-card"
                                        showUploadList={false}
                                        action="//jsonplaceholder.typicode.com/posts/"
                                        onChange={this.handleChange}
                                    >
                                    {this.state.userImg?<img src={this.state.userImg}/>:<Icon type="plus"/>}
                                    </Upload>
                                )
                            }
                        </FormItem>
                        <FormItem {...offsetLayout}>
                            {
                                getFieldDecorator('userImg')(
                                   <Checkbox>我已阅读过<a href="#">慕课协议</a></Checkbox>
                                )
                            }
                        </FormItem>
                        <FormItem {...offsetLayout}>
                            <Button type="primary" onClick={this.handleSubmit}>注册</Button>
                        </FormItem>
                    </Form>
                </Card>
            </div>
        );
    }
}
export default Form.create()(FormRegister);
```



#### 联系地址

在设置联系地址的范围最大行数，最小行数时：autoSize={} 里面要求是一个对象。如const rows = {minRows:2,manRows:6}; autoSize={rows } ;成立。autoSize={minRows:2,manRows:6} 将报错。 AntD官方文档描述如下： 

![12](https://qq292383147.github.io/pictureLibrary/picture/React/单车/23.jpg)

```js
<FormItem label="联系地址" {...formItemLayout}>
  {
   getFieldDecorator('address',{
   nitialValue:'北京市海淀区奥林匹克公园'
   })(
   <TextArea
      autosize={rowObject}
      />
   )}
</FormItem>
```

效果如图：

![12](https://qq292383147.github.io/pictureLibrary/picture/React/单车/24.jpg)

#### 日期显示

**同时显示日期和时间 要showTime 和	format=‘YYYY–MM–DD HH:mm:ss’同时使用**

```js
<FormItem label="生日" {...formItemLayout}>
  {
    getFieldDecorator('birthday',{
    initialValue:moment('2018-08-08')
    })(
    <DatePicker
     showTime
     format="YYYY-MM-DD HH:mm:ss"
     />
     )}
</FormItem>
```

**如图**

![12](https://qq292383147.github.io/pictureLibrary/picture/React/单车/25.jpg)

#### 上传头像

- 实际做项目中，与现在有所不同

  要用自己的接口替换 action="[//jsonplaceholder.typicode.com/posts/](http://jsonplaceholder.typicode.com/posts/)"里的内容

  不需要 getBase64 方法，直从接口返回上传成功的URL地址，服务端把图片存到服务器里，返回前段一个服务器的图片地址，我们把图片地址放在img的src展示

**antD上传头像使用.jpg的图片格式**

```js
 //获取文件格式的字符串
getBase64 = (img, callback)=>{
	const reader = new FileReader();
    reader.addEventListener('load', () => callback(reader.result));
    reader.readAsDataURL(img);
}
handleChange = (info) => {
    if (info.file.status === 'uploading') {
        this.setState({ loading: true });
        return;
    }
    if (info.file.status === 'done') {
        // Get this url from response in real world.
        this.getBase64(info.file.originFileObj, imageUrl => this.setState({
            userImg:imageUrl,
            loading: false,
        }));
    }
}

<FormItem label="头像" {...formItemLayout}>
    {
        getFieldDecorator('userImg',{
        })(
            <Upload
                listType="picture-card"
                showUploadList={false}
                action="//jsonplaceholder.typicode.com/posts/"
                onChange={this.handleChange}
            >
                {this.state.userImg?<img src={this.state.userImg} />:<Icon type="plus"/>}
            </Upload>
        )
    }
</FormItem>
```

### 表格-基础表格

#### 源代码

**src/pages/table/basicTable.js**

```js
import React from 'react';
import { Card, Table, Modal, Button, message} from 'antd';
import axios from './../../axios/index'
import Utils from './../../utils/utils';
export default class BasicTable extends React.Component{

    state={
        dataSource2:[]
    }

    params = {
        page:1
    }

    componentDidMount(){
        const data = [
            {
                id:'0',
                userName:'Jack',
                sex:'1',
                state:'1',
                interest:'1',
                birthday:'2000-01-01',
                address:'北京市海淀区奥林匹克公园',
                time:'09:00'
            },
            {
                id: '1',
                userName: 'Tom',
                sex: '1',
                state: '1',
                interest: '1',
                birthday: '2000-01-01',
                address: '北京市海淀区奥林匹克公园',
                time: '09:00'
            },
            {
                id: '2',
                userName: 'Lily',
                sex: '1',
                state: '1',
                interest: '1',
                birthday: '2000-01-01',
                address: '北京市海淀区奥林匹克公园',
                time: '09:00'
            },
        ]
        data.map((item,index)=>{
            item.key = index;
        })
        this.setState({
            dataSource: data
        })
        this.request();
    }

    // 动态获取mock数据
    request = ()=>{
        let _this = this;
        axios.ajax({
            url:'/table/list',
            data:{
                params:{
                    page:this.params.page
                }
            }
        }).then((res)=>{
            if(res.code == 0){
                res.result.list.map((item, index) => {
                    item.key = index;
                })
                this.setState({
                    dataSource2:res.result.list,
                    selectedRowKeys:[],
                    selectedRows:null,
                    pagination: Utils.pagination(res,(current)=>{
                        _this.params.page = current;
                        this.request();
                    })
                })
            }
        })
    }

    onRowClick = (record,index)=>{
        let selectKey = [index];
        Modal.info({
            title:'信息',
            content:`用户名：${record.userName},用户爱好：${record.interest}`
        })
        this.setState({
            selectedRowKeys:selectKey,
            selectedItem: record
        })
    }

    // 多选执行删除动作
    handleDelete = (()=>{
        let rows = this.state.selectedRows;
        let ids = [];
        rows.map((item)=>{
            ids.push(item.id)
        })
        Modal.confirm({
            title:'删除提示',
            content: `您确定要删除这些数据吗？${ids.join(',')}`,
            onOk:()=>{
                message.success('删除成功');
                this.request();
            }
        })
    })

    render(){
        const columns = [
            {
                title:'id',
                key:'id',
                dataIndex:'id'
            },
            {
                title: '用户名',
                key: 'userName',
                dataIndex: 'userName'
            },
            {
                title: '性别',
                key: 'sex',
                dataIndex: 'sex',
                render(sex){
                    return sex ==1 ?'男':'女'
                }
            },
            {
                title: '状态',
                key: 'state',
                dataIndex: 'state',
                render(state){
                    let config  = {
                        '1':'咸鱼一条',
                        '2':'风华浪子',
                        '3':'北大才子',
                        '4':'百度FE',
                        '5':'创业者'
                    }
                    return config[state];
                }
            },
            {
                title: '爱好',
                key: 'interest',
                dataIndex: 'interest',
                render(abc) {
                    let config = {
                        '1': '游泳',
                        '2': '打篮球',
                        '3': '踢足球',
                        '4': '跑步',
                        '5': '爬山',
                        '6': '骑行',
                        '7': '桌球',
                        '8': '麦霸'
                    }
                    return config[abc];
                }
            },
            {
                title: '生日',
                key: 'birthday',
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                key: 'address',
                dataIndex: 'address'
            },
            {
                title: '早起时间',
                key: 'time',
                dataIndex: 'time'
            }
        ]
        const selectedRowKeys = this.state.selectedRowKeys;
        const rowSelection = {
            type:'radio',
            selectedRowKeys
        }
        const rowCheckSelection = {
            type: 'checkbox',
            selectedRowKeys,
            onChange:(selectedRowKeys,selectedRows)=>{
                this.setState({
                    selectedRowKeys,
                    selectedRows
                })
            }
        }
        return (
            <div>
                <Card title="基础表格">
                    <Table 
                        bordered
                        columns={columns}
                        dataSource={this.state.dataSource}
                        pagination={false}
                    />
                </Card>
                <Card title="动态数据渲染表格-Mock" style={{margin:'10px 0'}}>
                    <Table
                        bordered
                        columns={columns}
                        dataSource={this.state.dataSource2}
                        pagination={false}
                    />
                </Card>
                <Card title="Mock-单选" style={{ margin: '10px 0' }}>
                    <Table
                        bordered
                        rowSelection={rowSelection}
                        onRow={(record,index) => {
                            return {
                                onClick:()=>{
                                    this.onRowClick(record,index);
                                }
                            };
                        }}
                        columns={columns}
                        dataSource={this.state.dataSource2}
                        pagination={false}
                    />
                </Card>
                <Card title="Mock-单选" style={{ margin: '10px 0' }}>
                    <div style={{marginBottom:10}}>
                        <Button onClick={this.handleDelete}>删除</Button>
                    </div>
                    <Table
                        bordered
                        rowSelection={rowCheckSelection}
                        columns={columns}
                        dataSource={this.state.dataSource2}
                        pagination={false}
                    />
                </Card>
                <Card title="Mock-表格分页" style={{ margin: '10px 0' }}>
                    <Table
                        bordered
                        columns={columns}
                        dataSource={this.state.dataSource2}
                        pagination={this.state.pagination}
                    />
                </Card>
            </div>
        );
    }
}
```




#### 单选表格效果

![12](https://qq292383147.github.io/pictureLibrary/picture/React/单车/26.jpg)

**点击行内任意一处，均有提示**

![13](https://qq292383147.github.io/pictureLibrary/picture/React/单车/27.jpg)

#### 多选表格效果

![14](https://qq292383147.github.io/pictureLibrary/picture/React/单车/28.jpg)

#### 分页表格效果

![15](https://qq292383147.github.io/pictureLibrary/picture/React/单车/29.jpg)

#### ajax封装(get)

**src/axios/index.js**

```js
import JsonP from 'jsonp'
import axios from 'axios'
import { Modal } from 'antd'
export default class Axios {
    static jsonp(options) {
        return new Promise((resolve, reject) => {
            JsonP(options.url, {
                param: 'callback'
            }, function (err, response) {
                if (response.status == 'success') {
                    resolve(response);
                } else {
                    reject(response.messsage);
                }
            })
        })
    }

    static ajax(options){
        let loading;
        if (options.data && options.data.isShowLoading !== false){
            loading = document.getElementById('ajaxLoading');
            loading.style.display = 'block';
        }
        let baseApi = 'https://www.easy-mock.com/mock/5a7278e28d0c633b9c4adbd7/api';
        return new Promise((resolve,reject)=>{
            axios({
                url:options.url,
                method:'get',
                baseURL:baseApi,
                timeout:5000,
                params: (options.data && options.data.params) || ''
            }).then((response)=>{
                if (options.data && options.data.isShowLoading !== false) {
                    loading = document.getElementById('ajaxLoading');
                    loading.style.display = 'none';
                }
                if (response.status == '200'){
                    let res = response.data;
                    if (res.code == '0'){
                        resolve(res);
                    }else{
                        Modal.info({
                            title:"提示",
                            content:res.msg
                        })
                    }
                }else{
                    reject(response.data);
                }
            })
        });
    }
}
```

#### 表格分页：pagination

**render函数return内容：**

```js
<Card title="Mock-表格分页" style={{margin:'10px 0'}}>
    <Table
        bordered
        columns = {columns }
        dataSource={this.state.dataSource2}
        pagination={this.state.pagination}
    />
</Card>
```

**逻辑代码**

```js
state = {
	dataSource2:[]
}

params = {
    page:1
}

componentDidMount(){
  
    this.request();
}

//动态获取mock数据
request = () =>{
    // console.log(111)
    let _this = this;
    axios.ajax({
        url:'/table/list',
        data:{
            params:{
                page:this.params.page
            },
        }
    }).then((res)=>{
        if (res.code == 0){
            res.result.list.map((item,index)=>{
                item.key = index;
            })
            this.setState({
                dataSource2:res.result.list,
                selectedRowKeys:[],
                // selectedIds:ids
                selectedRows:null,
                //分页
                pagination:Utils.pagination(res,(current)=>{
                    //to-do
                    _this.params.page = current;
                    console.log(current)
                    this.request();
                    // console.log('333')
                })
            })
        }
    })
}
```

**Loading：加载数据成功前loading功能**

```js
static ajax(options){
    let loading ;
    //发送请求前加载
    if(options.data && options.data.isShowLoading !== false){
        loading = document.getElementById('ajaxLoading');
        //block显示loading
        loading.style.display = 'block';
    }
    let baseApi = 'https://www.easy-mock.com/mock/5c84ccabcfb6692c295163b4/BikeSharingAPI'
    return new Promise((resolve,reject)=>{
        axios({
            url:options.url,
            method:'get',
            baseURL:baseApi,
            timeout:10000,
            params:(options.data && options.data.params)  || "",
        }).then((response)=>{
            //请求成功后关闭loading
            if(options.data && options.data.isShowLoading !== false){
                loading = document.getElementById('ajaxLoading');
                //none 关闭loading
                loading.style.display = 'none';
            }
            if(response.status=="200"){
                let res = response.data
                if(res.code == '0'){
                    resolve(res);
                }else {
                    Modal.info({
                        title:"提示",
                        content:res.msg
                    })
                }
            }else{
                reject(response.data)
            }
        })
    });
}
```

**发送ajax时isShowLoading：true，也可以不写**

```js
axios.ajax({
            url:'/table/list',
            data:{
                params:{
                    page:this.params.page
                },
                //不想有loading时。默认为true
                // isShowLoading :false,
            }
        }).then((res)=>{
            
        })
    }
```

**发送请求前加载**

```js
  //发送请求前加载
    if(options.data && options.data.isShowLoading !== false){
        loading = document.getElementById('ajaxLoading');
        //block显示loading
        loading.style.display = 'block';
    }
```

**请求成功后关闭loading**

```js
   //请求成功后关闭loading
   if(options.data && options.data.isShowLoading !== false){
       loading = document.getElementById('ajaxLoading');
       //none 关闭loading
       loading.style.display = 'none';
   }
```

**注意：不想有loading时，要设置ShowLoading：false,默认为true**

```js
axios.ajax({
  url:'/table/list',
  data:{
     params:{
         page:this.params.page
     },
     //不想有loading时。默认为true
     // isShowLoading :false,
      }
    }).then((res)=>{
        
  })
}
```

#### 点击行内任意位置，均有提示，可进行增删改查

![16](https://qq292383147.github.io/pictureLibrary/picture/React/单车/30.jpg)

**点击行内任意一处，均有提示**

![17](https://qq292383147.github.io/pictureLibrary/picture/React/单车/31.jpg)

**render里return的标签内容**



```js
render (){
	const {selectedRowKeys} = this.state
    const rowSelection = {
        type:'radio',
        //必写。告诉table组件，选中了那个/那些行
        selectedRowKeys
    }
	<Card title="Mock-单选" style={{margin:'10px 0'}}>
	      <Table
	          bordered
	          rowSelection={rowSelection}
	          onRow={(record,index) => {
	              return {
	                  onClick: () => {
	                      this.onRowClick(record,index)
	                  },       // 点击行
	              };
	          }}
	          columns = {columns }
	          dataSource={this.state.dataSource2}
	          pagination={false}
	      />
	  </Card>
   }
```

**render上的逻辑代码**

```js
//获取每一行里的 item值
  nRowClick = (record,index) =>{
     //多选时用数组
     let selectKey = [index ];
     Modal.info({
         title:'信息',
         content:`用户名：${record.userName},用户爱好:${record.interest}`
     });
     this.setState({
         selectedRowKeys:selectKey,
         //获取item值 可对单个行进行新增删除操作。
         selectedRowItem:record
     })
    }
```

#### checkBox表格多选删除

![18](https://qq292383147.github.io/pictureLibrary/picture/React/单车/32.jpg)

```js
 //多选删除事件
    handleDelete = () =>{
        let rows = this.state.selectedRows;
        let ids = [];
        rows.map((item,index)=>{
            ids.push(item.id)
        })
        Modal.confirm({
            title:'提示',
            content:`您确定要删除这些数据吗？${ids.join(',')}`,
            onOk:()=>{
                message.success('删除成功');
                this.request();
            }
        })
    }

    render (){
        const {selectedRowKeys} = this.state
        const rowCheckSelection = {
            type:'checkbox',
            selectedRowKeys,
            onChange:(selectedRowKeys,selectedRows) =>{
                // let ids = [];
                // selectedRowKeys.map((item,index)=>{
                //     item.key = index;
                //     ids.push(item.id)
                // })
                this.setState({
                    //必写。告诉table组件，选中了那个/那些行
                    selectedRowKeys,
                    // selectedIds:ids
                    selectedRows
                })
        }
        }

        return(
            <div>
                <Card title="Mock-多选" style={{margin:'10px 0'}}>
                    <div style={{marginBottom:10}}>
                        <Button onClick={this.handleDelete}>删除</Button>
                    </div>
                    <Table
                        bordered
                        rowSelection={rowCheckSelection}
                        columns = {columns }
                        dataSource={this.state.dataSource2}
                        pagination={false}
                    />
                </Card>
               
            </div>
        )
    }
```

### 表格-高级表格

#### 源代码

```js
import React from 'react';
import { Card, Table, Modal, Button, message, Badge } from 'antd';
import axios from './../../axios/index'
import Utils from './../../utils/utils';
export default class BasicTable extends React.Component {

    state = {

    }
    params = {
        page:1
    }
    componentDidMount(){
        this.request();
    }

    // 动态获取mock数据
    request = () => {
        let _this = this;
        axios.ajax({
            url: '/table/high/list',
            data: {
                params: {
                    page: this.params.page
                }
            }
        }).then((res) => {
            if (res.code == 0) {
                res.result.list.map((item, index) => {
                    item.key = index;
                })
                this.setState({
                    dataSource: res.result.list
                })
            }
        })
    }

    handleChange = (pagination, filters, sorter)=>{
        console.log("::" + sorter)
        this.setState({
            sortOrder:sorter.order
        })
    }

    // 删除操作
    handleDelete = (item)=>{
        let id = item.id;
        Modal.confirm({
            title:'确认',
            content:'您确认要删除此条数据吗？',
            onOk:()=>{
                message.success('删除成功');
                this.request();
            }
        })
    }

    render(){
        const columns = [
            {
                title: 'id',
                key: 'id',
                width:80,
                dataIndex: 'id'
            },
            {
                title: '用户名',
                key: 'userName',
                width: 80,
                dataIndex: 'userName'
            },
            {
                title: '性别',
                key: 'sex',
                width: 80,
                dataIndex: 'sex',
                render(sex) {
                    return sex == 1 ? '男' : '女'
                }
            },
            {
                title: '状态',
                key: 'state',
                width: 80,
                dataIndex: 'state',
                render(state) {
                    let config = {
                        '1': '咸鱼一条',
                        '2': '风华浪子',
                        '3': '北大才子',
                        '4': '百度FE',
                        '5': '创业者'
                    }
                    return config[state];
                }
            },
            {
                title: '爱好',
                key: 'interest',
                width: 80,
                dataIndex: 'interest',
                render(abc) {
                    let config = {
                        '1': '游泳',
                        '2': '打篮球',
                        '3': '踢足球',
                        '4': '跑步',
                        '5': '爬山',
                        '6': '骑行',
                        '7': '桌球',
                        '8': '麦霸'
                    }
                    return config[abc];
                }
            },
            {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                key: 'address',
                width: 120,
                dataIndex: 'address'
            },
            {
                title: '早起时间',
                key: 'time',
                width: 80,
                dataIndex: 'time'
            }
        ]
        const columns2 = [
            {
                title: 'id',
                key: 'id',
                width: 80,
                fixed:'left',
                dataIndex: 'id'
            },
            {
                title: '用户名',
                key: 'userName',
                width: 80,
                fixed: 'left',
                dataIndex: 'userName'
            },
            {
                title: '性别',
                key: 'sex',
                width: 80,
                dataIndex: 'sex',
                render(sex) {
                    return sex == 1 ? '男' : '女'
                }
            },
            {
                title: '状态',
                key: 'state',
                width: 80,
                dataIndex: 'state',
                render(state) {
                    let config = {
                        '1': '咸鱼一条',
                        '2': '风华浪子',
                        '3': '北大才子',
                        '4': '百度FE',
                        '5': '创业者'
                    }
                    return config[state];
                }
            },
            {
                title: '爱好',
                key: 'interest',
                width: 80,
                dataIndex: 'interest',
                render(abc) {
                    let config = {
                        '1': '游泳',
                        '2': '打篮球',
                        '3': '踢足球',
                        '4': '跑步',
                        '5': '爬山',
                        '6': '骑行',
                        '7': '桌球',
                        '8': '麦霸'
                    }
                    return config[abc];
                }
            },
            {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            },
            {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            }, {
                title: '生日',
                key: 'birthday',
                width: 120,
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                key: 'address',
                width: 120,
                fixed: 'right',
                dataIndex: 'address'
            },
            {
                title: '早起时间',
                key: 'time',
                width: 80,
                fixed: 'right',
                dataIndex: 'time'
            }
        ]
        const columns3 = [
            {
                title: 'id',
                key: 'id',
                dataIndex: 'id'
            },
            {
                title: '用户名',
                key: 'userName',
                dataIndex: 'userName'
            },
            {
                title: '性别',
                key: 'sex',
                dataIndex: 'sex',
                render(sex) {
                    return sex == 1 ? '男' : '女'
                }
            },
            {
                title: '年龄',
                key: 'age',
                dataIndex: 'age',
                sorter:(a,b)=>{
                    return a.age - b.age;
                },
                sortOrder:this.state.sortOrder
            },
            {
                title: '状态',
                key: 'state',
                dataIndex: 'state',
                render(state) {
                    let config = {
                        '1': '咸鱼一条',
                        '2': '风华浪子',
                        '3': '北大才子',
                        '4': '百度FE',
                        '5': '创业者'
                    }
                    return config[state];
                }
            },
            {
                title: '爱好',
                key: 'interest',
                dataIndex: 'interest',
                render(abc) {
                    let config = {
                        '1': '游泳',
                        '2': '打篮球',
                        '3': '踢足球',
                        '4': '跑步',
                        '5': '爬山',
                        '6': '骑行',
                        '7': '桌球',
                        '8': '麦霸'
                    }
                    return config[abc];
                }
            },
            {
                title: '生日',
                key: 'birthday',
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                key: 'address',
                dataIndex: 'address'
            },
            {
                title: '早起时间',
                key: 'time',
                dataIndex: 'time'
            }
        ]
        const columns4 = [
            {
                title: 'id',
                dataIndex: 'id'
            },
            {
                title: '用户名',
                dataIndex: 'userName'
            },
            {
                title: '性别',
                dataIndex: 'sex',
                render(sex) {
                    return sex == 1 ? '男' : '女'
                }
            },
            {
                title: '年龄',
                dataIndex: 'age'
            },
            {
                title: '状态',
                dataIndex: 'state',
                render(state) {
                    let config = {
                        '1': '咸鱼一条',
                        '2': '风华浪子',
                        '3': '北大才子',
                        '4': '百度FE',
                        '5': '创业者'
                    }
                    return config[state];
                }
            },
            {
                title: '爱好',
                dataIndex: 'interest',
                render(abc) {
                    let config = {
                        '1': <Badge status="success" text="成功"/>,
                        '2': <Badge status="error" text="报错" />,
                        '3': <Badge status="default" text="正常" />,
                        '4': <Badge status="processing" text="进行中" />,
                        '5': <Badge status="warning" text="警告" />
                    }
                    return config[abc];
                }
            },
            {
                title: '生日',
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                dataIndex: 'address'
            },
            {
                title: '操作',
                render:(text,item)=>{
                    return <Button size="small" onClick={(item) => { this.handleDelete(item) }}>删除</Button>
                }
            }
        ]
        return (
            <div>
                <Card title="头部固定">
                    <Table
                        bordered
                        columns={columns}
                        dataSource={this.state.dataSource}
                        pagination={false}
                        scroll={{y:240}}
                    />
                </Card>
                <Card title="左侧固定" style={{ margin: '10px 0' }}>
                    <Table
                        bordered
                        columns={columns2}
                        dataSource={this.state.dataSource}
                        pagination={false}
                        scroll={{ x: 2650 }}
                    />
                </Card>
                <Card title="表格排序" style={{ margin: '10px 0' }}>
                    <Table
                        bordered
                        columns={columns3}
                        dataSource={this.state.dataSource}
                        pagination={false}
                        onChange={this.handleChange}
                    />
                </Card>
                <Card title="操作按钮" style={{ margin: '10px 0' }}>
                    <Table
                        bordered
                        columns={columns4}
                        dataSource={this.state.dataSource}
                        pagination={false}
                    />
                </Card>
            </div>
        )
    }
}
```

#### 头部固定

![19](https://qq292383147.github.io/pictureLibrary/picture/React/单车/33.jpg)

```
table标签里设置scroll={{scroll={{y:240}}
```


**y：y轴、240:y轴长度**

```js
<Card title="头部固定">
    <Table
        bordered
        columns={columns }
        dataSource={this.state.dataSource}
        pagination={false}
        scroll={{y:240}}
    />
</Card>
```

#### 两侧固定

```
table标签里设置scroll={{scroll={{x:1050}}

x：x轴、1050:x轴总宽度，width之和
```

```js
<Card title="左侧固定" style={{margin: '10px 0'}}>
    <Table
        bordered
        columns={columns2 }
        dataSource={this.state.dataSource}
        pagination={false}
        scroll={{x:1050}}
    />
</Card>
```

**在标题栏下设置fixed：'left';fixed：'right'**

```js
 const columns2 = [
     {
         title: 'id',
         dataIndex: 'id',
         width:80,
         fixed:'left'
     },
     {
         title: '用户名',
         dataIndex: 'userName',
         fixed:'left',
         width:80,
     },
     {
         title: '性别',
         dataIndex: 'sex',
         render(sex){
             return sex == 1 ? '男' : '女'
         },
         width:80,
     },
     {
         title: '生日',
         width:120,
         dataIndex: 'birthday'
     },

     {
         title: '早起时间',
         dataIndex: 'time',
         width:80,
     },
     {
         title: '地址',
         width:120,
         fixed:'right',
         dataIndex: 'address',
     },
   ]
```

**若中间有缝隙，可增加标题种类**

![20](https://qq292383147.github.io/pictureLibrary/picture/React/单车/34.jpg)

```
若中间有过度太窄，修改scroll={{x：1050}}，修改width之和
```


#### 年龄排序

![21](https://qq292383147.github.io/pictureLibrary/picture/React/单车/35.jpg)

```js
    render() {
        
    const columns3 = [
        {
            title: 'id',
            dataIndex: 'id',
            width:80,
            fixed:'left'
        },
        {
            title: '用户名',
            dataIndex: 'userName',
            fixed:'left',
            width:80,
        },
        {
            title: '性别',
            dataIndex: 'sex',
            render(sex){
                return sex == 1 ? '男' : '女'
            },

        },
        {
            title: '年龄',
            dataIndex: 'age',
            width:80,

            //升序 降序 功能实现 加两个参数
            sorter:(a,b)=>{
                return a.age-b.age;
            },
            sortOrder:this.state.sortOrder
        },
        {
            title: '状态',
            dataIndex: 'state',
            width:80,
            render(state){
                let config = {
                    '1': '咸鱼一条',
                    '2': '天才',
                    '3': '最强大脑',
                    '4': '码奴',
                    '5': '旅行家',
                }
                return config[state]
            }
        },
        {
            title: '爱好',
            width:80,
            dataIndex: 'interest',
            render(ABC){
                let config = {
                    '1': '游泳',
                    '2': '打球',
                    '3': '慢跑',
                    '4': '听歌',
                    '5': '看书',
                    '6': '看电影',
                    '7': '旅行',
                    '8': '学习',
                }
                return config[ABC]
            }
        },
        {
            title: '生日',

            dataIndex: 'birthday'
        },
        {
            title: '地址',
            width:120,
            dataIndex: 'address',
        },
        {
            title: '早起时间',
            dataIndex: 'time',

        },
        {
            title: '生日',
            width:120,
            dataIndex: 'birthday'
        },

        {
            title: '早起时间',
            dataIndex: 'time',
            width:80,
        },
        {
            title: '地址',
            width:120,
            fixed:'right',
            dataIndex: 'address',
        },
    ]
    
    return (
        <div>
            <Card title="年龄排序" style={{margin: '10px 0'}}>
                <Table
                    bordered
                    columns={columns3 }
                    dataSource={this.state.dataSource}
                    pagination={false}
                    scroll={{x:1100}}
                    onChange={this.handleChange}
                />
            </Card> 
        </div>
    )
  }
```

**升序/降序功能的实现，加两个参数`sorter`和`sortOrder`**

```js
 {
   title: '年龄',
   dataIndex: 'age',
   width:80,

   //升序 降序 功能实现 加两个参数
   sorter:(a,b)=>{
       return a.age-b.age;
   },
   sortOrder:this.state.sortOrder
},
```

**逻辑代码**

```js
handleChange = (pagination,filers,sorter)=> {
        console.log(sorter)
        this.setState({
           sortOrder: sorter.order
        })
 }
```

#### 按钮操作-删除

![22](https://qq292383147.github.io/pictureLibrary/picture/React/单车/36.jpg)

```js
    render() { 
        const columns4 = [
            {
                title: 'id',
                dataIndex: 'id',
                fixed:'left'
            },
            {
                title: '用户名',
                dataIndex: 'userName',

            },
            {
                title: '性别',
                render(sex){
                    return sex == 1 ? '男' : '女'
                },

            },
            {
                title: '年龄',
                dataIndex: 'age',
            },

            {
                title: '状态',
                dataIndex: 'state',
                render(state){
                    let config = {
                        '1': '咸鱼一条',
                        '2': '天才',
                        '3': '最强大脑',
                        '4': '码奴',
                        '5': '旅行家',
                    }
                    return config[state]
                }
            },
            {
                title: '爱好',
                dataIndex: 'interest',
                render(ABC){
                    let config = {
                        '1': <Badge status="success" text="成功"/>,
                        '2': <Badge status="error" text="报错"/>,
                        '3': <Badge status="default" text="正常"/>,
                        '4': <Badge status="processing" text="进行中"/>,
                        '5': <Badge status="warning" text="警告"/>,
                        '6': <Badge status="default" text="正常"/>,
                        '7': <Badge status="processing" text="进行中"/>,
                        '8': <Badge status="warning" text="警告"/>,

                    }
                    return config[ABC]
                }
            },
            {
                title: '生日',
                dataIndex: 'birthday'
            },
            {
                title: '地址',
                dataIndex: 'address',
            },
            {
                title: '早起时间',
                dataIndex: 'time',
            },
            {
                title: '操作',
                dataIndex: 'time',
                //注意使用箭头函数 否则会找不到下面的this
                render:(text,item)=>{
                    return <Button  size='small'onClick={(item)=>{this.handleDelete(item)}}>删除</Button>
                }
            },


        ]

        return (
            <div>
                <Card title="操作按钮" style={{margin: '10px 0'}}>
                    <Table
                        bordered
                        columns={columns4}
                        dataSource={this.state.dataSource}
                        pagination={false}
                        onChange={this.handleDelete}
                    />
                </Card>
            </div>
        )
    }
```

**逻辑代码**

```js
//删除操作
    handleDelete = (item) =>{
        let id = item.id;
        Modal.confirm({
            title:'确认',
            content:'您确认要删除磁条数据吗？',
            onOK:()=>{
                message.success('删除成功');
                this.request();
            }
        })
    }
```

**Badge样式：** 

![23](https://qq292383147.github.io/pictureLibrary/picture/React/单车/37.jpg)

```js
{
   title: '爱好',
    dataIndex: 'interest',
    render(ABC){
        let config = {
            '1': <Badge status="success" text="成功"/>,
            '2': <Badge status="error" text="报错"/>,
            '3': <Badge status="default" text="正常"/>,
            '4': <Badge status="processing" text="进行中"/>,
            '5': <Badge status="warning" text="警告"/>,
            '6': <Badge status="default" text="正常"/>,
            '7': <Badge status="processing" text="进行中"/>,
            '8': <Badge status="warning" text="警告"/>,

        }
        return config[ABC]
    }
},
```

### 富文本编辑

#### 介绍

富文本编辑器Rich Text Editor,简称RTE,是一种可内嵌于浏览器，所见即所得的文本编辑器 

![24](https://qq292383147.github.io/pictureLibrary/picture/React/单车/38.jpg)

#### 安装插件

**react-draft-wysiwyg：文本编辑器插件**

**draftjs-to-html：文本转换为html的插件**

```
yarn add react-draft-wysiwyg draftjs-to-html --save
```

#### 代码实现

**pages-rich-index.js：对应路由/admin/rich**

```js
import React from 'react'
import {Button,Card,Modal} from 'antd'
import {Editor} from 'react-draft-wysiwyg'
import 'react-draft-wysiwyg/dist/react-draft-wysiwyg.css'
import draftjs from 'draftjs-to-html'
export default class RichText extends React.Component{

    state = {
        showRichText:false,
        editorContent: '',
        editorState: '',
    };

    handleClearContent = ()=>{  //清空文本
        this.setState({
            editorState:''
        })
    }

    handleGetText = ()=>{   //获取文本内容
        this.setState({
            showRichText:true
        })
    }

    onEditorChange = (editorContent) => {   //编辑器的状态
        this.setState({
            editorContent,
        });
    };

    onEditorStateChange = (editorState) => {    //编辑器内容状态
        this.setState({
            editorState
        });
    };

    render(){
        const { editorContent, editorState } = this.state;
        return (
            <div>
                <Card style={{marginTop:10}}>
                    <Button type="primary" onClick={this.handleClearContent}>清空内容</Button>
                    <Button type="primary" onClick={this.handleGetText}>获取HTML文本</Button>
                </Card>
                <Card title="富文本编辑器">
                    <Editor
                        editorState={editorState}
                        onContentStateChange={this.onEditorChange}
                        onEditorStateChange={this.onEditorStateChange}
                    />
                </Card>
                <Modal
                    title="富文本"
                    visible={this.state.showRichText}
                    onCancel={()=>{
                        this.setState({
                            showRichText:false
                        })
                    }}
                    footer={null}
                >
                    {draftjs(this.state.editorContent)}
                </Modal>
            </div>
        );
    }
}
```

### 城市管理页面

#### 页面效果

![25](https://qq292383147.github.io/pictureLibrary/picture/React/单车/39.jpg)

#### Easy Mock城市管理的数据接口

```js
{
  "code": 0,
  "msg": "",
  "result": {
    "item_list|10": [{
      "id|+1": 1,
      "name": "@city",
      "mode|1-2": 1,
      "op_mode|1-2": 1,
      "franchisee_id": 77,
      "franchisee_name": "松果自营",
      "city_admins|1-2": [{
        "user_name": "@cname",
        "user_id|+1": 10001
      }],
      "open_time": "@datetime",
      "sys_user_name": "@cname",
      "update_time": 1546580667000
    }]
  },
  page: 1,
  page_size: 10,
  total: 20
}
```

#### 顶部子组件一：选择表单

```js
class FilterForm extends React.Component{
 
    render(){
        const { getFieldDecorator } = this.props.form;
        return (
            <Form layout="inline">
                <FormItem label="城市">
                    {
                        getFieldDecorator('city_id')(
                            <Select
                                style={{width:100}}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">北京市</Option>
                                <Option value="2">天津市</Option>
                                <Option value="3">深圳市</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="用车模式">
                    {
                        getFieldDecorator('mode')(
                            <Select
                                style={{ width: 120 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">指定停车点模式</Option>
                                <Option value="2">禁停区模式</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="营运模式">
                    {
                        getFieldDecorator('op_mode')(
                            <Select
                                style={{ width: 80 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">自营</Option>
                                <Option value="2">加盟</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="加盟商授权状态">
                    {
                        getFieldDecorator('auth_status')(
                            <Select
                                style={{ width: 100 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">已授权</Option>
                                <Option value="2">未授权</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem>
                    <Button type="primary" style={{margin:'0 20px'}}>查询</Button>
                    <Button>重置</Button>
                </FormItem>
            </Form>
        );
    }
}
FilterForm = Form.create({})(FilterForm);
```

#### componentDidMount()

**调用this.requestList(),默认请求接口数据**

```js
 componentDidMount() {
    this.requestList();
  }

  // 默认请求我们的接口数据
  requestList = ()=>{
    let _this = this;
    axios.ajax({
      url: '/open_city',
      data:{
        params:{
          page:this.params.page
        }
      }
    }).then((res)=>{
      let list = res.result.item_list.map((item, index) => {
        item.key = index;
        return item; // 注:这里要返回item的值
      });
      this.setState({
        list:list,
        pagination:Utils.pagination(res,(current)=>{
          _this.params.page = current;
          _this.requestList();
        })
      })
    })
  }
  
  render(){
      ...
  }
```

![26](https://qq292383147.github.io/pictureLibrary/picture/React/单车/40.jpg)

#### 开通城市-弹框功能

为以上组件,增加点击按钮 弹窗(Modal)功能

**[开通城市]按钮:监听 onClick 事件,调用this.handleOpenCity()显示弹框**

```js
state = {
    list:[],
   isShowOpenCity:false      // 默认不可见
}

// 开通城市
 handleOpenCity = ()=>{
    this.setState({
            isShowOpenCity:true
    })
 }
```

**Modal部分默认隐藏，触发事件进行显示**

**onOk：点击确定回调，参数为关闭函数**

**onCancel：取消回调，参数为关闭**

```js
<Modal
       title="开通城市"
       visible={this.state.isShowOpenCity}
       onCancel={()=>{
           this.setState({
                isShowOpenCity:false
           })
       }}
       onOk={this.handleSubmit}
>
       <OpenCityForm wrappedComponentRef={(inst)=>{this.cityForm = inst;}}/>
</Modal>
```

wrapperComponentRef属性：

**拿到表单中的信息对象inst，通过this.cityForm存到state中**

**经过Form.create之和如果要拿到ref,可以使用rc-form提供的wrappedComponentRef,详细内容可以查看这里**

```js
class CustomizedForm extends React.Component {...}
// use wrappedComponentRef
const EnhancedForm = Form.create()(CustomizedFrom);
<EnhancedFrom wrappedComponentRef={(form)=>this.form=from}/>
this.form // => The instance of CustomizedForm
```

**城市开通提交**

```js
// 城市开通提交
handleSubmit = ()=>{
        let cityInfo = this.cityForm.props.form.getFieldsValue();
        console.log(cityInfo);
        axios.ajax({
            url:'/city/open',
            data:{
                params:cityInfo
            }
        }).then((res)=>{
            if(res.code === 0){
                message.success('开通成功');
                this.setState({
                    isShowOpenCity:false
                })
                this.requestList();
            }
        })
}
```

**弹框子组件二：开通城市表单**

```js
class OpenCityForm extends React.Component {
  render() {
    const formItemLayout = {
      labelCol: {
        span: 5
      },
      wrapperCol: {
        span: 19
      }
    };
    const {getFieldDecorator} = this.props.form;
    return (
      <Form layout="horizontal">
        <FormItem label="选择城市"  {...formItemLayout}>
          {
            getFieldDecorator('city_id', {
              initialValue: '1'
            })(
              <Select style={{width: 100}}>
                <Option value="">全部</Option>
                <Option value="1">北京市</Option>
                <Option value="2">天津市</Option>
              </Select>
            )
          }
        </FormItem>
        <FormItem label="营运模式"  {...formItemLayout}>
          {
            getFieldDecorator('op_mode', {
              initialValue: '1'
            })(
              <Select style={{width: 100}}>
                <Option value="1">自营</Option>
                <Option value="2">加盟</Option>
              </Select>
            )
          }

        </FormItem>
        <FormItem label="用车模式"  {...formItemLayout}>
          {
            getFieldDecorator('use_mode', {
              initialValue: '1'
            })(
              <Select style={{width: 100}}>
                <Option value="1">指定停车点</Option>
                <Option value="2">禁停区</Option>
              </Select>
            )
          }
        </FormItem>
      </Form>
    );
  }
}

OpenCityForm = Form.create({})(OpenCityForm);
```

**Easy Mock城市管理的数据接口：**

```js
{
  "code": 0,
  "list": "开通成功"
    
}
```

#### 实例代码

```js
import React from 'react';
import { Card, Button, Table, Form, Select, Modal, message } from 'antd';
import axios from './../../axios/index';
import Utils from './../../utils/utils';
const FormItem = Form.Item;
const Option = Select.Option;
export default class City extends React.Component{

    state = {
        list:[],
        isShowOpenCity:false
    }
    params = {
        page:1
    }
    componentDidMount(){
        this.requestList();
    }

    // 默认请求我们的接口数据
    requestList = ()=>{
        let _this = this;
        axios.ajax({
            url: '/open_city',
            data:{
                params:{
                    page:this.params.page
                }
            }
        }).then((res)=>{
            let list = res.result.item_list.map((item, index) => {
                item.key = index;
                return item;
            });
            this.setState({
                list:list,
                pagination:Utils.pagination(res,(current)=>{
                    _this.params.page = current;
                    _this.requestList();
                })
            })
        })
    }

    // 开通城市
    handleOpenCity = ()=>{
        this.setState({
            isShowOpenCity:true
        })
    }
    // 城市开通提交
    handleSubmit = ()=>{
        let cityInfo = this.cityForm.props.form.getFieldsValue();
        console.log(cityInfo);
        axios.ajax({
            url:'/city/open',
            data:{
                params:cityInfo
            }
        }).then((res)=>{
            if(res.code == '0'){
                message.success('开通成功');
                this.setState({
                    isShowOpenCity:false
                })
                this.requestList();
            }
        })
    }
    render(){
        const columns = [
            {
                title:'城市ID',
                dataIndex:'id'
            }, {
                title: '城市名称',
                dataIndex: 'name'
            }, {
                title: '用车模式',
                dataIndex: 'mode',
                render(mode){
                    return mode ==1 ?'停车点':'禁停区';
                }
            }, {
                title: '营运模式',
                dataIndex: 'op_mode',
                render(op_mode) {
                    return op_mode == 1 ? '自营' : '加盟';
                }
            }, {
                title: '授权加盟商',
                dataIndex: 'franchisee_name'
            }, {
                title: '城市管理员',
                dataIndex: 'city_admins',
                render(arr){
                    return arr.map((item)=>{
                        return item.user_name;
                    }).join(',');
                }
            }, {
                title: '城市开通时间',
                dataIndex: 'open_time'
            }, {
                title: '操作时间',
                dataIndex: 'update_time',
                render: Utils.formateDate
            }, {
                title: '操作人',
                dataIndex: 'sys_user_name'
            }
        ]
        return (
            <div>
                <Card>
                    <FilterForm />
                </Card>
                <Card style={{marginTop:10}}>
                    <Button type="primary" onClick={this.handleOpenCity}>开通城市</Button>
                </Card>
                <div className="content-wrap">
                    <Table
                        bordered
                        columns={columns}
                        dataSource={this.state.list}
                        pagination={this.state.pagination}
                    />
                </div>
                <Modal 
                    title="开通城市"
                    visible={this.state.isShowOpenCity}
                    onCancel={()=>{
                        this.setState({
                            isShowOpenCity:false
                        })
                    }}
                    onOk={this.handleSubmit}
                >
                    <OpenCityForm wrappedComponentRef={(inst)=>{this.cityForm = inst;}}/>
                </Modal>
            </div>
        );
    }
}

class FilterForm extends React.Component{

    render(){
        const { getFieldDecorator } = this.props.form;
        return (
            <Form layout="inline">
                <FormItem label="城市">
                    {
                        getFieldDecorator('city_id')(
                            <Select
                                style={{width:100}}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">北京市</Option>
                                <Option value="2">天津市</Option>
                                <Option value="3">深圳市</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="用车模式">
                    {
                        getFieldDecorator('mode')(
                            <Select
                                style={{ width: 120 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">指定停车点模式</Option>
                                <Option value="2">禁停区模式</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="营运模式">
                    {
                        getFieldDecorator('op_mode')(
                            <Select
                                style={{ width: 80 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">自营</Option>
                                <Option value="2">加盟</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="加盟商授权状态">
                    {
                        getFieldDecorator('auth_status')(
                            <Select
                                style={{ width: 100 }}
                                placeholder="全部"
                            >
                                <Option value="">全部</Option>
                                <Option value="1">已授权</Option>
                                <Option value="2">未授权</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem>
                    <Button type="primary" style={{margin:'0 20px'}}>查询</Button>
                    <Button>重置</Button>
                </FormItem>
            </Form>
        );
    }
}
FilterForm = Form.create({})(FilterForm);

class OpenCityForm extends React.Component{
    render(){
        const formItemLayout = {
            labelCol:{
                span:5
            },
            wrapperCol:{
                span:19
            }
        }
        const { getFieldDecorator }  =this.props.form;
        return (
            <Form layout="horizontal">
                <FormItem label="选择城市" {...formItemLayout}>
                    {
                        getFieldDecorator('city_id',{
                            initialValue:'1'
                        })(
                            <Select style={{ width: 100 }}>
                                <Option value="">全部</Option>
                                <Option value="1">北京市</Option>
                                <Option value="2">天津市</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="营运模式" {...formItemLayout}>
                    {
                        getFieldDecorator('op_mode', {
                            initialValue: '1'
                        })(
                            <Select style={{ width: 100 }}>
                                <Option value="1">自营</Option>
                                <Option value="2">加盟</Option>
                            </Select>
                        )
                    }
                </FormItem>
                <FormItem label="用车模式" {...formItemLayout}>
                    {
                        getFieldDecorator('use_mode', {
                            initialValue: '1'
                        })(
                            <Select style={{ width: 100 }}>
                                <Option value="1">指定停车点</Option>
                                <Option value="2">禁停区</Option>
                            </Select>
                        )
                    }
                </FormItem>
            </Form>
        );
    }
}
OpenCityForm = Form.create({})(OpenCityForm);
```