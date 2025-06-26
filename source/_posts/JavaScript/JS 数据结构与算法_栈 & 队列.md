---
title: JS 数据结构与算法_栈 & 队列
date: 2019-11-24 19:03:55
tags: JavaScript
categories: JavaScript
---

#### 写在前面

原计划是把《你不知道的Javascript》三部全部看完的，偶然间朋友推荐了数据结构与算法的一套入门视频，学之。发现数据结构并没有想象中那么遥不可及，反而发觉挺有意思的。手头上恰好有《学习Javascript数据结构与算法》的书籍，便转而先把数据结构与算法学习。

#### 一、认识数据结构

什么是数据结构？下面是维基百科的解释：

> 数据结构是计算机存储、组织数据的方式。数据结构意味着接口或封装：一个数据结构可被视为两个函数之间的接口，或者是**由数据类型联合组成的存储内容的访问方法封装**

我们每天的编码中都会用到数据结构，因为**数组是最简单的内存数据结构**，下面是常见的数据结构：

- 数组（Array）
- 栈（Stack）
- 队列（Queue）
- 链表（Linked List）
- 树（Tree）
- 图（Graph）
- 堆（Heap）
- 散列表（Hash）

下面来学习学习栈和队列。

#### 二、栈

##### 2.1 栈数据结构

> 栈是一种遵循**后进先出（LIFO）**原则的有序集合。新添加的或待删除的元素都保存在栈的同一端，称作**栈顶**，另一端就叫**栈底**。在栈里，新元素都接近栈顶，旧元素都接近栈底。

![112](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/112.jpg)

类比生活中的物件：一摞书📚或者推放在一起的盘子。

##### 2.2 栈的实现

普通的栈常用的有以下几个方法：

- `push` 添加一个（或几个）新元素到栈顶
- `pop` 溢出栈顶元素，同时返回被移除的元素
- `peek` 返回栈顶元素，不对栈做修改
- `isEmpty` 栈内无元素返回 `true`，否则返回 `false`
- `size` 返回栈内元素个数
- `clear` 清空栈

```js
class Stack {
    constructor() {
        this._items = []; // 储存数据
    }
    // 向栈内压入一个元素
    push(item) {
        this._items.push(item);
    }
    // 把栈顶元素弹出
    pop() {
        return this._items.pop();
    }
    // 返回栈顶元素
    peek() {
        return this._items[this._items.length - 1];
    }
    // 判断栈是否为空
    isEmpty() {
        return !this._items.length;
    }
    // 栈元素个数
    size() {
        return this._items.length;
    }
    // 清空栈
    clear() {
        this._items = [];
    }}
```

现在再回头想想数据结构里面的栈是什么。

突然发现并没有那么神奇，仅仅只是对原有数据进行了一次封装而已。而封装的结果是：**并不去关心其内部的元素是什么，只是去操作栈顶元素**，这样的话，在编码中会更可控一些。

##### 2.3 栈的应用

**（1）十进制转任意进制**

**要求：**给定一个函数，输入目标数值和进制基数，输出对应的进制数（最大为16进制）。

```js
baseConverter(10, 2) ==> 1010baseConverter(30, 16) ==> 1E
```

**分析：**进制转换的本质——将目标值一次一次除以进制基数，得到的取整值为新目标值，记录下余数，直到目标值小于0，最后将余数逆序组合即可。利用栈，记录余数入栈，组合时出栈。

```js
// 进制转换
function baseConverter(delNumber, base) {
    const stack = new Stack();
    let rem = null;  let ret = [];
    // 十六进制中需要依次对应A~F
    const digits = '0123456789ABCDEF';
    
  while (delNumber > 0) {
      rem = Math.floor(delNumber % base);
      stack.push(rem);
      delNumber = Math.floor(delNumber / base);
  }
  while (!stack.isEmpty()) {
      ret.push(digits[stack.pop()]);
  }
  return ret.join('');
}
console.log(baseConverter(100345, 2)); //输出11000011111111001
console.log(baseConverter(100345, 8)); //输出303771
console.log(baseConverter(100345, 16)); //输出187F9
```

**（2）逆波兰表达式计算**

**要求：** 逆波兰表达式，也叫后缀表达式，它将复杂表达式转换为可以依靠简单的操作得到计算结果的表达式，例如 `(a+b)*(c+d)`转换为 `a b+c d+*`

```js
["4", "13", "5", "/", "+"] ==> (4 + (13 / 5)) = 6
["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
==> ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
```

**分析：** 以符号为触发节点，一旦遇到符号，就将符号前两个元素按照该符号运算，并将新的结果入栈，直到栈内仅一个元素

```js
function isOperator(str) {
    return ['+', '-', '*', '/'].includes(str);}
// 逆波兰表达式计算
function clacExp(exp) {
    const stack = new Stack();
    for (let i = 0; i < exp.length; i++) {
        const one = exp[i];
        if (isOperator(one)) {
            const operatNum1 = stack.pop();
            const operatNum2 = stack.pop();
            const expStr = `${operatNum2}${one}${operatNum1}`;
            const res = eval(expStr);
            stack.push(res);
        } else {
            stack.push(one);
        }
    }
    return stack.peek();
}
console.log(clacExp(["4", "13", "5", "/", "+"])); // 6.6
```

**（3）利用普通栈实现一个有 min方法的栈**

**思路：** 使用两个栈来存储数据，其中一个命名为 `dataStack`，专门用来存储数据，另一个命名为 `minStack`，专门用来存储栈里最小的数据。始终保持两个栈中的元素个数相同，压栈时判别压入的元素与 `minStack`栈顶元素比较大小，如果比栈顶元素小，则直接入栈，否则复制栈顶元素入栈；弹出栈顶时，两者均弹出即可。这样 `minStack`的栈顶元素始终为最小值。

```js
class MinStack {
    constructor() {
        this._dataStack = new Stack();
        this._minStack = new Stack();
    }
  push(item) {
      this._dataStack.push(item);
      // 为空或入栈元素小于栈顶元素，直接压入该元素
      if (this._minStack.isEmpty() || this._minStack.peek() > item) {
          this._minStack.push(item);
      } else {
          this._minStack.push(this._minStack.peek());
      }
  }
  pop() {
      this._dataStack.pop();
      return this._minStack.pop();
  }
  min() {
      return this._minStack.peek();
  }
}
const minstack = new MinStack();
minstack.push(3);
minstack.push(4);
minstack.push(8);
console.log(minstack.min()); // 3
minstack.push(2);
console.log(minstack.min()); // 2
```

#### 三、队列

##### 3.1 队列数据结构

> 队列是遵循**先进先出（FIFO，也称为先来先服务）原则的一组有序的项。队列在尾部添加新元素，并从顶部移除元素**。最新添加的元素必须排在队列的末尾。



![113](https://qq292383147.github.io/pictureLibrary/picture/JavaScript/113.jpg)

类比：日常生活中的购物排队。

##### 3.2 队列的实现

普通的队列常用的有以下几个方法：

- `enqueue` 向队列尾部添加一个(或多个)新的项
- `dequeue` 移除队列的第一(即排在队列最前面的)项，并返回被移除的元素
- `head` 返回队列第一个元素，队列不做任何变动
- `tail` 返回队列最后一个元素，队列不做任何变动
- `isEmpty` 队列内无元素返回 `true`，否则返回 `false`
- `size` 返回队列内元素个数
- `clear` 清空队列

```js
class Queue {
    constructor() {
        this._items = [];
    }
  enqueue(item) {
      this._items.push(item);
  }
  dequeue() {
      return this._items.shift();
  }
  head() {
      return this._items[0];
  }
  tail() {
      return this._items[this._items.length - 1];
  }
  isEmpty() {
      return !this._items.length;
  }
  size() {
      return this._items.length;
  }
  clear() {
      this._items = [];
  }
}
```

与栈类比，栈仅能操作其头部，队列则首尾均能操作，但仅能在头部出尾部进。当然，也印证了上面的话：栈和队列并不关心其内部元素细节，也无法直接操作非首尾元素。

##### 3.3 队列的应用

**（1）约瑟夫环（普通模式）**

**要求：** 有一个数组 `a[100]`存放0~99；要求每隔两个数删掉一个数，到末尾时循环至开头继续进行，求最后一个被删掉的数。

**分析：** 按数组创建队列，依次判断元素是否满足为指定位置的数，如果不是则 `enqueue`到尾部，否则忽略，当仅有一个元素时便输出。

```js
// 创建一个长度为100的数组const arr_100 = Array.from({ length: 100 }, (_, i) => i*i);
function delRing(list) {
    const queue = new Queue();
    list.forEach(e => { 
        queue.enqueue(e);
    });
  let index = 0;
    while (queue.size() !== 1) {
        const item = queue.dequeue();
        index += 1;
        if (index % 3 !== 0) {
            queue.enqueue(item);
        }
    }
  return queue.tail();
}
console.log(delRing(arr_100)); // 8100 此时index=297
```

**（2）菲波那切数列（普通模式）**

**要求：** 使用队列计算斐波那契数列的第n项。

**分析：** 斐波那契数列的前两项固定为1，后面的项为前两项之和，依次向后，这便是斐波那契数列。

```js
function fibonacci(n) {
    const queue = new Queue();
    queue.enqueue(1);
    queue.enqueue(1);
    let index = 0;
    while(index < n - 2) {
        index += 1;
        // 出队列一个元素
        const delItem = queue.dequeue();
        // 获取头部值
        const headItem = queue.head();
        const nextItem = delItem + headItem;
        queue.enqueue(nextItem);
    }
    return queue.tail();
}
console.log(fibonacci(9)); // 34
```

**（3）用队列实现一个栈**

**要求：** 用两个队列实现一个栈。

**分析：** 使用队列实现栈最主要的是在队列中找到栈顶元素并对其操作。具体的思路如下：

1. 两个队列，一个备份队列 `emptyQueue`，一个是数据队列 `dataQueue`；
2. 在确认栈顶时，依次 `dequeue`至备份队列，置换备份队列和数据队列的引用即可。

```js
class QueueStack {
    constructor() {
        this.queue_1 = new Queue();
        this.queue_2 = new Queue();
        this._dataQueue = null;
        // 放数据的队列
        this._emptyQueue = null;
        // 空队列,备份使用
    }
  // 确认哪个队列放数据,哪个队列做备份空队列
    _initQueue() {
        if (this.queue_1.isEmpty() && this.queue_2.isEmpty()) {
            this._dataQueue = this.queue_1;
            this._emptyQueue = this.queue_2;
        } else if (this.queue_1.isEmpty()) {
            this._dataQueue = this.queue_2;
            this._emptyQueue = this.queue_1;
        } else {
            this._dataQueue = this.queue_1;
            this._emptyQueue = this.queue_2;
        }
    };
  push(item) {
      this.init_queue();
      this._dataQueue.enqueue(item);
  };
  peek() {
      this.init_queue();
      return this._dataQueue.tail();
  }
  pop() {
      this.init_queue();
      while (this._dataQueue.size() > 1) {
          this._emptyQueue.enqueue(this._dataQueue.dequeue());
      }
      return this._dataQueue.dequeue();
  };
};
```

同样的，一个队列也能实现栈的基本功能：

```js
class QueueStack {
    constructor() {
        this.queue = new Queue();
    }
  push(item) {
      this.queue.enqueue(item);
  }
  pop() {
      // 向队列末尾追加 队列长度-1 次，后弹出队列头部
      for(let i = 1; i < this.queue.size(); i += 1) { 
          this.queue.enqueue(this.queue.dequeue());
      }
      return this.queue.dequeue();
  }
  peek() {
      return this.queue.tail();
  }
}
```

学习了栈和队列这类简单的数据结构，我们会发现。**数据结构并没有之前想象中那么神秘，它们只是规定了这类数据结构的操作方式：栈只能对栈顶进行操作，队列只能在尾部添加在头部弹出；且它们不关心内部的元素状态。**