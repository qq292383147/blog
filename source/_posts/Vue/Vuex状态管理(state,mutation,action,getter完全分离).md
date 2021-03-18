---
title: Vuex状态管理(state,mutation,action,getter完全分离)
date: 2019-10-31 21:20:11
tags: vue
categories: vue
---



## 一、安装依赖

```js
npm install vuex --save
或者
yarn add vuex --save
```
## 二、基本配置文件事例
在项目中src文件夹下新建store文件夹,并在创建如下文件：

![4](http://zhanglong292383147.gitee.io/picture_images/picture/vue/93.jpg)

index.js 入口文件
state.js 所有状态的管理
mutations.js
mutation-types.js 存储相关mutation字符串常量
action.js 异步操作，修改，mutation的封装
getters映射



### 1）在main.js中引入store

```js
import store from './store'
new Vue({
  el: '#app',
  store,
  render: h => h(App)
})
```

### 2）index文件

```js
import Vue from 'vue'
import Vuex from 'vuex'
import * as actions from './actions'
import * as getters from './getters'
import state from './state'
import mutations from './mutations'
import createLogger from 'vuex/dist/logger'
// createLogger 每次通过mutation修改state通过log控制台打印log，看到日志，方便查看

Vue.use(Vuex)

const debug = process.env.NODE_ENV !== 'production'
// npm run dev是dev环境,线上调试degbug为true
// npm run build 是 production环境,线上调试degbug为false
// 当debug为true开启严格模式
// 当为false，上线时这个模式关闭
// debug会有性能损失，所以不建议线上使用
export default new Vuex.Store({
  actions,
  getters,
  state,
  mutations,
  strict: debug,
  plugins: debug ? [createLogger()] : []
})
```

### 3）state文件

```js
import {playMode} from 'common/js/config'

const state = {
  singer: {},
  playing: false, // 是否正在播放
  fullScreen: false, // 是否全屏
  playlist: [], // 播放的列表
  sequenceList: [], // 顺序列表 随机播放列表 历史列表
  mode: playMode.sequence, // 播放模式
  currentIndex: -1 // 单签歌曲
}
export default state

// config.js
export const playMode = {
  sequence: 0,
  loop: 1,
  random: 2
}

```

### 4）mutation-types

```js
export const SET_SINGER = 'SET_SINGER'

export const SET_PLAYING_STATE = 'SET_PLAYING_STATE'

export const SET_FULL_SCREEN = 'SET_FULL_SCREEN'

```

### 5）mutations

```js
import * as types from './mutation-types'

const mutations = {
  [types.SET_SINGER](state, singer) {
    state.singer = singer
  },
  [types.SET_PLAYING_STATE](state, flag) {
    state.playing = flag
  },
  [types.SET_FULL_SCREEN](state, flag) {
    state.fullScreen = flag
  },
}
export default mutations

```

### 6）getters

```js
export const singer = state => state.singer

export const playing = state => state.playing

export const fullScreen = state => state.fullScreen

```

### 7）actions

```js
import * as types from './mutation-types'

export const selectPlay = function({commit, state}, {list, index}) {
  commit(types.SET_SEQUENCE_LIST, list)
  if (state.mode === playMode.random) {
    let randomList = shuffle(list)
    commit(types.SET_PLAYLIST, randomList)
    index = findIndex(randomList, list[index])
  } else {
    commit(types.SET_PLAYLIST, list)
  }
  commit(types.SET_CURRENT_INDEX, index)
  commit(types.SET_FULL_SCREEN, true)
  commit(types.SET_PLAYING_STATE, true)
}
export const randomPlay = function({commit}, {list}) {
  commit(types.SET_PLAY_MODE, playMode.random)
  commit(types.SET_SEQUENCE_LIST, list)
  let randomList = shuffle(list)
  commit(types.SET_PLAYLIST, randomList)
  commit(types.SET_CURRENT_INDEX, 0)
  commit(types.SET_FULL_SCREEN, true)
  commit(types.SET_PLAYING_STATE, true)
}

```

我们在组件中使用 来获得状态 show , 类似的 , 我们可以使用 $store.getters.not_show 来获得状态 not_show 。

注意 : $store.getters.not_show 的值是不能直接修改的 , 需要对应的 state 发生变化才能修改。



## 三、mapGetters、mapMutations、mapActions的使用事例

### 1）mapGetters

注意：要使用`...mapGetters`、`...mapMutations`、`..mapActions`
需要安装`eslint-plugin-vue`
并且在目录也有`.barbelrc`

```js
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }],
    "stage-2"
  ],
  "plugins": ["transform-vue-jsx", "transform-runtime"]
}

import {mapGetters} from ''vuex
//  一般在computed中使用
computed:{
  ...
  },
  ...mapGetters([// 一般放在computed的最后
      'currentIndex',
      'fullScreen'.
      'playlist'
  ])
}
// 可直接在template中使用
<template>
    <div>
      <div v-html="currentIndex"></div>
    </div>
</template>

```

### 2）mapMutations

```js
import {mapMutations} from ''vuex
//  一般在methods中使用
methods:{
  ...
  back() {
      this.setFullScreen(false)// 使用
  },
  open() {
      this.setFullScreen(true)
  },
  ...mapMutations({// 一般放在methods的最后      
      setFullScreen: 'SET_FULL_SCREEN'
  })
}
// 可直接在template中使用
<template>
    <div>
      <div v-html="currentIndex"></div>
    </div>
</template>
```

### 2）mapActions

在`methods`中使用

```js
methods:{
  ...
  },
  selectItem(item, index) {
      this.selectPlay({
        list: this.songs,
        index: index
      })
 },
random() {
      this.randomPlay({
        list: this.songs
      })
 },
  ...mapActions([
      'selectPlay',
      'randomPlay'
    ])
}
```







