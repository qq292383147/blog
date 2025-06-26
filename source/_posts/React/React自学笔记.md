---
title: React自学笔记
date: 2019-05-23 15:02:00
tags: React & React Native
categories: React & React Native
---


React 核心概念

> 1、虚拟DOM（Virtual DOM）
> 2、Diff 算法（Diff Algorithm）
> 3、单向数据流渲染（Data Flow）
> 4、组件生命周期
> 5、JSX
> 6、一切皆为组件



搭建开发环境


```bash
mkdir react-demo

cd react-demo

npm init -y

npm install react react-dom -S

npm install webpack webpack-cli webpack-dev-server babel babel-cli babel-core babel-loader babel-preset-react babel-preset-env babel-preset-es2015 -D
(解析jsx和es6语法)
```


<h2>webpack.config.js</h2>


```js
module.exports = {
    entry: './main.js',
    output: {
        path: '/',
        filename: 'index.js',
    },
    module:{
        rules:[{
            test: /\.js?$/,
            use: {
                loader: 'babel-loader',
                options:{
                    prosets:['env','react','es2015']
                }
            }
        }]
    }
}
```

<h2>index.html</h2>

```html
<html>
<head>
    <meta></meta>    
    <title>React App</title>
    
</head>
<body>
	<div id="root"></div>
    <script src="index.js"></script>
</body>
</html>
```

<h2>main.js</h2>

```js
// 1. 要通过class创建组件，首先要引入Component这个类，以后创建的组件都需要继承这个类
import React, {Component} from 'react';
// react-dom 包提供了DOM特定的方法，可以在你的应用程序的顶层使用，如果你需要的话，也可以作为React模型之外的特殊操作DOM接口
import ReactDOM from 'react-dom';

// render方法有两个参数，第一个参数时要渲染的内容（组件），第二个参数时这个组件要渲染到的地方
ReactDOM.render(
  <h1>hello world</h1>
  document.getElementById('root'));

```

<h2>package.json</h2>

```json
"start": "webpack-dev-server --inline --hot --open --port 8090 --mode development"
```

<h2>React开发脚手架</h2>

```shell
npm install -g create-react-app // 推荐使用
create-react-app my-testproject(这是你的项目名)
cd create-react-app
npm start [or] yarn start
```

<h2>JSX</h2>

1.1基本使用

```js
const element = <h1>Hello,world</h1>;
```

这种看起来可能有些奇怪的标签语法既不是字符串也不是HTML。

它被称为JSX，一种JavaScript的语法扩展，我们推荐在React中使用JSX来描述用户界面



1.2嵌套元素

注意：只能包含一个根节点

```js
ReactDOM.render(
	// 模板只能包含一个根节点
	<div>
		<h1>hello</h1>
		<h2>jack</h2>
	</div>
	document.getElementById('root')
)
```

1.3表达式

```js
import React, {Component} from 'react';
import ReactDOM from 'react-dom';

// jsx表达式 通过{}来使用，和vue当中的{{}}很类似，它也有它的合法使用方式
// 1. 直接在{}里面写一个变量
// 2. 数字的运算
// 3. 字符串拼接
// 4. 三元运算符，（注意if-else语句不行）
// 5. 函数

// const element = <h1>hello world</h1>
// 注意jsx语法中只能包含一个根节点·
const STR = 'hello world11'
let age = 18

function test(age, str) {
  return age + str
}
ReactDOM.render(
<div>
	<div>{STR}</div>
	<div>{1 + 2}</div>
    <div>{'李' + 'jack'}</div>
    <div>{age >= 18 ? '已成年' : '未成年'}</div>
    <div>{test(23, 'jack')}</div>
</div>
document.getElementById('root')）
```

1.4注释

```js
   1. { // 单行注释 }
   2. { /**/ 多行注释 }
注意：{} 这是注释开始于结束
```

1.5属性

因为JSX的特性更接近Javascript而不是HTML，所以React DOM使用camelCase 小驼峰命名来定义属性的名称，而不是使用html的属性名称

1.html的class属性改为className

2.html中label标签的for属性改为htmlFor

3.标签中的自定义属性使用data-开头

```js
// 图片要写成这样
import avatar from './avatar.jpg'
<img src={avatar} alt=""/>
    
    
{/* 在jsx中，想要加类得通过className来加，不能直接写class */}
<div className="test">hahaa</div>
{/* label的for属性变成htmlFor */}
<label htmlFor="sex">性别</label>
<input type="text" id="sex" />
{/* a标签的tabindex属性变成了tabIndex */}
<a href="http://www.w3school.com.cn/" tabIndex="2">W3School</a>
<a href="http://www.google.com/" tabIndex="1">Google</a>
```

1.6函数方式创建组件

注意：创建组件，组件名一定要大写，函数名作为组件名使用

在函数内部必须要return一些内容,如果没有东西返回，必须return null

在函数式组中，要想获取从父组件传递过来的属性，需要通过一个参数，props

```js
const Hello =( props )=>{
    return (
        <div>
    	<div>hello world function</div>
        <div>hello {props.name}: {props.age}</div>
    	<p>dddccgggee</p>
        </div>
    )
}
// 传递变量
let name = 'rose'
let age = 12

// 传递对象
let user = {
    name: 'rose',
    age: 18
}

ReactDOM.render(
//<Hello/>,
//传递变量<Hello name={name} age={age}/>,
//传递对象
<Hello {...user} />
//如果是要打注释，必须加div标签包裹
document.getElementById('root');
)
```

通过class创建组件

1.要通过class创建组件，首先要引入Component这个类，以后创建的组件都需要继承这个类

```js
import React, { Component } from ‘react’;

class Hello extends Component {
 render(){
  return (
	<div>hello</div>  
  )
 }
}

```

2.第二种方法获取props中的值,使用内置的方法

```js
class Hello extends Component {
	componentWillMount(){  // 这个是生命周期
        console.log(this.props);
	}
	render(){
        return (
          <div>hello {this.props.name}</div>
        )
	}
}
ReactDOM.render(
 <Hello name='rose' age='22' />
 document.getElementById('root')
);
```

props

作用：props给组件传递数据，一般用在父子组件之间

注意：props是只读的，无法给props添加或修改属性

props.children：获取组件的内容，比如：`<Hello>组件内容</Hello>`中的组件内容

```react
class Test extends Component {
    render(){
        return (
            {/* this.props.children指的是这个组件在使用的使用，他的innerTHML位置的内容 */}
        	<div>{ this.props.children }</div>
        )
    }
}

class App extends Component {
    render(){
        return (
         <div>
         	<Test>
         	  <p>sssss</p>
         	  <p>sssss</p>
         	  <p>sssss</p>
         	  <p>sssss</p>
         	  <h1>111155</h1>
         	</Test>
         </div>
        )
    }
}
```



## 默认属性

给类（或者函数）绑定一个defaultProps属性

```js
Test.defaultProps = {
    name: 'default name'
}
```



## 属性效验

```shell
npm i pro-types -S
```



## 组件生命周期

![](https://qq292383147.github.io/pictureLibrary/picture/React/React的生命周期.jpg)



```react native
import PropTypes from 'prop-types'

Hello.proptypes = {
    name: Proptypes.string,
    age: Proptypes.number.isRequired
}
```

注意： propTypes 和 ProTypes

## state

作用：用来给组件提供组件内部使用的数据

注意： 

1、只有通过class创建的组件才具有状态

2、状态是私有的，完全由组件来控制

3、state只能在构造函数中添加

```react native
import React, {Component} from 'react';
import ReactDom from 'react-dom';

class Hello extends Component {
    constructor(props) { // state只能在构造函数中添加
      // 调用Component中的构造函数 -> 父组件
      super(props)
      this.state ={
          country: 'china'
      }
    }
}

class App extends Component {
    render(){
        return (
            {this.state.country}
        )
    }
}
```

 

```
唯一可以分配this.state 的地方是构造函数

不要直接修改state(状态)，类似于这样this.state.comment = "Hello" ， 用setState() 代替:

this.setState({ comment: 'Hello' })

this.setState() 方法更新是异步的，此时需要给它传递第二个参数，即一个回调来在更新之后执行

```



```react native
class App extends Component {
    constructor(props) {
        super(props)
        this.state = {
            val: 'hello neil'
        }
        this.handleClick = this.handleClick.bind(this)
    }
    handleClick(){
        this.setState({
            val: 'hello world'
        })
        // this.setState()是异步的，所以这里的console.log打印出来并不是想要的
        console.log(this.state.val);
    }
    render(){
        return {
            <button onClick = {() => this.handleClick}>{this.state.val}></button>
        }
    }
}




{/*----------------------------------------------------------------------*/}
render(){
    return (
      <div>
        {/*这个this.state.name表示的是Test组件中state的name的值*/}
        {this.state.name}
        {/*this.props.name表示Test组件中name属性的值的，这个值是从App组件中的state的name值传递过去的*/}
        {this.props.name}
      </div>
    )
}

class App extends Component {
    constructor(props) {
        super(props)
        this.state = {
            name : 'rose'
        }
    }
}

render(){
    return (
     <div>
       {/*这个this.state.name表示的是app组件中的state的name的值*/}
       {this.state.name}
       <Test name={this.state.name}>
       </Test>
     </div>
    )
}
```



组件的state(状态)可以向下传递，作为其子组件的props(属性)，通常称为一个“从上到下”，或者单向的数据流

## 函数式组件和类组件的区别

不同： 类允许我们在其中添加本地状态（state）和生命周期钩子  --- s

相同：里面props 是只读的，无法修改



重点： 我们在开发的时候，凡是没有state的组件，就一定要使用函数式组件

使用函数的方式创建的组件更易于测试和数据的维护。也就是说，只要我们的组件没有state，我们就要使用函数式组件（也叫无状态组件）



## React渲染列表数据

```react
class App extends Component {
    constructor(props){
        super(props)
        this.state = {
            commentList: [
                {user:'张三',content: '1 a'},
                {user:'李四',content: '2 b'},
                {user:'老五',content: '3 c'},
                {user:'老六',content: '4 d'},
                {user:'老七',content: '5 e'},
            ]
        }
    }
}

render(){
    return (
        <div>
        <h1>评论列表</h1>
            {this.state.commentList.map((item,index) =>{
                return (
                    <div key={index}>
                        <h3>{item.user}</h3>
                        <p>{item.content}</p>
                    </div>
                )
            })}
        </div>
    )
}
export default App;
```

优化1-函数式组件

```react
class App extends Component {
    constructor(props){
        super(props)
        this.state = {
            commentList: [
                {user:'张三',content: '1 a'},
                {user:'李四',content: '2 b'},
                {user:'老五',content: '3 c'},
                {user:'老六',content: '4 d'},
                {user:'老七',content: '5 e'},
            ]
        }
    }
}

createList = () => {
   return {this.state.commentList.map((item,index) =>{
   return (
       <div key={index}>
          <h3>{item.user}</h3>
          <p>{item.content}</p>
        </div>
     )
   })}
}

render(){
    return (
        <div>
        <h1>评论列表</h1>
		{this.creatList()}
        </div>
    )
}
export default App;
```

优化2-类组件

```react
class NumberList extends Component {
    constructor(props){
        super(props)
    }
    render(){
        return (
            this.props.list.map((item,index) => {
                return (
				<Comment {...item}/>
                )
            })
        )
    }
}

class Comment extends Component {
    render(){
        return (
            <div>
                <h3>{this.props.user}</h3>
                <p>{this.props.conten t}</p>
            </div>
        )
    }
}

class App extends Component {
    constructor(props){
        super(props)
        this.state = {
            commentList: [
                {user:'张三',content: '1 a'},
                {user:'李四',content: '2 b'},
                {user:'老五',content: '3 c'},
                {user:'老六',content: '4 d'},
                {user:'老七',content: '5 e'},
            ]
        }
    }
}

render(){
    return (
        <div>
        <h1>评论列表</h1>
            <NumberList list={this.state.commentList}></NumberList>
        </div>
    )
}
export default App;
```

优化3 -- 推荐使用

```react
const NumberList = (props) => {
    return props.list.map((item,index) => <Comment {...item} key={index}/>)
}

const Comment = (props) => {
    return (
    <div>
     <h3>{this.props.user}</h3>
     <p>{this.props.content}</p>
    </div>
    )
}


class App extends Component {
    constructor(props){
        super(props)
        this.state = {
            commentList: [
                {user:'张三',content: '1 a'},
                {user:'李四',content: '2 b'},
                {user:'老五',content: '3 c'},
                {user:'老六',content: '4 d'},
                {user:'老七',content: '5 e'},
            ]
        }
    }
}

render(){
    return (
        <div>
        <h1>评论列表</h1>
            <NumberList list={this.state.commentList}></NumberList>
        </div>
    )
}
export default App;
```

## 监听事件

React事件使用驼峰命名

通过JSX，你传递一个函数作为事件处理程序

```react
<button onClick={activateLasers}>
 Activate Lasers
</button>
```

绑定this(类方法中没有绑定this)

1、在构造函数中绑定（建议）

```react
constructor(props){
    super(props);
    this.state = { isToggleOn: true };
    
    // 这个绑定是必要的，使this在回调中起作用
    this.handleClick = this.handleClick.bind(this);
}
handleClick(){
    this.setState(prevState =>({
        isToggleOn: !prevState.isToggleOn
    }))
}
```



```react
class App extends Component {
    constructor(props) {
        super(props)
        this.state = {
            name:'rove'
        }
        // 可将以下方法写在button里
        //this.changeName = this.changeName.bind(this)
    }
    changeName(){
        this.setState({name:'Rose'})
    }
}

render(){
    return(
    <div>
     <h1>{this.state.name}</h1>
     {/*在React中监听事件都是使用驼峰命名法，比如onClick，onKeyUp...*/}
     <button onclick={this.changeName.bind(this)}>改变name</button>
    </div>
    )
}
export default App;
```

2、使用箭头函数(属性初始化语法)

```react
class LoggingButton extends React.Component{
    // 这个语法确保this绑定在handleClick中
    // 警告：这是实验性的语法
    handleClick = () =>{
        console.log("this is:", this);
    }
    
    render(){
        return(
        	<button onClick={this.handleClick}>
        	Click me
        	</button>
        )
        
    }
}
```

## 将参数传递给事件处理程序

```react
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this,id)}>Delete Row</button>
```

```react
// 如果通过bind来获取事件对象的话，需要将这个事件对象参数写到函数参数的最后的位置
changeName(myName,e){
    this.setState({name: myName})
}
<button onClick={this.changeName.bind(this,'xxx')}>改变name</button>
```



```react
class App extends Component {
    constructor(props) {
        super(props)
        this.state = {
            name:'rove'
        }
        // 可将以下方法写在button里
        //this.changeName = this.changeName.bind(this)
    }

}
changeName = () =>{
    this.setState({name:'Rose'})
}
/*changeName = (myName) =>{
    this.setState({name:myName})
}
*/
render(){
    return(
    <div>
     <h1>{this.state.name}</h1>
     {/*在React中监听事件都是使用驼峰命名法，比如onClick，onKeyUp...*/}
     {/*这里如果需要传递参数，可以通过包裹一层箭头函数的形式去传递参数*/}
     {/*如果你要传递事件对象，就需要给箭头函数加一个参数*/}
     <button onclick={()=>this.changeName('dds')}>改变name</button>
     <button onclick={this.changeName}>改变name</button>
    </div>
    )
}
export default App;
```

## 处理state的异步数据

```react
// 因为state是异步数据，所以想要获取的数据不一致
this.setState({
    name:myName
},()=>{ // 回调函数，这个回调函数里面去执行相应的操作
    console.log(this.state.name); // 这样state的数据即时更新数据
})
```

## 组件通讯

### 父组件向子组件通讯

通讯是单向的，数据必须是由一方传到另一方。在React中，父组件可以向子组件通过传props的方式，向子组件进行通讯。

```react
class Parent extends Component{
  state = {
    msg: 'start'
  };

  render() {
    return <Child parms={this.state.msg} />;
  }
}

class Child extends Component{
  render() {
    return <p>{this.props.parms}</p>
  }
}
```

### 子组件向父组件通讯

而子组件向父组件通讯，同意也需要父组件向子组件传递props进行通讯，只是父组件传递的，是作用域为父组件自身的函数，子组件调用该函数，将子组件想要传递的信息，作为参数，传递到父组件的作用域中。

```react
class Parent extends Component{
 
    constructor(props) {
        super(props);
        state = {
            msg: 'start'
        };
    }
    
    
    transMsg(types){
        var newOrders = [];
        for(let type of types){
            if(type)
            alert(type);
        }
        
      }

  render() {
    return <Child parms={this.state.msg} />;
  }
}



class Child extends Component{
    
     constructor(props) {
        super(props);
        // call parent component
        console.log("parms :",this.props.parms);
       this.props.transMsg("hi ~~");
    }

  render() {
    return <p>{this.props.parms}</p>
  }
}

{/* ------------------老师代码----------------- */}
class Parent extends Component {
  constructor(props) {
    super(props)
    this.state = {
      sonWords: '????'
    }
  }
  // 定义接收函数，这个函数里面的参数，可以用来接收上传过来的值
  getMsg = (val) => {
    this.setState({
      sonWords: val
    })
  }
  render() {
    return (
      <div>
        <div>我儿子给我说：{this.state.sonWords}</div>
        {/* 给子组件的getChildMsg属性绑定一个函数，用于接收子组件传递过来的值 */}
        <Childone getChildMsg={this.getMsg}/>
      </div>
    )
  }
}

class Childone extends Component {
  constructor(props) {
    super(props)
    this.state = {
      msg: '我在学习'
    }
  }
  render() {
    // 想要实现子组件传值给父组件，需要给子组件绑定一个props，这个props是一个函数，通过props这个里面的函数去调用父组件里面的方法，实现通信
    return <button onClick={() => this.props.getChildMsg(this.state.msg)}>点击告诉爸爸我在传智博客学习</button>
  }
}

export default Parent;

```

## 兄弟通讯

兄弟通讯主要是子组件向父组件通讯，然后再由父组件传到另一个子组件，从而实现兄弟通讯

React中的通讯：基于发布订阅模式，React组件间通讯，不使用状态提升，不使用redux,不限制层级，直接通讯。

## 受控表单和非受控表达

受控表单：设定了value值的input表单就是一个受控表单，此时的表单是不受你控制的，受react控制

不受控表单：value没有值的input是一个不受控组件。用户的任何输入都会反映到输入框中。默认值设置：

```
<input type="checkbox"> 和 <input type="radio"> 支持defaultChecked，而<select>和<textarea>支持defaultValue (它仅会被渲染一次，在后续的渲染时并不起作用)。要获取非受控表单的值，需要借助于ref
```



| 特征                       | 不受控制表单(不推荐使用) | 受控表单 |
| -------------------------- | ------------------------ | -------- |
| 一次性检索（例如表单提交） | yes                      | yes      |
| 及时验证                   | no                       | yes      |
| 有条件的禁用提交按钮       | no                       | yes      |
| 执行输入格式               | no                       | yes      |
| 一个数据的几个输入         | no                       | yes      |
| 动态输入                   | no                       | yes      |



## 使用refs的场景

1、处理focus、文本选择或者媒体播放

2、触发强制动画

3、集成第三方DOM库

注意：尽量少用refs

## DOM元素上使用refs

通过回调函数来实现对dom的引用

```js
定义： ref={(input) => { this.textInput = input }}
使用： this.textInput.focus()

componentDidMount(){
    this.inputRef.focus()
}
...
<input type="text" ref={(el) => this.inputRef = el }>
```



## TODO添加和删除&列表展示功能

```react
import React, { Component } from 'react'
import './App.css'

class App extends Component {
  constructor(props){
    super(props)
    this.state = {
      todoList: [
        {id:22,text:'react'}
      ]
    
  }
}
handleDel = (id) =>{
  console.log(id, '父组件中')
  // 直接通过数组的findIndex方法找数组的索引，我们这里的条件是，只要数组项中的id和传入的id和传入的id相等，我就把那一项的索引取出来，保存在idx中
  let idx = this.state.todoList.findIndex(item => item.id === id)
  // 直接对数组进行删除操作
  let tempArr = this.state.todoList
  tempArr.splice(idx,1)
  this.setState({
    todoList: tempArr
  })
}
getInput = (val)=>{
  console.log(val);
  let id = this.state.todoList.length === 0?0:this.state.todoList[this.state.todoList.length - 1].id + 1
  this.setState({
    todoList:this.state.todoList.concat({id:id,text:val})
  })
}
render(){
  return (
    <div>
    {/* 这个input也要封装成组件形式 */}
    <Input onSubmit={this.getInput}></Input>
    {
      this.state.todoList.map((item)=>{
        return < Todo {...item} key={item.id} onDel={this.handleDel} />
      })
    }
    </div>
    )
  }
}

// 组件可分离
class Input extends Component {
  constructor(props){
    super(props)
    this.state = {
      inputVal: ''
    }
  }
  getInputVal=(e)=>{
    this.setState({
      inputVal:e.target.value
    })
  }
  emitVal = (e) =>{
    // 如果按的是回车键，那么就开始讲数据传给父组件，再将input置空
    if(e.keyCode === 13){
      this.props.onSubmit(this.state)
      this.setState({
        inputVal: ''
      })
    }
  }
  render(){
    return (
      <div>
       <input type="text" value={this.state.inputVal} onChange={this.getInputVal} onKeyUp={this.emitVal} ></input>
      </div>
    ) 
  }
}

// 组件可分离
class Todo extends Component {
  delTodo = (id) => {
    console.log(id)
    this.props.onDel(id)
  }
  
  render(){
    return (
      <div>
       <div>
        {this.props.text}
        <span style={{paddingLeft: '44px',color:'red'}} onClick={(id) => this.delTodo(this.props.id)}>X</span>
       </div>
      </div>
    )
  }
}
```

如果是要将组件分离出来，在分离的代码段上加上这两段代码

```react
export default class Input extends Component
import React, { Component } from 'react';
```

## 样式

### 内联样式

局限： hover等伪类不能够使用

```react
const styleComponent = {
    hander: {
        backgroundColor: '#333',
        color: '#fff',
        "paddingTop": '15px',
        paddingBottom: '15px'
    }
}

// jsx中这样使用
<header style={styleComponent.header}></header>
```

### 从css文件引入

定义一个样式文件，直接引入（通过link标签），然后给相应的元素加上className。它是全局的，会有污染。

也可以直接通过import引入，然后给相应的元素加上`className`

## 内联样式表达式

```react
const styleComponent = {
    header :{
        backgroundColor: '#333',
        color: '#fff',
        "paddingTop": '15px',
        paddingBottom: (this.state.isMini) ? '10px': '15px'
    }
}

{/* 注意：这个定义样式的对象，需要放在render函数中，因为它里面要访问state，如果定义在类的外面的话，就无法获取state */}
```

## css 模块化

```shell
npm install style-loader css-loader -D
```

```react
{
    test: /\.css$/,
    use: [
        'style-loader',
        {
            loader: 'css-loader',
            options: {
                modules: true,
                localIdentName: '[path][name]__[local]--[hash:base64:5]'
            }
        }
    ]
}
```

create-react-app 不支持，

[需要直接手动配置]: https://segmentfault.com/a/1190000011225917

（react的脚手架）

使用类似下面这样

```react
import cssHeader from (./style.css)
<header calssName={cssHeader.header}></header>
```

##css模块化优点

1、所有样式都是local的，解决了命名冲突和全局污染问题

2、class名生成规则配置灵活，可以以此压缩class名

3、只需引用组件的js就能搞定js和css



## 路由

### React-router

路由的基本使用（BrowserRouter，HashRouter，Router&Link）

```shell
yarn add react-router-dom
npm i react-router-dom
```

路由组件无法接受两个以上子元素

只想匹配某个路由，加`exact`参数，表示要求路径与location.pathname必须完全匹配

```
使用<Switch>组件来包裹一组<Route>。
<Switch>会遍历自身的子元素(即路由)并对第一个匹配当前路径的元素进行渲染，后面的不会再渲染
```

> HashRouter：http://localhost:8080/#/abc/def
> BrowserRouter：http://localhost:8080/abc/def

如果有服务器端的动态支持，建议使用`BrowserRouter`，否则建议使用`HashRouter`。

原因在于，如果是单纯的静态文件，加入路径从/切换到/a后，此时刷新页面，页面将无法正常访问。

二者的替换方法很简单，我们在引入react-router-dom时，如以下：

```react
import { BrowserRouter as Router } from 'react-router-dom'
```

## 路由参数

参数获取： `this.props.match.params.xxx`

![](https://qq292383147.github.io/pictureLibrary/picture/React/React路由初体验1.jpg)

![](https://qq292383147.github.io/pictureLibrary/picture/React/React路由初体验2.jpg)

## axios也可以在React中发送请求

```shell
npm i axios
```



## fetch

[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 提供了一个 JavaScript接口，用于访问和操纵HTTP管道的部分，例如请求和响应。它还提供了一个全局 [`fetch()`](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalFetch/fetch)方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。

## UI框架

##Ant Design（国内）

## 安装

```shell
$ npm install antd --save
$ yarn add antd
```

###在 create-react-app中使用

```bash
$ npm install -g create-react-app
$ yarn create react-app antd-demo

$ npm install --save react-router-dom
```

工具会自动初始化一个脚手架并安装 React 项目的各种必要依赖，如果在过程中出现网络问题，请尝试配置代理或使用其他 npm registry。

然后我们进入项目并启动。

```bash
$ cd antd-demo
$ yarn start
```

## 使用crate-react-app或者antd创建一个React项目

### 安装 create-react-app

先装脚手架

```bash
npm install -g create-react-app
```

然后运行

```bash
create-react-app 你的项目名
```

```bash
npm run start
```

## 安装 antd

先装脚手架

```bash
npm install antd-init -g
```

然后cd到你要建项目到目录

```bash
antd-init
```

然后跑项目

```bash
npm start
```

访问地址：http://localhost:8000

antd脚手架的依赖也就是多了一个自己的套餐antd

```json
 "dependencies": {
    "antd": "^3.0.0",
    "moment": "^2.19.3",
    "react": "^16.2.0",
    "react-dom": "^16.2.0"
  }
```

## 升级版本

基于dva的脚手架

首先是安装脚手架

```bash
npm install dva-cli -g
```

然后创建项目

```bash
dva new dvatest
```

运行项目

```bash
npm start
```



### 按需加载

我们现在已经把组件成功运行起来了，但是在实际开发过程中还有很多问题，例如上面的例子实际上加载了全部的 antd 组件的样式（对前端性能是个隐患）。

此时我们需要对 create-react-app 的默认配置进行自定义，这里我们使用 [react-app-rewired](https://github.com/timarney/react-app-rewired) （一个对 create-react-app 进行自定义配置的社区解决方案）。

引入 react-app-rewired 并修改 package.json 里的启动配置。由于新的 [react-app-rewired@2.x](https://github.com/timarney/react-app-rewired#alternatives) 版本的关系，你还需要安装 [customize-cra](https://github.com/arackaf/customize-cra)。

```bash
$ yarn add react-app-rewired customize-cra
```

```diff
/* package.json */
"scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test",
+   "test": "react-app-rewired test",
}
```

然后在项目根目录创建一个 `config-overrides.js` 用于修改默认配置。

```react
module.exports = function override(config, env) {
  // do stuff with the webpack config...
  return config;
};
```

### 使用 babel-plugin-import

[babel-plugin-import](https://github.com/ant-design/babel-plugin-import) 是一个用于按需加载组件代码和样式的 babel 插件（[原理](https://ant.design/docs/react/getting-started-cn#%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD)），现在我们尝试安装它并修改 `config-overrides.js` 文件。

```diff
$ yarn add babel-plugin-import
+ const { override, fixBabelImports } = require('customize-cra');

- module.exports = function override(config, env) {
-   // do stuff with the webpack config...
-   return config;
- };
+ module.exports = override(
+   fixBabelImports('import', {
+     libraryName: 'antd',
+     libraryDirectory: 'es',
+     style: 'css',
+   }),
+ );
```

然后移除前面在 `src/App.css` 里全量添加的 `@import '~antd/dist/antd.css';` 样式代码，并且按下面的格式引入模块。

```diff
  // src/App.js
  import React, { Component } from 'react';
- import Button from 'antd/lib/button';
+ import { Button } from 'antd';
  import './App.css';

  class App extends Component {
    render() {
      return (
        <div className="App">
          <Button type="primary">Button</Button>
        </div>
      );
    }
  }

  export default App;
```

最后重启 `yarn start` 访问页面，antd 组件的 js 和 css 代码都会按需加载

如图操作：

![](https://qq292383147.github.io/pictureLibrary/picture/React/按需加载UI框架-antd.jpg)

## Material-UI（国外）

## 安装

```shell
$ npm install --save material-ui@next
$ npm install --save material-ui-icons
```

## ES6跨域数据访问fetch-jsonp

参考地址：https://blog.csdn.net/liu942626/article/details/79317837

安装 ：npm install fetch-jsonp

引用 ：import fetchJsonp from 'fetch-jsonp'

Native App（原生App）

原生语言程式是为了特定的操作系统而编码，用的也是特定操作系统的开发套件（Platform SDK）

##所用技术

IOS：Ojbect-C,Swift

Android：java

###优点

1、执行速度快，效能佳。适合需要极快速反应的程式、复杂的动画、游戏...等等

2、对硬体装置的支援度较好，可以应用几乎所有硬体上的功能。例如：相机功能、GPS地理定位等等

3、可以在官方线上商店上架、设定下载App的人是否要付钱，用以赚取费用

4、可以离线使用

##Web App（网页App）

### 所用技术

纯HTML，CSS,JavaScript

### 优点

具有跨平台特性

开发过程中， WebApp只要使用装置的浏览器需输入网址即可执行测试，若有任何问题，程式修改后，可以快速的进行测试，甚至有时只需要简单的重新整理网页即可。

WebApp不需要支付官方开发者年费，也不需要至官方应用程式商店上架，审核或让官方抽成

WebApp有任何功能更新，只需要在后端网站主机修改即可。使用者不需要重新下载安装，就可以随时使用最新的功能

Hybrid App（混合App）

混合语言程式的部分代码会以web技术编写，如HTML5,CSS和JavaScript，这些程式都是被包裹在原生容器（Native Container）和透过手机上的浏览器引导来呈现HTML和执行JavaScript，最后可在包装后像原生APP一样上架至应用程式商店

###优点

1、具有跨平台特性

2、有些框架工具，可让混合式App也能像原生App般，控制硬体装置。例如：相机功能，GPS地理定位，测速计，磁力计，陀螺仪...等等

3、可以在官方线上App商店上架，设定下载App的人是否要付钱，用以赚取费用。

## 移动App的主流开发技术（前端角度）

### Hybrid App

1、Ionic+Angular+Cordova+ionic css

2、Framework7

3、Titanium Appcelerator

4、Onsen UI

5、Xamarin （based on C#）

打包DClud，APICloud，PhoneGap（Cordova）

## Native App

1、React Native

2、Weex

## 快速打包一个Hybrid App

```shell
npm install ionic cordova -g

ionic start myApp tabs

ionic cordova platform add android

ionic serve

ionic cordova build android (可能需要单独配置Gradle) ---打包
```

可能还会报错，按照报错说明去Android SDK Manager 安装响应的包，检查是否连接手机

![安卓报错信息处理](https://qq292383147.github.io/pictureLibrary/picture/React/安卓报错信息处理.jpg)

## py环境配置

![安装py环境](https://qq292383147.github.io/pictureLibrary/picture/React/安装py环境.jpg)

## Android环境配置

![Android环境配置](https://qq292383147.github.io/pictureLibrary/picture/React/Android环境配置.jpg)

[React Native搭建开发环境](https://reactnative.cn/docs/getting-started/)

##React Native快速上手

![1](https://qq292383147.github.io/pictureLibrary/picture/React/React Native项目配置.jpg)

![React Native驱动安装成功](https://qq292383147.github.io/pictureLibrary/picture/React/React Native驱动安装成功.jpg)

## weex快速上手

![weex](https://qq292383147.github.io/pictureLibrary/picture/React/weex.jpg)

注意：weex有很多坑，使用时请注意！！

## React Native(Vysor)

注意：在react-native中不能使用html的标签，比如div/p，只能使用react-native中帮我们封装的组件

网络图片需要加上宽高

还有使用本地图片：require

使用网络图片： url

ScrollView的父容器需要有一个确定的高度

ListView是优化性能用的

通过StyleSheet.crate创建的样式，凡是设置宽度大小等，不能加px单位，只能是数字

在react-native中默认flex布局，并且flex-direction默认为column

## 配置路由

react-native-router-flux

```shell
npm i react-native-router-flux -S
```

```react
import {Scene, Router} from 'react-native-router-flux'

class App extends React.Component {
    render() {
     // Router能够让我们的整个应用程序拥有路由
     return  (
        <Router>
        <Scene key="root">
          {/* Scene是一个场景，专门用来渲染组件的，每个场景都必须有一个key，这个key是唯一标识场景用的。
            将来我们这些key都会保存在Actions中，然后我们可以通过Actions.key()跳转到相应的key对应的场景去
          */}
         <Scene key="login" component={Login} title="{Login}" />
         <Scene key="register" component={Login} title="{register}" />
         <Scene key="home" component={Login} title="{home}" />
         </Scene>
        </Router>
        )
    }
}
```



## react-native-swiper组件（轮播图）

gitHub:https://github.com/leecade/react-native-swiper

```bash
$ npm i react-native-swiper --save
```

- 删除：npm rm react-native-swiper --save

### 引入外部组件

```react
import Swiper from 'react-native-swiper';
```

## 计算屏幕底部距离

onEndReachedThreshold() : 调用onEndReached之前的临界值，单位是像素

如果距离不足则调用onEndReached方法：当所有的数据都已经渲染过，并且列表被滚动到距离最底部不足onEndReachedThreshold个像素的距离时调用。原生的滚动事件会被作为参数传递。

注：当第一次渲染时，如果数据不足一屏（比如初始值是空的），这个事件也会被触发...

## TouchableHighlight

当你想在View标签中使用跳转则可以使用TouchableHighlight

本组件用于封装视图，使其可以正确响应触摸操作。当按下的时候，封装的视图的不透明度会降低，同时会有一个底层的颜色透过而被用户看到，使得视图变暗或变亮。在底层实现上，实际会创建一个新的视图到视图层级中，如果使用的方法不正确，有时候会导致一些不希望出现的视觉效果。譬如没有给视图的backgroundColor显式声明一个不透明的颜色。

```react
import { TouchableHighlight } from 'react-native';

<TouchableHighlight onPress={() => this.jumpToDetail(this.props.id,this.props.title)} activeOpacity={0.3} underlayColor='#666'>
```

## FlatList

高性能的简单列表组件，支持下面这些常用的功能：

> 完全跨平台。
> 支持水平布局模式。
> 行组件显示或隐藏时可配置回调事件。
> 支持单独的头部组件。
> 支持单独的尾部组件。
> 支持自定义行间分隔线。
> 支持下拉刷新。
> 支持上拉加载。
> 支持跳转到指定行（ScrollToIndex）。

如果需要分组/类/区（section），请使用[`SectionList`](https://reactnative.cn/docs/sectionlist).



## React Native安卓项目打包APK

### 1, 产生签名的key

该过程会用到`keytool`，开发过安卓的都应该接触过该东西。详细请见[密钥和证书管理工具](https://link.jianshu.com/?t=http://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html)。
在项目的主目录中执行：

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
[注：在产生的时候需要提供密钥和存储密码，后续会用到]

mv my-release-key.keystore android/app/
```

### 2, 修改`android/gradle.properties`文件，增加如下

```properties
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=xx
MYAPP_RELEASE_KEY_PASSWORD=xx
[注意替换xx为你自己设置的密钥和存储密码]
```

### 3, 修改`android/app/build.gradle`文件中的签名配置：

```gradle
...
android { 
  ... 
  defaultConfig { 
    ... 
  } 
  signingConfigs { 
    release { 
        storeFile file(MYAPP_RELEASE_STORE_FILE) 
        storePassword MYAPP_RELEASE_STORE_PASSWORD 
        keyAlias MYAPP_RELEASE_KEY_ALIAS 
        keyPassword MYAPP_RELEASE_KEY_PASSWORD 
    } 
  } 
  buildTypes { 
    release { 
      ... 
      signingConfig signingConfigs.release 
    } 
  }
}
```

### 4, 然后进入android目录执行如下：

```bash
./gradlew assembleRelease
如果./不行则去掉
```

结束后会在`android/app/build/outputs/apk/app-release.apk`。

每次执行前，注意将该apk删除。



## Redux基本概念

Redux是Javascript （不是react，其他的想Angular也可以使用，甚至单纯的JavaScript也可以使用）状态容器，提供可预测化的状态管理

应用中所有的`state`都以一个对象树的形式存在一个单一的`store`中。唯一改变`state`的办法是触发`action`，一个描述发生什么的对象。为了描述`action`如何`action`如何改变`state`树，你需要编写`reducers`。

![Redux原理](https://qq292383147.github.io/pictureLibrary/picture/React/Redux原理.jpg)

## Redux中的三大原则

### 单一数据源

整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。

这让同构应用开发变得非常容易。来自服务端的 state 可以在无需编写更多代码的情况下被序列化并注入到客户端中。由于是单一的 state  tree ，调试也变得非常容易。在开发中，你可以把应用的 state 保存在本地，从而加快开发速度。此外，受益于单一的 state tree  ，以前难以实现的如“撤销/重做”这类功能也变得轻而易举。

### State 是只读的

**唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。**

这样确保了视图和网络请求都不能直接修改  state，相反它们只能表达想要修改的意图。因为所有的修改都被集中化处理，且严格按照一个接一个的顺序执行，因此不用担心 race  condition 的出现。 Action 就是普通对象而已，因此它们可以被日志打印、序列化、储存、后期调试或测试时回放出来。

```react
store.dispatch({
  type: 'COMPLETE_TODO',
  index: 1
})

store.dispatch({
  type: 'SET_VISIBILITY_FILTER',
  filter: 'SHOW_COMPLETED'
})
```

### 使用纯函数来执行修改

**为了描述 action 如何改变 state tree ，你需要编写 reducers。**

Reducer 只是一些纯函数，它接收先前的 state 和 action，并返回新的 state。刚开始你可以只有一个  reducer，随着应用变大，你可以把它拆成多个小的 reducers，分别独立地操作 state tree 的不同部分，因为 reducer  只是函数，你可以控制它们被调用的顺序，传入附加数据，甚至编写可复用的 reducer 来处理一些通用任务，如分页器。

```react
function visibilityFilter(state = 'SHOW_ALL', action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter
    default:
      return state
  }
}

function todos(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case 'COMPLETE_TODO':
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: true
          })
        }
        return todo
      })
    default:
      return state
  }
}

import { combineReducers, createStore } from 'redux'
let reducer = combineReducers({ visibilityFilter, todos })
let store = createStore(reducer)
```



Redux核心内容

###Store

store是Redux的实例对象，专门用来存放应用的状态，它里面保存有应用的state，action，reducer。

注意：应用程序只能有唯一一个store

store有以下职责：

1、维持应用的state；

2、提供getState() 方法更新state；

3、通过subscribe( listener ) 注册监听器；

4、通过subscribe( listener ) 返回的函数注销监听器。



```react
import { createStore, combineRedurers } from 'redux'
// 创建一个Redux实例，让它去管理应用中的state
// 1. createStore 函数可以传三个参数，分别是reducer (function);
// 初四时的state和enhancer(function),enhancer是一个组合 store creator的高阶函数，返回一个新的强化过的store creator
// 2. combineReducers()函数会将多个不同的reducer合并成一个大的reducer函数，合并后的reducer可以调用各个子reducer，并把他们返回的结果合并成一个state对象。由combineReducers()返回的state对象，会将传入的每个reducer返回的state按其传递给combineReducers()时对应的key进行命名。
const store = createStore(combineReducers({userReducer}));

// store.subscribe()方法可以监听store的更新
store.subscribe(()=>{
    console.log("Store updated!", store.getState());
})
```

### State

State是一个普通对象，用来保存应用的数据。例如：

```react
const initialState = {
    result: 1,
    lastValues: [],
    username: "Max"
}
```

state对象中的数据不能随意修改，要想更改state中的数据，需要用到发起一个action，这个action是一个对象，，描述了你要干什么事情

### Action

action

​    Action就是一个普通JavaScript对象，用来描述发生了什么事情。我们约定，action内必须使用一个字符串类型的type字段来表示将要执行的动作，type会被定义成字符串常量。

```react
{
    type: "SET_AGE"，
    payload: 30
}

// 提交一个action
store.dispatch({
    type: "SET_AGE",
    payload:  30
})
```

但它并没有去修改state，为了去做action描述的事情，我们需要用reducer将action和state联系起来。

### action创建函数

action创建函数式用来创建action的函数，就是专门用来生成action对象的函数，例如：

```react
function addTode(text){
    return {
    	type: ADD_TODO,
    	payload: text
    }
}
```

### Reducer

reducer是一些纯函数，它接收两个参数：state和action，返回值是一个新的state。

注意：

1、不要修改state，而是返回一个新的对象

2、在default情况下返回旧的state



```react
const userReducer = ( state = {
    name: "Max",
    age: 27
}, action) => {
    switch(action.type) {
        case "SET_NAME":
        	state = {
                ...state,
                name: action.payload
        	};
        break;
        case "SET_AGE":
        	state = {
                ...state,
                age: action.payload
        	};
        break;
    }
    // 注意：这个reducer是一个传函数，最后要返回一个新的state
    return state;
}
```

## React 和 Redux 连接

```bash
npm i react-redux -S
```

1、如何将react和redux进行连接，也就是如何让react应用程序拥有redux中的state

```react
import { Provider } from 'react-redux'
render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('app')
)
```

2、其他组件如何调用redux中的state或者触发reducer函数呢？

```react
import { connect } from 'react-redux';
const mapStateToProps = (state) => {
	return {
        // state.userReducer这个userReducer必须和上面const store = createStore(combineReducers({userReducer}));中的userReducer名字对应
        user: state.userReducer
	}
}

const mapDispatchToProps = (dispatch) => {
    return {
        setName: (name) => {
        	dispatch({
                type: "SET_NAME",
                payload: name
        	})
		}
    }
}

export default connect(mapStateToProps, mapDispatchToProps)(App);

// 接下来，可以通过this.props.user.name获取state中的name值
// 通过this.props.setName('xxx')触发一个reducer
```





