# ES6 标准入门

## let 和 const

#### let

1. let 声明的变量只在 let 命令所在的代码块内有效

```
{
    let a = 1
    var b = 2
}
a // ReferenceError: a is not defined
b // 2
```

2. 不存在变量提升。使用 var 声明的变量可以在声明前使用，值为 undefined，而使用 let 声明的变量不可以在声明前使用，使用会报错。

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

4. ES5 没有块级作用域，所以内部变量可能会覆盖外部的变量

#### const

1. const 声明一个只读的常量，一单声明，值就不能改变。
2. 实际上 const 指向的是一个内存地址，这个内存地址不能改变。但是对于对象和数组而言，变量指向的是这个内存地址的指针，只能固定指针，不能固定里面的值。

```
const a = {}

a.name = 'hello'
console.log(a) // {name: "hello"}

a = []  //Uncaught TypeError: Assignment to constant variable.

```

## 变量的解构赋值

1. es6 允许按照一定模式从**数组**和**对象**中提取值，并对变量赋值，这样叫解构。

```
let [x, y] = [1, 2]

x // 1
y // 2
```

2. 解构不成功的，值为 undefined

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

1. javascript 中允许采用`\uxxxx`形式表示一个字符。
2. 以前 js 只提供了`indexOf()`方法来确定一个字符串中是否包含在另一个字符串中。es6 又提供了三种方法。以下方法还接收参数，表示开始搜索的位置。

- `includes()`，返回布尔值，表示是否找到了参数字符串
- `startsWith()`，返回布尔值，表示参数是否在字符串的头部
- `endsWith()`，返回布尔值，表示参数是否在字符串的尾部

3. `repeat()`方法可以将字符串重复 n 次，并返回新的字符串
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

5. es6 引入了模板字符串，用` `` `表示。用`${name}`嵌套变量。
6. 模板字符串里面可以使用表达式/函数等。

## 正则的扩展

1. es6 添加了`u`修饰符和`y`修饰符。y 修饰符可以表示必须在剩余的匹配中为头部匹配，就是隐含了`^`标志。
2. `sticky`属性，表示是否设置了 y 修饰符。
3. es5 的`source`属性能够返回表达式的正文。
4. es6 的`flags`属性能够返回正则表达式的修饰符。
5. `replace`的第二个参数可以是函数，该函数的参数序列如下：

- mathed, 整个匹配结果
- capture1, 第一个组匹配
- capture2, 第二个组匹配
- capture3, 第三个组匹配
- position, 匹配开始的位置
- S, 原字符串
- groups, 具名组构成的一个对象

## 数值的扩展

1. es6 提供了`Number.isFinite()`方法和`Number.isNan()`方法。
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
8. JavaScript 能够准确表示的整数范围在-2^53 和 2^53 之间。超过这个范围就无法正确显示

```
Math.pow(2, 53)
```

9. `Number.isSafeInteger()`用来判断一个数值是否是在安全数值之内。

## 第七章

1. es6 可以直接在参数上赋值
2. 函数的`name`属性会返回函数的函数名。但给一个变量声明函数，es5 返回`''`，es6 返回变量名。
3. 箭头函数里面的 this 指向就是函数定义时所在的对象，而不是使用时所在的对象。
4. 箭头函数不可以使用使用 arguments 对象，该对象在函数体内不存在。可以用 rest 参数代替。
5. 尾调用就是指某个函数的最后一步是调用另一个函数。
6. 函数调用自身成为递归。如果尾调用自身就称为尾递归。
7. 尾调用优化只在严格模式下生效，因为正在模式下函数内部有两个变量，可以跟踪函数的调用栈。

- arguments 返回调用时函数的参数
- caller 返回调用当前函数的那个参数
