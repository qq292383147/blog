---
title: Vue中Vuex的详解与使用(简洁易懂的入门小实例)
date: 2020-06-26 15:10:55
tags: vue
categories: vue
---



**Vuex 是一个专为 Vue.js 应用程序开发的`状态管理模式`。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。**

**例如：你有几个数据，几个操作，在多个组件上都需要使用，如果每个组件都去调用都是写，就会很麻烦，代码又臭又长。当然 如果没有大量的操作和数据需要在多个组件内使用的话呢，其实也就可以不用这个 Vuex了。看个人吧！**

**这里我就用自己对 Vuex 的理解来介绍这个东西怎么去使用，我人也不聪明，整好久才整明白，话不多说，下面开始上代码。**

**1、首先为了项目格式便于维护和相对规范一点，我们先在 目录下建立一个 store 文件夹，并且在下面建立一个 store.js 文件：**



![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/1.jpg)

 

## 2、简单明了，先引入 Vue 和 Vuex 并且别忘了 Vue.use(Vuex);

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/2.jpg)

**当然你 Vuex 首先得跟 main.js 扯上点关系嘛。这里的m_index.js === main.js 因为项目原因，暂时换了个名字，不过也无影响，好了我们继续。**

**=》引入 store 文件  =》   并且 Vue 实例上得将 挂载 store ，这下万无一失。可以继续了** 

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/3.jpg)

 **然后我们就可以开始编写我们的vuex业务代码了，那么，我们的数据如何保存？**

 

## 3、现在开始 Vuex 的主宰部分 new Vuex.Store（{}）

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/4.jpg)

 **在这张图上可以清楚的看到 new Vuex.Store 里面有一个 state:{ } 注释也写了，**

**这是你要设置的全局访问的 state 对象，也就是你需要 count 就丢个 count进去，需要 price 就丢个 price进去，**

**这里我丢了个 count 和 ChangeShowCom 两个不同的数据类型 作为一个对比。**

 

## 4、如何在页面中获取 state 里面的 数据呢？

**通过 this.$store.state.count 可以拿到 state里面的 count 也就是0，话不多说，看看吧**



 ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/5.jpg)

 

## 5、getters  =》getters 和 组件的 computed 类似，方便直接生成一些可以直接用的数据。当组装的数据要在多个页面使用时，就可以使用 getters 来做。

　**注释也写了，getters 可以实时监听state值的变化(最新状态)**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/6.jpg)

 **我给 getters 里面获取 count 值的方法命名为 getCount 并且需要传入 state**

**那么如何获取 通过 getters 获取 承载变化的 count 的值呢？**

```
this.$store.getters.getCount  具体效果在 第4 栏里面有些，这里就不作重复了。
```



## 6、那么， 我们如果想改变 count 的值，应该怎么做呢？ 这时候就可以用到  mutations 。

**要修改 store 中的值唯一的方法就是提交 mutation 来修改，我们现在 Hello World.vue 文件中添加两个按钮，一个加1，一个减1；**

**这里我们点击按钮调用 add（执行加的方法）和 del（执行减法的方法），然后在里面直接提交 mutations 中的方法修改值：**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/7.jpg)

 

**修改 store.js 文件，添加 mutations，在 mutations 中定义两个函数，用来对 count 加 1 和减 1，**

**这里定义的两个方法就是上面 commit 提交的两个方法如下：**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/8.jpg)

　　**我们可以将参数传递给 mutations 中的函数进行计算 这里是 num 。**

​      **现在我们看看效果 ：**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/9.jpg)

  **很好，count 数值都发生了改变，我点击了两下，并且 是可以在 Vue Devtools 中的 Vuex 看到过程效果**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/10.jpg)

**payload ：1 就是数值变化1 type 操作的方法是 addCount 也就是 mutations 根方法**

**ok！完美。**

 

**7、到了 Actions 了**  

**Action 类似于 mutation，不同在于：**

- **Action 提交的是 mutation，而不是直接变更状态。**
- **Action 可以包含任意异步操作。**

**我们来看一下：**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/11.jpg)

**然后我们去修改 Hello World.vue 文件：**

**这里我们把 commit 提交 mutations 修改为使用 dispatch 来提交 actions；我们点击页面，效果是一样的。**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/12.jpg)

**现在让我们来看看效果，这里我又点击了6下，很显然，效果是一样的。**

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/13.jpg)

 

注意，当实际写项目的时候  里面未必直接传的是 数字1 可能是对象啊 或者字符串啊。所以这个时候就要注意了，我举个例子：

这里写个 input 输入框 双向绑定一个 something 记得在 data 里面初始化一下，

然后，我们将 something 传入这个方法里面 add(something) 

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/14.jpg)

 

这个时候，看着好像没有什么问题，那么问题这时候就来了，我们先试试点加号会发生什么？

 ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/15.jpg)

   我点击了三下加号，看到没，直接在 0后面拼接了111 变成0111 这显然不是我们想要的效果了，这是为什么呢？

 

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/16.jpg)

我们来打印一下 这个 1 的数据类型

 

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/17.jpg)

 原来如此，这个是字符串类型，难怪不能直接加，那么现在我们该怎么办呢？当然是 字符串转换成数字啦 parseInt()

 ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/18.jpg)

 

  当然是 字符串转换成数字啦  哈哈哈哈哈哈 parseInt(); 方法  然后继续打印结果

  ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/19.jpg)

 ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/20.jpg)

 

  好了，现在就是数字类型了，那么我们继续最后一步，并且看看效果吧

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/21.jpg)

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/22.jpg)

 

 这里我点击了三下，结果成功的变成了 6.

 

**8、来看一下 Vuex 里面的好东西，辅助函数 mapState、mapGetters、mapActions**

```
如果我们不喜欢这种在页面上使用“this.stroe.state.count”和“this.store.dispatch('funName')”这种很长的写法，

那么我们可以使用 mapState、mapGetters、mapActions就不会这么麻烦了；

并且我们配合 ... 拓展符 一起使用。

```



![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/23.jpg)

 

![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/24.jpg)

 ![img](https://qq292383147.github.io/pictureLibrary/picture/vuex/25.jpg)

 

**正常显示，效果是一样的，我们就可以不再使用很长的写法来调用了。**