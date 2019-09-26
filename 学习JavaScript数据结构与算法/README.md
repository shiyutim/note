## 第一章 JavaScript简介
1. null 表示变量没有值，undefined表示变量已被声明，但尚未赋值
2. 尽量避免使用全局变量
3. 在JavaScript中有两种数据类型
* 原始数据类型： null、undefined、bollean、string、number和Symbol
* 派生数据类型： 函数、数组和正则表达式
4. 如果字符串为空（长度为0）就是false，其他都是true（长度大于等于1）
```
if (name == '')
//   可以写成 
if (!name)
```

## 第二章 ECMAScript和TypeScript
1. ECMA是一个将信息标准化的组织。而JavaScript是该标准的一个实现
2. JavaScript函数中有一个内置的对象，叫做arguments对象。它是一个数组，包含函数调用时传入的参数。即使不知道参数的名称，我们也可以动态获取并使用这些参数
3. 使用typescript可以实现静态检查


## 第三章 数组
1. 斐波那契数列，即前两个数相加，等于第三个数。数学上的公式为`F(1)=1，F(2)=1, F(n)=F(n-1)+F(n-2)`。意思为，先定义前两个数字分别为1，然后开始相加。
```
let arr = [, 1, 1] //这里0不存在，因此为空

for (let i=3;i<20;i++) {
    arr[i] = arr[i-1] + arr[i-2]
}
```
2. 在数组的开头添加值，可以使用unshift()方法。
```
let arr = [0, 1, 2, 3, 4, 5]
    Array.prototype.insertFirstPosition = function (value) {
        for(let i=this.length;i>=0;i--) {
            this[i] = this[i -1]
        }
        this[0] = value
    }
    arr.insertFirstPosition(100)
```
3. 从数组的末尾删除元素，可以使用pop()。
4. 删除数组的第一个元素使用shift()。
5. 使用@@iterator可以获得数组中的值
```
const num = [5, 13, 15, 32]

let num2 = num[Symbol.iterator]()

方法一for循环遍历：
for(let i=0;i<num.length;i++) {
    console.log(num2.next().value)
}
方法二for of循环遍历：
for (let i of num2) {
    console.log(i)
}

```
6. 使用entries()可以获取数组中的键值对集合
```
const num = [5, 13, 15, 32]
let entries = num.entries()
for(let i of entries) {
    console.log(i)
}
```
7. keys()方法返回包含数组索引的@@iterator。
```
const num = [5, 13, 15, 32]
const akeys = num.keys()
console.log(akeys.next()) // {value: 0, done: false}
console.log(akeys.next()) // {value: 1, done: false}
console.log(akeys.next()) // {value: 2, done: false}
console.log(akeys.next()) // {value: 3, done: false}
console.log(akeys.next()) // {value: undefined, done: true}
直到数组值遍历完之后，返回undefined和true
```
8. values()方法返回@@iterator包含数组的值。
9. 使用from()可以根据已有的数组创建一个新数组
```
const num = [5, 13, 15, 32]
const num2 = Array.from(num)
```
还可以传入值
```
const num2 = Array.from(num, i => i > 10)
// false,true,true,true
```
10. fill()方法可以填充数组。还可以指定索引，fill(9, 1, 3)
```
const num = [5, 13, 15, 32]
const num2 = Array.from(num).fill(9)
// (4)[9, 9, 9, 9]
// num2先复制num，然后填充4个9

const num2 = Array.from(num).fill(9, 1, 3)
// 填充为9，从第2个开始，到第4个结束(不包括)
// [5, 9, 9, 32]
```
11. copyWithin()方法可以复制数组中一系列元素到同一数组中指定的位置。copyWithin(复制到哪， 复制值起始， 复制值结束(不包含))
12. JavaScript在做字符串比较的时候，是根据字符对应的ASCII值来比较的
13. find()方法可以搜索一个满足回调函数条件的值，返回第一个满足条件的值。findIndex()返回这个值在数组里的索引
14. includes()方法可以检测数组里是否存在某个元素。


## 第四章 栈
1. 栈是一种遵从后进先出原则的有序集合。新添加或待删除的元素都保存在栈的同一端，称作栈顶，另一端就叫栈底。在栈里，新元素都靠近栈顶，旧元素都接近栈底。
2. 使用Class类给栈封装了几个方法：
```
class Stack {
    constructor() {
        this.count = 0
        this.items = {}
    }
    push(element) {
        this.items[this.count] = element
        this.count++
    }
    pop() {
        if (this.isEmpty()) {
            return undefined
        }
        this.count--
        const result = this.items[this.count]
        delete this.items[this.count]
        return result
    }

    // 查看栈顶(数组新添加的项)，也就是最后一项
    peek() {
        if(this.isEmpty()) {
            return undefined
        }
        return this.items[this.count - 1]
    }

    isEmpty() {
        return this.count === 0
    }
    size() {
        return this.count
    }
    clear() {
        this.count = 0
        this.items = {}
        // while(!this.isEmpty()) {
        //     this.pop()
        // }
    }
    toString () {
        debugger;
        if (this.isEmpty()) {
            return ''
        }
        let str = `${this.items[0]}`
        for(let i=1;i<this.count;i++) {
            str = `${str},${this.items[i]}`
        }
        return str
    }
}

```
3. 基于以上，又封装了10进制转为2进制的方法：
```
function decimalToBinary(decNumber) {
    const remStack = new Stack()
    let number = decNumber
    let str = ''
    let rem = null
    while(number > 0) {
        rem = Math.floor(number % 2)
        remStack.push(rem)
        number = Math.floor(number / 2)
    }
    while(!remStack.isEmpty()) {
        str += remStack.pop().toString()
    }
    return str
}
```
4. 基于以上，封装了10进制转为2-36进制的方法：
```
function decimalToBinary(decNumber, base) {
    const remStack = new Stack()
    const digits = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    let number = decNumber
    let str = ''
    let rem = null

    if(!(base >=2 && base <= 36)) {
        return ''
    }

    while(number > 0) {
        rem = Math.floor(number % base)
        remStack.push(rem)
        number = Math.floor(number / base)
    }
    while(!remStack.isEmpty()) {
        str += digits[remStack.pop()]
    }
    return str
}
```

## 第五章 队列和双端队列
1. 队列是遵循先进先出(FIFO)原则的一组有序的项。队列在尾部添加新元素，并从顶部移除元素。最新添加的元素必须排在队列的末尾
2. 按照队列的原则封装了方法：
```
class Queue {
    constructor () {
        this.items = {}
        this.count = 0       // 代表当前个数
        this.lowestCount = 0  // 最顶部的值
    }
    // 队列尾部添加项
    enqueue (element) {
        this.items[this.count] = element
        this.count++
    }
    // 移除队列的第一项
    dequeue () {
        if(this.isEmpty()) {
            return undefined
        }
        let result = this.items[this.lowestCount]
        delete this.items[this.lowestCount]
        this.lowestCount++
        return result
    }
    // 返回队列中第一个元素
    peek () {
        if(this.isEmpty()) {
            return undefined
        }
        return this.items[this.lowestCount]
    }            
    isEmpty () {
        return this.count-this.lowestCount === 0
    }
    clear () {
        this.items = {}
        this.count = 0
        this.lowestCount = 0
    }
    size () {
        return this.count-this.lowestCount
    }
    toString () {
        if(this.isEmpty()) {
            return undefined
        }
        let str = this.items[this.lowestCount]
        for(let i=this.lowestCount+1;i<this.count;i++) {
            str = `${str},${this.items[i]}`
        }
        return str
    }            
}
```

## 第六章 链表
1. 链表储存有序元素的集合，但不同于数组，链表中的元素在内存中并不是连续放置的。每个元素由一个储存元素本身的节点和一个指向下一个元素的引用组成。
2. 