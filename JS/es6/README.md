# ES6标准入门
## let 和 const
#### let
1. let声明的变量只在let命令所在的代码块内有效
```
{
    let a = 1
    var b = 2
}
a // ReferenceError: a is not defined
b // 2
```
2. 不存在变量提升。使用var声明的变量可以在声明前使用，值为undefined，而使用let声明的变量不可以在声明前使用，使用会报错。
```

{   
    console.log(a)  //ReferenceError: Cannot access 'a' before initialization
    let a = 2
    
    console.log(b) // undefined
    var b = 3
}
```
3. 不允许重复声明变量，包括函数的参数
```
let func = () => {
    let a = 2
    let a = 4  // Uncaught SyntaxError: Identifier 'a' has already been declared
}


let func = (name) => {
    let name = 4 // Uncaught SyntaxError: Identifier 'name' has already been declared
}
let func = (name) => {
    {
        let name = 'tim' // 不报错
    }
}
```
4. ES5没有块级作用域，所以内部变量可能会覆盖外部的变量

#### const
1. const声明一个只读的常量，一但声明，值就不能改变。
2. 实际上const指向的是一个内存地址，这个内存地址不能改变。但是对于对象和数组而言，变量指向的是这个内存地址的指针，只能固定指针，不能固定里面的值。
```
const a = {}

a.name = 'hello'
console.log(a) // {name: "hello"}

a = []  //Uncaught TypeError: Assignment to constant variable.

```

## 变量的解构赋值
1. es6允许按照一定模式从**数组**和**对象**中提取值，并对变量赋值，这样叫解构。
```
let [x, y] = [1, 2]

x // 1
y // 2
```
2. 解构不成功的，值为undefined
```
let [a, b] = [1]
console.log(`a`, a)   // a 1
console.log(`b`, b)   // b undefined
```
3. 不完全解构，可以赋值成功
```
let [a] = [1, 2]
a // 1
```
4. 解构赋值允许指定默认值
```
let [foo = true] = []
foo // true
```
5. 对象也可以解构赋值，只是不像数组那样有序排列，而是根据命名进行匹配的。
```
let {foo, bar} = {bar: 'b', foo: 'a'}
foo // a
bar // b
```
6. 如果变量名和属性名不一致，需要写成这样:
```
let {foo: name} = {foo: 'tim'}
name // 'tim'
```
7. 对象的解构赋值其实是下面这样的形式简写，被赋值的是后者，而不是前者
```
let {foo: foo, bar: bar} = {foo: 'a', bar: 'b'}

```
8.  函数的参数也可以进行解构赋值
```
function add([x, y]) {
    return x + y
}
add([1, 2]) // 3
```

## 字符串的扩展
1. javascript中允许采用`\uxxxx`形式表示一个字符。
2. 以前js只提供了`indexOf()`方法来确定一个字符串中是否包含在另一个字符串中。es6又提供了三种方法。以下方法还接收参数，表示开始搜索的位置。
- `includes()`，返回布尔值，表示是否找到了参数字符串
- `startsWith()`，返回布尔值，表示参数是否在字符串的头部
- `endsWith()`，返回布尔值，表示参数是否在字符串的尾部
3. `repeat()`方法可以将字符串重复n次，并返回新的字符串
4. `padStart()`和`padEnd()`能够补全字符串。第一个参数为字符串的最小长度，第二个参数为要补全的参数
```
'a'.padStart(3, 'b') // 'bba'
'a'.padEnd(3, 'b') // 'abb'
```
常见用途为:
- 位数补全
- 提示字符串格式
```
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```
5. es6引入了模板字符串，用` `` `表示。用`${name}`嵌套变量。
6. 模板字符串里面可以使用表达式/函数等。


## 正则的扩展
1. es6添加了`u`修饰符和`y`修饰符。y修饰符可以表示必须在剩余的匹配中为头部匹配，就是隐含了`^`标志。
2. `sticky`属性，表示是否设置了y修饰符。
3. es5的`source`属性能够返回表达式的正文。
4. es6的`flags`属性能够返回正则表达式的修饰符。
5. `replace`的第二个参数可以是函数，该函数的参数序列如下：
- mathed, 整个匹配结果
- capture1, 第一个组匹配
- capture2, 第二个组匹配
- capture3, 第三个组匹配
- position, 匹配开始的位置
- S, 原字符串
- groups, 具名组构成的一个对象

## 数值的扩展
1. es6提供了`Number.isFinite()`方法和`Number.isNan()`方法。
2. Number.isFinite()用来检查一个数值是否为有限的。
```
Number.isFinite(10) // true
Number.isFinite(2) // true
Number.isFinite(Nan) // false
Number.isFinite(true) // false
Number.isFinite('a') // false
```
3. `Number.isNan()`用来检查一个值是否为`NaN`
4. 这两个方法与`isFinite()`和`isNaN()`区别在于，传统的方法会先调用`Number()`将非数值转换为数值，在进行判断。而新方法只对数值有效。
5. `Number.parseInt()`和`Number.parseFloat()`
6. `Number.isInteger()`判断一个值是否为整数。
```
Number.isTnteger(10) // true
Number.isTnteger(10.0) // true
Number.isTnteger(10.2) // false
Number.isTnteger("10") // false
Number.isTnteger(true) // false
```
7. `Number.EPSILON`是一个极小的常量。因为浮点数计算不准确，如果计算后的值小于这个常量，就认为是正确的。
8. JavaScript能够准确表示的整数范围在-2^53 和 2^53之间。超过这个范围就无法正确显示
```
Math.pow(2, 53)
```
9. `Number.isSafeInteger()`用来判断一个数值是否是在安全数值之内。


## 第七章
1. es6可以直接在参数上赋值
2. 函数的`name`属性会返回函数的函数名。但给一个变量声明函数，es5返回`''`，es6返回变量名。
3. 箭头函数里面的this指向就是函数定义时所在的对象，而不是使用时所在的对象。
4. 箭头函数不可以使用使用arguments对象，该对象在函数体内不存在。可以用rest参数代替。
5. 尾调用就是指某个函数的最后一步是调用另一个函数。
6. 函数调用自身成为递归。如果尾调用自身就称为尾递归。
7. 尾调用优化只在严格模式下生效，因为正在模式下函数内部有两个变量，可以跟踪函数的调用栈。
- arguments 返回调用时函数的参数
- caller 返回调用当前函数的那个参数


## 第八章
1. 扩展运算符(`...`),可以将一个数组转为用逗号分隔的参数序列。
2. 如果将扩展运算符用于数组赋值，则只能将其放在参数的最后一位。
3. `Array.from()`用于将两类对象转为真正的数组：类似数组的对象(array-like object)和可遍历(iterable)对象。
4. `Array.from()`可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理
```
Array.from(...num, x => x > 10)
// 等同于
Array.from(...num).map(x => x > 10)
```
5. `Array.of()`可以将一组值转换为数组。
6. `Array.prototype.copyWithin()`能够复制当前数组内的值到其他位置。接受三个参数：
- target: 从该位置开始替换数据
- start: 从该位置开始读取数据，默认为0,
- ends：到该位置前停止读取数据，默认为数组长度。
7. 数组的`find(value, index, arr)`方法用于找出第一个符合条件的数组成员。如果没有找到，则返回undefined
8. `findIndex()`方法用于找出第一个符合条件成员的位置。如果没有则返回-1。
9. `fill()`方法使用给定值填充一个数组。还可以接受第二个参数和第三个参数，用于指定填充的起始位置和结束位置。
```
[1, 2, 3].fill(5)
// [5, 5, 5]
```
10. 数组实例的`entries()`、`keys()`和`values()`。keys用于遍历键名，values用于遍历键值，entries用于遍历键值对。
```
for(let item of [1, 2, 3].values()) {
    console.log(item)
}
// 1
// 2
// 3
```
```
for(let [index, elem] of ['a', 'b'].entries()) {
    console.log(index, elem)
}
// 0 'a'
// 1 'b'
```

## 第九章
1. es6允许直接写入变量名和函数作为对象的属性和方法
2. es6允许字面量定义对象
```
let foo = 'bar'
let obj = {
    [foo]: 'abc'
}
obj['bar'] // 'abc'
```
3. 函数的name属性可以获取函数名。bind方法创造的函数，name属性返回`bound`加上原函数的名字。如果对象的方法是一个Symbol值，那么name属性返回的是Symbol值的描述。
4. 相等运算符`==`会自动转换数据类型。严格相等运算符`===`不会转换。
5. Object.is()可以比较两个值是否严格相等。
```
Object.is('foo', 'foo') // true
```
6. Object.assign()方法用于将源对象的所有可枚举属性复制到目标对象。第一个参数是复制到的对象（目标对象），后面的参数是要复制的对象（源对象）。
```
let obj1 = {
    a: 1
}
let obj2 = {
    b: 2
}
let obj3 = {
    c: 3
}

Object.assign(obj1, obj2, obj3)
obj1 // {a: 1, b: 2, c: 3}
let obj4 = Object.assign({}, Obj2, obj3)
```
7. 如果有多个同名属性，则后面的会覆盖前面的。
8. Object.assign()方法实行的是浅复制，而不是深复制。也就是说，如果源对象的某个属性的值是**对象**，那么目标对象复制得到的是**这个对象的引用**。而且修改对象会改变原来对象的内容。
9. 为对象添加方法:
```
Object.assign(SomeClass.prototype, {
    someMethods() {},
    someMethods() {},
})
```
10. `Object.getOwnPropertyDescriptor()`能够获取该属性的描述对象。如果对象的enumerable（可枚举）为false，就表示某些操作会忽略当前属性。
11. Object.__proto__代替方案：
- Object.setPrototypeOf() （写操作）
- Object.getPrototypeOf() （读操作）
- Object.create() （生成操作）
12. 对象的解构赋值，同样复制是进行浅复制。如果一个键的值是复合类型的值（数组、对象、函数），那么解构赋值复制的是这个值的引用，而不是这个值的副本。
13. 解构赋值不会复制继承自原型对象的属性。
14. 扩展运算符用于取出参数对象的所有可遍历属性，并将其复制到当前对象之中。
```
let z = {a: 3, b: 4}
let n = {...z}
```
等同于使用Object.assin方法
```
let aClone = {...a}
等同于
let aClone = Object.assin({}, a)

let aClone = {...a, ...b}
等同于
let aClone = Object.assign({}, a, b)
```
15. es5的`Object.getOwnPropertyDescriptor()`可以用来获取某个对象属性的描述对象
```
let obj = {
    name: 'a'
};
console.log(Object.getOwnPropertyDescriptor(obj, 'name'));
```
16. es8（es2017）引入了`Object.getOwnPropertyDescriptors`方法，返回指定对象**所有**自身属性。该方法的引用主要是为了解决`Object.assign()`无法正确复制get属性和set属性的问题。


## 第十章
1. es6引入了一种新的原始数据类型`Symbol`，**表示独一无二的值**。它是JavaScript语言的**第7种**数据类型，前6种分别是：`Undefined`、`Null`、`Boolean`、`String`、`Number`、`Object`。
2. Symbol是一个原始类型的值，不是对象。也就是说，由于Symbol值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。
3. Symbol值不能与其他类型的值进行运算，否则会报错。
4. Symbol值作为对象属性名时不能使用点运算符。
5. 在对象的内部，使用Symbol值定义属性时，Symbol值必须放在方括号中。
```
let s = Symbol()
let obj = {
    [s]: arg => { ... }
}
obj[s](132)
```
6. `Object.getOwnPropertySymbols()`可以获取指定对象的所有Symbol属性名。
7. 使用`Reflect.ownKeys()`方法可以返回所有类型的键名，包括常规键名和Symbol键名。
8. `Symbol.for()`可以搜索有没有以该参数作为名称的symbol值，如果有，则返回，没有则创建。创建的值会被登记在全局环境中供搜索，而symbol()不会。
9. `Symbol.keyfor()`返回一个已登记的symbol类型值的key。
10.  194p


## 第十一章
1. es6提供了新的数据结构——Set。它类似与数组，但是**成员的值都是唯一的，没有重复**。
2. 数组去重：`[...new Set(arr)]`
3. set实例的方法：
- add(value): 添加某个值
- delete(value): 删除某个值
- has(value): 返回一个布尔值，表示参数是否为set的成员
- clear(value): 清除所有成员
4. 数组去重函数：
```
let dedupe = array => {
    return Array.from(new Set(array))
}
```
5. 遍历方法:
- keys(): 返回键名的遍历器
- values(): 返回键值的遍历器
- entries(): 返回键值对的遍历器
- forEach(): 使用回调函数遍历每个成员
6. set的遍历顺序就是插入的顺序，能够按照顺序调用。
7. 扩展运算符（`...`）内部使用for...of循环。
8. WeakSet结构与set类似，不过有两个区别：
- WeakSet的成员只能是对象，不能是其他的值。
- WeakSet中的对象引用都是弱引用，垃圾回收机制不考虑WeakSet对该对象的引用。
9. WeakSet有三个方法：
- WeakSet.prototype.add(value)
- WeakSet.prototype.delete(value)
- WeakSet.prototype.has(value)
10. Map结构的键可以是各种类型的值。
11. Map的键实际上是和内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞的问题，我们扩展别人的库时，如果使用对象作为键名，不用担心自己的属性与原作者的属性同名。
12. Map结构的方法：
- set(key, value)： set方法设置key所对应的键值。如果有值则更新，没有则创建
- get(key): 读取key对应的键值，如果找不到，则返回undefined
- has(key): 返回一个布尔值，表示某个键是否存在
- delete(key): 返回一个布尔值，如果删除失败，返回`false`
- delete(key): 删除某个键
- clear()： 清除所有成员。
13. Map的遍历方法：
- keys(): 返回键名的遍历器
- values(): 返回键值的遍历器
- entries(): 返回所有成员的遍历器
- forEach(): 遍历Map的所有成员。按插入顺序遍历。
。。。
---

## 第十二章
1. proxy用于修改某些操作的默认行为，可以理解成在目标对象前架设一个*拦截层*，外界对该对象的访问都必须通过这层拦截。
2. es6原声提供Proxy构造函数，用于生成proxy实例。`let proxy = new Proxy(target, handler)`。target表示所要拦截都目标对象，handler也是一个对象，用来定制拦截行为。

## 第十三章


## 第十四章
1. promise 是异步编程的一种解决方案。Promise是一个对象，从它可以获取异步操作的消息。
2. promise有三种状态。只有异步操作的结果可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。
- `Pending` 进行中
- `Fulfilled` 已成功
- `Rejected` 已失败
3. 一旦状态改变，就不会再变。Promise状态的状态改变只有两种可能，从Pending变为Fulfilled和从Pending变为Rejected。
4. Promise可以将异步操作以同步操作的流程表达出来，避免来层层嵌套的回调函数。
5. 一个新的Promise实例：
```
let promise = new Promise((resolve, reject) => {
    if(/*   异步操作成功  */) {
        resolve(value)
    }else {
        reject(error)
    }
})
```
6.一般来说，调用resolve和reject后，Promise的使命就完成了，后续操作应该放在then方法里面，而不是直接写在resolve和reject后面。所以，**最好在他们前面加上return语句，这样就不会产生意外。**
```
new Promise((resolve, reject) => {
    return resolve(1)
})
```
7. Promise对象的错误具有冒泡性质，会一直向后传递，直到被捕获为止。也就是说，错误总是会被下一个catch语句捕获。
8. Promise.all()方法用于将多个Promise对象封装成一个新都Promise实例。
9. Promise的状态有两种情况：
- 只有所有参数的状态都变为`fulfilled`，才会返回`fulfilled`。
- 只要有一个被`rejected`,就会返回`rejected`.
10. Primise.race()方法也是将多个Promise实例转包装成一个新都Promise实例。但是**只要有一个实例率先改变状态，就会改变状态。**
```
// 可以设置一个5秒超时响应。如果5秒后没有响应返回，则返回一个错误
let p = Promise.race([
    Promise.resovle(...),
    new Promise((resolve, reject) => {
        setTimeout(() => {
            reject(request timeout)
        }, 5000)
    })
])
```
11. Promise.resolve()可以将现有对象转换为Promise对象。
12. Promise.resolve是在本轮“事件循环结束”时调用，而不是在下一轮“事件循环”开始时执行。
```
setTimeout(() => {
    console.log('three')
})

Promise.resolve().then(res => {
    console.log('two')
})

console.log('one')


// 'one'
// 'two'
// 'three'

setTimeout() 是在下一轮 事件循环 开始时执行的，Promise.resolve是在本轮 事件循环 结束时执行，console.log 则是立即执行。
```
13. Promise.reject返回一个rejected状态的Promise实例。


## 第十八章
1. async函数返回一个Promise对象，可以使用then方法添加回调函数。当函数执行当时候，一旦遇到await就会先返回，等到异步操作成功，再接着执行函数体内后面的语句。
2. async函数有多种使用形式：
```
async function foo() {}

const foo = async function() {}

let obj = { async foo () {}}
obj.foo.then()

const foo = async () => {}
```
3. 如果await语句后面的Promise变为reject，那么整个async函数都会中断执行，可以使用catch进行捕获。
```
async function f() {
    await Promise.reject(error)
    .catch(err => throw err)
    
    return await Promise.resolve('hello world')
}
```
4. 多个await命令后面的异步操作如果不存在继发关系，最好让他们同时触发。因为只有执行完第一个后，才会执行第二个，这样比较耗时。
```
// 写法一
let [foo, bar] = await Promise.all([xxx, xxx])

// 写法二
let fooP = getFoo()
let barP = getBar()

let foo = await fooP
let bar = await Bar

// 这样就会同时触发，节省程序执行时间

```

## 第二十二章
1. 在ES6之前，社区有一些模块加载方案，最主要的有CommonJS和AMD两种。前者用于服务器，后者用于浏览器。
2. 模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
```
export let first = 'first'
export let second = 'second'

// 或者
let first = 'first'
let second = 'second'

export {first, second}    // 优先采用这种写法 一目了然
```
3. import命令在编译阶段执行，所以是最早执行的。
4. 可以整体加载：`import * as xxx`
```javascript
// test.js
let first = 'first'
let second = 'second'

export {first, second}

// 
import * as core from '../test

core.first
core.second
```
5. export default 相对于 export 来说，可以省略`{}`，但是只能使用一次。
6. require是运行时加载模块。到底加载哪一个模块只有在运行时才能够知道。

## 第二十三章
1. 默认情况下，浏览器同步加载JavaScript脚本，即渲染引擎遇到`<script>`标签就会停下来，等到脚本执行完毕再继续向下渲染。如果是外部脚本，还必须加入脚本下载的时间。
2. 使用`defer/async`可以使脚本异步加载。渲染引擎遇到这一行命令就会开始下载外部脚本，但不会等它下载和执行，而是直接执行后面的命令。
3. defer和async的区别是：
- defer 
    - 等到页面正常渲染结束才会执行
    - 多个脚本按照顺序执行
- async
    - 一旦下载完成，渲染引擎就会中断渲染，执行这个脚本后再继续渲染 
    - 多个脚本不能保证按照顺序
4. 浏览器加载es6模块时使用`type='module'`属性。
5. CommonJS模块输出的是值的赋值，会缓存值。而ES6模块是动态引用，不会缓存值。

