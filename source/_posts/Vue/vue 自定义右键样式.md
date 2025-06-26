---
title: vue 自定义右键样式
date: 2019-11-13 22:42:04
tags: vue
categories: vue
---

##### 主要是靠`双击`和`右键`来操作，可操作多个模态框，跟操作`windows`类似，接下来在里面拆出一个功能块来写一篇文章，就是`自定义系统默认的右键`。

##### 自定义右键操作有五个步骤：

1. `阻止`默认右键。
2. 获取当前右键点击时的`x`/`y`坐标，及`id`。
3. 自定义右键菜单样式及内容，定位在指定的位置后显示。
4. 返回对应点击目录的事件如:`查看`、`删除`、`编辑`。
5. 在任何地方点击左键时`隐藏右键菜单`。

##### 关键方法：

```
@contextmenu.prevent
```

> 这个是vue内置的，点击右键（阻止默认右键的默认行为）的一个回调方法，他返回了一大串东西这里我用到的是这两个(用于定位显示菜单的x,y位置)

![114](https://qq292383147.github.io/pictureLibrary/picture/vue/114.jpg)

> `x_index`，`y_index` 是储存在`data`中的，用于定位模态框位置。
>  `ctrlId` 用于给接口处理的依据
>  `showMenu` 用于判断是否显示右键菜单

```vue
<!--template-->
<ul>
    <li class="role_list" 
	v-for="(item,index) in role" 
	:key="index"
	@contextmenu.prevent="(e)=>{
		x_index = e.layerX;
	        y_index = e.layerY;
		ctrlId = item.id;
		showMenu = true;
	}">
	    <img :src="item.head_portrait" alt="">
	    <p>{{item.name}}</p>
	</li>
</ul>
```

> 需要的参数(x,y,id)都具备了，因为右键操作很多地方都用到了，所以封装成了一个组件

#### right_menu.vue 组件代码

| 参数名   | 注释     |
| -------- | -------- |
| x        | x坐标    |
| y        | y坐标    |
| showMenu | 显示状态 |

```vue
<template>
	<div v-if="show"
	     class="menu_style" 
	     :style="{top:y+'px',left:x+'px'}">
		<ul>
			<!-- 分别传递事件给父元素调用 -->
			<li @click="()=>{$emit('open')}">打开</li>
			<li @click="()=>{$emit('update')}">编辑</li>
			<li @click="()=>{$emit('del')}">删除</li>
		</ul>
	</div>
</template>
<script>
	export default{
		name:'right_menu',
		props:{
			x:{
				type:[Number],
				default:0
			},
			y:{
				type:[Number],
				default:0
			},
			showMenu:{
				type:[Boolean],
				default:false
			}
		},
		data(){
			return {
				show:false,
			}
		},
		methods:{
			// 点击别处时隐藏目录，并传递一个关闭事件
			closeMenu(e){
				this.show = false;
				this.$emit("close",false)
			},
		},
		mounted(){
			// 监听body上的点击
			document.querySelector("body").addEventListener("click",this.closeMenu)
		},
		beforeDestroy(){
			// 移除监听
			document.querySelector("body").removeEventListener("click",this.closeMenu)
		},
		watch:{
			// 监听，保持显示状态与父元素一致
			showMenu(val){
				this.show = val;
			}
		},
	}
</script>
<style scoped>
	.menu_style{
		position: absolute;
		width: 150px;
		background-color: #fff;
		border-radius: 2px;
		box-shadow: 2px 2px 14px #d0d0d0;
	}
	.menu_style>ul>li{
		text-indent: 25px;
		height: 38px;
		line-height: 38px;
		border-bottom: 1px dashed #f0f0f0;
		cursor: pointer;
	}
	.menu_style>ul>li:hover{
		background: #E0EEFF;
	}
</style>
```

##### 组件使用

```vue
<template>
    <div class="modal_data_box">
        <ul>
            <li class="role_list" 
                v-for="(item,index) in role" 
                :key="index"
                @contextmenu.prevent="(e)=>{
                    x_index = e.layerX;
                    y_index = e.layerY;
                    ctrlId = item.id;
                    showMenu = true;
                }">
                <img :src="item.head_portrait" alt="">
                <p>{{item.name}}</p>
            </li>
        </ul>
	<!--组件-->
	<right-menu :x="x_index"
	            :y="y_index" 
	            :showMenu="showMenu"
	            @close="closeMenu"
	            @open="openDetail"
	            @del="delAttr"
	            @update="updateArr">
	</right-menu>
    </div>
</template>
<script>
    // 导入组件
	import rightMenu from '../module/right_menu.vue';
	export default{
		name:"roleModal",
		components:{rightMenu},
		data(){
			return {
				x_index:0,
				y_index:0,
				ctrlId:'',
				showMenu:false,
				role:[],
			}
		},
		methods:{
		    //关闭回调  
		    closeMenu(state){
		        console.log('关闭')
		        this.showMenu = state;
		    },
		    //打开详情回调 			
		    openDetail(){
		        console.log('编辑')
		    },
		    //删除回调 			
		    delAttr(){
		        console.log('删除')
		    },
		    //编辑回调 			
		    updateArr(){
		        console.log('编辑')
		    },
		}
	}
</script>
```

#### 修复漏洞

[d[o_0\]b](https://juejin.im/user/5cf2512e51882504d340ab01)同学发现了一个漏洞，就是当鼠标在屏幕右边点击时，菜单会被遮挡住，这边做了一些调整。

##### 修复前：

![115](https://qq292383147.github.io/pictureLibrary/picture/vue/115.jpg)

```js
//原来的代码
<ul>
    <li class="role_list" 
	v-for="(item,index) in role" 
	:key="index"
	@contextmenu.prevent="(e)=>{
		x_index = e.layerX;
	        y_index = e.layerY;
		ctrlId = item.id;
		showMenu = true;
	}">
	    <img :src="item.head_portrait" alt="">
	    <p>{{item.name}}</p>
	</li>
</ul>
```

##### 修复后：

![116](https://qq292383147.github.io/pictureLibrary/picture/vue/116.jpg)

```js
//修改后的代码，（由于要判断，所以单独写了个方法，把e跟item都传过去）
<ul>
	<li class="role_list" 
		v-for="(item,index) in role" 
		:key="index"
		@contextmenu.prevent="(e)=>{
			rightClick(e,item)
		}">
		<img :src="item.head_portrait" alt="">
		<p>{{item.name}}</p>
	</li>
</ul>

//对应的rightClick方法
rightClick(e,item){
	// 屏幕可见宽
	let clientWidth = document.body.clientWidth;
	// 菜单宽
	let menuWidth = 150;
	// 点击右键时会返回对应的clientX，用这个值与(clientWidth+菜单宽度)对比，如果大于的话，就把菜单左偏移一个菜单宽
	let clickClientX = e.clientX + menuWidth
	if(clickClientX > clientWidth){
		console.log("菜单超出视线范围")
		this.x_index = e.layerX - menuWidth;
	}else{
		this.x_index = e.layerX;
	}
	this.y_index = e.layerY;
	this.ctrlId = item.id;
	this.showMenu = true;
},
```

#### 方法更新:

右键的优化方案  `$event`

```js
@contextmenu.prevent="rightClick($event,item)"
```

