---
title: TS总结笔记
date: 2021-08-18 17:22:00
tags: TypeScript
categories: TypeScript
---



## 如何创建ts文件并使用



### 1 使用命令行创建ts 环境

```bash
$ npm i typescript -g

tsc -V  检测版本
```

新建 learn.ts 文件，index.html 页面

命令行运行 tsc ./learn.ts 在同层目录下生成 learn.js

html 页面引用 js 文件即可, 不会自动更新



### 2 让 vscode 创建 ts 文件并编译

运行 `tsc -init` 创建 `tsconfig.json` 文件

设置 `outDir` 文件目录为 `./js/`

使用 vscode 打开终端运行任务， `tsc` 监视-即可在同层目录下生成`js` 文件



### 语法：

#### 1 变量

（1）js： let 变量名 = 值

（2）ts：let 变量名: 变量类型 = 值

#### 2 常见类型

（1）js原有类型：

string number boolean Array Null undefined Symbol Object

（2）ts新增类型：

tuple（元祖）：元祖是一个包含固定数量的元素和相关类型的数组

enum（枚举）

any（任意类型）：一般在取 dom 的时候使用

never：底部类型，可以付给所有其他类型

void：表示无含义，一般在没有返回值的函数中使用



#### 3 修饰符 Modifiers

public：修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 public 的；

private：修饰的属性或方法是私有的，不能在声明它的类的外部访问；

protected：修饰的属性或方法是受保护的，它和 private 类似，区别是它在子类中也是允许被访问的



```ts
public readonly msg!: number | string;
private readonly msg!: number | string;
protected readonly msg!: number | string;
```



#### 4 readonly 只读

只读属性关键字，只允许出现在属性声明或索引签名或构造函数中。

```ts
readonly msg!: number | string;
public readonly msg!: number | string;
```



#### 5 类型推断

一般在同一行，没有给类型的，会进行类型推断；

```ts
let a = 18; ===>  let a:number = 18
```

联合类型：不确定时，可以给多个类型：let a :string | null = fun()



#### 5.1 定义类型(范围)

```ts
type NumStr = number | string;

let a: NumStr = 10;
a = "hello";

let b: NumStr = "hello";

let c: "on" | "off" = "on";

// 如果c赋值为other则会报错
```

## 数组类型

```ts
let tup: [number ,string , boolean] = [1, 'fh', true]
```





#### 6 函数

**返回值类型**

> function 函数名():返回值类型()
>
> let 变量名: 变量类型 = 函数名()

**形参类型**

> function 函数名(参数1：类型，参数2：类型)： 返回值类型{}
>
> let 变量名： 变量类型= 函数名（实参1，实参2）

**带默认值的参数传递**

> function 函数名（参数1：类型=默认值1，参数2：类型=默认值2）:f返回值类型{}

```ts
function add (x:number=2,y:number = 3):number {
	console.log(x+y)
    retrun x+y
}
add()  // 5
add(6)  //9
add(undefined,5)   // 7

// * 不传参 add() -->  add(2,3)
// * 传一个参数 add(6) ---> add(6,3)
// * 两个参数都传 add(6,5) ---> add(6,5)
// * 传后一个参数 add(undefined,5) --> add(2,5)

```

**形参不确定的情况**

第一个参数确定，后面的参数用展开运算符，并且是数组类型指代

```ts
function edit(x?:number,...y?:number[]):void {
    let num:number = x? x:1
    for(const ele of y){
        num+= ele
    }
    console.log(num)
}
edit()   // 1
edit(3)  // 3
edit(1,2,3,4,5)  // 15
```

#### 7 类

**构造函数 + new 方法创造类**

**class 函数创造类**

> 根据 ES6 的 class 构造函数中的例子用 ts 方法改写类

```ts
class Demo2 {
    x:string|number;
    y:string|number;
    constructor(x:string|number,y:string|number){
        this.x = x;
        this.y = y;
    }
    test():string{
        return `${this.x}是x的值，${this.y}是Y的值`
    }
    static change():string{
        return '测试是否能被继承'
    }
}

let str2 = new Demo2(5,6).test()
let str3 = Demo2.change()
console.log(str2)  // 5是 X的值，6是 Y的值
console.log(str3)  // 测试是否能被继承

```

### 案例----ts中类的使用

**需求：1、加载评论列表，2、文章评论存入 localstorage，3、页面删除评论**



![image-20210819171206754](C:\Users\111\AppData\Roaming\Typora\typora-user-images\image-20210819171206754.png)

## 接口

#### 接口的使用

直接在对象名称后面写类型注解的坏处：1、代码结构不简洁 2、无法复用类型注解



接口： 为对象的类型注解命名，并为你的代码建立契约来约束对象的结构

语法：

```ts
interface IUser {
    name: string
    age: number
}
```

使用：

```TS
let pl : IUser = {
    name: 'jack',
    age: 18
}
```

`interface`  表示接口，接口名称约定已 I 开头

推荐：使用接口来作为对象的类型注解。



## TS 的类型推论

在TS 中， 某些没有明确指出类型的地方，类型推论会帮助提供类型。

换句话说，由于类型推论的存在，这些地方，类型注解可以省略不写！

发生类型推论的2种常见场景：1、声明变量并初始化时 2、决定函数返回值时。

```ts
let age: number = 10 // =>  let age = 18
function sum (num1:number,num2:number): number {
    return num1 + num2
}
function sum(num1: number,num2:number){
    return num1 + num2
}
```

注意： 这两种情况下，类型注解可以省略不写！

推荐：能省略类型注解的地方，就省略（偷懒、充分利用TS类型推论的能力，提升开发效率）

学习的时候，培养大家去建立类型思维；出师了，可以去繁就简。



## 类型断言

问题： 调用 `querySelector()` 通过id选择器获取DOM 元素时，拿到的元素类型都是`Element`

因为无法根据id 来确定元素的类型，所以，该方法就返回了一个**宽泛** 的类型：元素（Element）类型。

不管是 `h1` 还是 `img` 都是元素

导致新问题： 无法访问 `img` 元素的 `src` 属性了。

因为： `element` 类型只包含所有元素共有的属性和方法（比如： id属性）

解决方式： 使用**类型断言**，来手动指定更加具体的类型（比如，此处应该比 `element`类型更加具体）

语法： 

```ts
值 as 更具体的类型
```

比如：

```ts
let img = document.querySelector('#image') as HTMLImageElement
```

解释：我们确定 `id="image"` 的元素是图片元素，所以，我们将类型指定为 `THMLImageElement`

技巧：通过 `console.dir()` 打印DOM 元素，在属性的最后面，即可看到该元素的类型。



## 设置生成JS版本

1、新建tsconfig.json 文件,并编写以下代码

```json
{
	"compilerOptions":{
		"target": "ES2017"
    }
}
```

运行

```bash
tsc
```

提示： 如果设置了 `tsconfig.json` 文件之后，直接运行 `tsc` 即可

