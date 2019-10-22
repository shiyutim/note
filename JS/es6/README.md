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
1. const声明一个只读的常量，一单声明，值就不能改变。
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