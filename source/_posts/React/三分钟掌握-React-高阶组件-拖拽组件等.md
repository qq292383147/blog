---
title: 三分钟掌握 React 高阶组件(拖拽组件等)
date: 2019-05-24 13:45:02
tags: React & React Native
categories: React & React Native
---

## 什么是高阶组件？

高阶组件（HOC）是 `React` 中用于复用组件逻辑的一种高级技巧。`HOC` 自身不是 `React API` 的一部分，它是一种基于 `React` 的组合特性而形成的设计模式。

## 它做了什么？

他们接收一个组件并返回一个新的组件！

## 什么时候去使用？

当你的组件之间出现重复的模式 / 逻辑的时候。

例子：

>挂载，订阅数据
>为 UI 增加交互（也可以使用容器组件，或者 [`Render Props`](https://react.docschina.org/docs/render-props.html)）
>排序，过滤输入的数据

>第三个说法，我个人可能更加倾向于在传入组件之前做处理，而不是使用高阶组件

## 一个愚蠢的例子

我们有一个 Mouse 组件。

```js
  const Mouse = () => (
      <span className="mouse" role="img">🐭</span>
  )
```

接下来，让我们使用 [GreenSock’s Draggable](https://greensock.com/draggable) 模块，来让组件变的可以拖拽。

```js
  class Mouse extends Component {
      componentDidMount = () => new Draggable(this.ELEMENT)
      render = () => (
          <span className="mouse" ref={e => (this.ELEMENT = e)} role="img">🐭</span>
      )
  }
```

![](https://qq292383147.github.io/pictureLibrary/picture/React/拖拽1.gif)

我们加一只猫 🐱

```js
  const Cat = () => (
      <span className="cat" role="img">🐱</span>
  )
```

这个组件同样需要变得可拖拽✋，接下来，让我们使用高阶组件（HOC）来试一下：

```js
  const withDrag = Wrapped => {
      class WithDrag extends Component {
          componentDidMount = () => new Draggable(this.ELEMENT)
          render = () => {
              return (
                  <span className="draggable_wrapper" ref={e => (this.ELEMENT = e)}>
                      <Wrapped  {...this.props} />
                  </span>
              )
          }
      }
      WithDrag.displayName = `WithDrag(${Wrapped.displayName || Wrapped.name})`
      return WithDrag;
  }
```

我们的高阶组件（HOC）可以通过 `props` 接受一组件，并返回一个新的组件。

许多高阶组件会在传递组件的过程中，注入新的 `props` 。这通常是决定我们是否应该使用高阶组件的因素之一。如果，我们不注入 `props` ，我们可以使用一个容器组件，或者 [Render Props](https://react.docschina.org/docs/render-props.html)。

对于我们的高阶组件（HOC），我们也可以使用 Render Props 来达到相同的效果。你可能会觉得使用 `HOC` 来实现并不合适。但是，这个 “愚蠢的例子” 会让你更加熟悉 `HOC` 。 这比注入数据的示例更加有趣！😉

让我们将这个 `HOC` 应用到 `Cat` 和 `Mouse` 组件上吧 👍

```js
  const Mouse = () => (
      <span className="mouse" role="img">🐭</span>
  )
  const Cat = () => (
      <span className="cat" role="img">🐱</span>
  )
  const DraggableMouse = withDrag(Mouse)
  const DraggableCat = withDrag(Cat)

  class App extends Component {
      render = () => (
          <Fragment>
              <DraggableMouse />
              <DraggableCat />
          </Fragment>
      )
  }
```

![](https://qq292383147.github.io/pictureLibrary/picture/React/拖拽2.gif)

接下来，让我们在高阶组件中增加 `onDrag` 回调函数，并在 `props` 中注入 `x` 和 `y` 的位置属性。

```js
  const withDrag = Wrapped => {
      class WithDrag extends Component {
          state = {
              x: undefined,
              y: undefined,
          }
          componentDidMount = () => new Draggable(this.ELEMENT, { onDrag: this.onDrag })
          onDrag = e => {
              const { x, y } = e.target.getBoundingClientRect();
              this.setState({ x: Math.floor(x), y: Math.floor(y) })
          }
          render = () => (
              <span className="draggable_wrapper" ref={e => (this.ELEMENT = e)}>
                  <Wrapped  {...this.props} x={this.state.x} y={this.state.y} />
              </span>
          )
      }
      WithDrag.displayName = `WithDrag(${Wrapped.displayName || Wrapped.name})`
      return WithDrag;
  }
```

```js
  const Mouse = () => (
      <span className="mouse" role="img">
          🐭
          {x !== undefined && 
              y !== undefined && (
                  <span className="mouse__position"> {`(${x}, ${y})`} </span>
          )}
      </span>
  )
```

现在 `Mouse` 组件会向用户展示他的 `XY` 位置属性 🤓

![](https://qq292383147.github.io/pictureLibrary/picture/React/拖拽3.gif)


我们也可以给 `HOC` 传递 `props`。然后在传递的过程中过滤掉这些无用的属性。举个例子，传递一个 `onDrag` 回调函数。

```js
  const withDrag = Wrapped => {
      class WithDrag extends Component {
          componentDidMount = () => new Draggable(this.ELEMENT, { onDrag: this.props.onDrag })
          render = () => {
              const { onDrag, ...passed } = this.props;
              return (
                  <span className="draggable__wrapper" ref={e => (this.ELEMENT = e)}>
                      <Wrapped  {...passed} />
                  </span>
              )
          }
      }
      WithDrag.displayName = `WithDrag(${Wrapped.displayName || Wrapped.name})`
      return WithDrag;
  }

  class App extends Component {
      render = () => (
          <Fragment>
              <DraggableMouse
                  onDrag={e => console.info(e.target.getBoundingClientRect())}
              />
          </Fragment>
      )
  }
```

通过使用 `HOC` ，我们的组件仍然很简单，复杂的逻辑都交给 `HOC` 来处理了。 我们的组件只关心传递给他们的内容。 我们可以在其他地方重复使用它们而且不会有可以被拖拽的属性。这使得我们的应用更容易维护。

优秀的实践 👍

>当出现重复的模式的时候，使用它们
>为了方便调试，需要更新处理之后组件的 `displayName`
>传递与当前 `HOC` 无关的所有 `props`

糟糕的实践 👎

>过度使用，其他模式可能会更加适合
>改变原始组件
>在 `render` 方法中使用高阶组件


>永远不要在 `React render()`方法中定义 `React` 组件（甚至是无状态组件）。`React` 在每次更新状态的时候，都会废弃旧的 `html DOM` 元素并将其替换为全新的元素。比如在 `render()` 函数中定义一个输入组件，元素被替换之后就会失去焦点，每次只能输入一个字符。

注意 🙏

>`Refs` 不会被传递
>务必复制静态方法
>大部分 `HOC` 都可以和 `render props` 相互替换使用