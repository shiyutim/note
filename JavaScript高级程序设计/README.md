# JavaScript高级程序设计笔记
## 第一章
1. JavaScript诞生于1995年。
2. 一个完整的JavaScript应由以下三个不同的部分组成
* 核心（JavaScript）**提供核心语言功能**
* 文档对象模型（DOM）**提供访问和操作网页内容的方法和接口**
* 浏览器对象模型（BOM）**提供与浏览器交互的方法和接口**
## 第二章
1. `<script>`标签：
* `async`属性：表示**应该立即下载脚本**，但不影响页面中的其他操作，如下载其他资源或等在加载其他脚本等。只对外部脚本文件有效。**脚本不会按照先后顺序执行**
* `defer`属性： 表示脚本可以延迟到文档完全被解析和现实之后再执行。只对外部脚本文件有效。**脚本按照先后顺序执行**
2. 包含在`<script>`标签内的JS代码将**从上至下**依次解释。
    在解释器对`<script>`内部的代码求值完毕前，**页面中的其余内容都不会被浏览器加载或显示**
3. 因为浏览器在遇到`<body>`标签时，才开始呈现内容，所以应该把`<script>`标签**放到页面内容底部**。
4. 使用外部加载JS脚本文件：
* 可维护性
* 可缓存
* 适应未来
## 第三章
1. JS中的一切都区分大小写
2. 标识符规则：
* 第一个字符必须是一个字母/下划线或一个美元符号
* 其他字符可以是字母/下划线/美元符号或数字
3. ECMA的变量是松散类型的，也就是说可以用来保存任何类型的数据。
4. 使用var定义的变量，成为该作用域中的局部变量。也就是说退出函数后，这个变量会被销毁。
5. ECMA中有5种简单数据类型：
* undefined
* Null
* number
* string
* boolean

一种复杂数据类型：
* object
6. 使用`typeof`可以判断数据的类型，用法为
```
var message = "hello world";
console.log(typeof message) //string
```
7. 如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为null。这样只要检查null值就可以知道相应的变量是否已经保存了一个对象的引用了。
```
if(car != null) {
    //某些操作
}
```
8. 使用`Boolean()`可以转换对应的boolean值。
```
var message = "hello world"
if (message) {
    console.log("value is true")
}
```
9. 保存浮点数值需要的内存空间是保存整数值的两倍
10. ECMA能够表示的最小数值保存在`Number.MIN_VALUE`中。最大数值保存在`Number.MAX_VALUE`中。
11. 使用`isFinite()`可以测试这个数是否在最大或最小数的中间。`true`为存在，`false`为不存在。
12. NaN(Not a number)即非数值，用于表示一个本来要返回数值的操作数没有返回数值的情况。因为这样就不会抛出错误了。
13. `isNaN()`用来判断**是否不是数值**。
14. 有三个函数可以把非数值转换为数值：
* Number()
* parseInt()
* parseFloat()

Number()可以转换任意类型，其他两个则专门用于把**字符串转换成数值**。

由于Number()函数在转换字符串时比较复杂且不够合理，因此处理整数的时候更常用的是`parseInt()`函数。此函数在转换时，更多的是看其是否符合数值模式。它会忽略前面的空格，直至找到第一个非空格字符串。
```
var num = parseInt("1234blue")  // 1234
```
对于多进制，可以提供参数
```
var num = parseInt("0xAF", 16);
```

**多数情况下，我们要解析的都是十进制数值，因此始终将10作为第二个参数是非常必要的**

`parseFloat()`只能解析10进制值，并且只能解析一个小数点的数值。
```
var num = parseFloat("22.34.5") // 22.34
```

15. `\r`为回车，`\n`为换行
16. 任意长度的字符串可以通过访问其`length`的属性取得：
```
var str = "hello world";
console.log(str.length)  // 11
```
17. 要把一个值转换为字符串可以使用`toString()`方法。
```
var boolean = true
var stringBoolean = boolean.toString()  // "true"
```

还有一个`String()`方法，此方法对null和undefined返回他本身
```
var value;
console.log(String(value) // undefined
```

18. 按位非，用波浪线（~）表示，返回数值的反码。其实就是：操作数的负值减1.
```
var num = 25;
console.log(~num)   // -26

//等同于
var num1 = 25;
var num2 = -num - 1;
console.log(num2)  // -26
```

19. 逻辑与操作符（&&）,规则为：
* 如果第一个运算子的布尔值为true，则返回第二个运算子的值。
* 如果第一个运算子的布尔值为false，则返回第一个运算子的值。

20. +法操作有时候会拼接字符串，如：
```
var num1 = 5;
var num2 = 10;
var message = "The number is" + num1 + num2 
console.log(message) // The number is 510
```
想要正确的计算值，可以加个括号，如:
```
var num1 = 5;
var num2 = 10;
var message = "The number is" + (num1 + num2 )
console.log(message) // The number is 15
```

21. `==`表示相等，`===`表示全等。规则为：
* == 在比较前会先转换类型。
* === 直接比较，不会转换类型，比较严格
```
var result1 = ("55" == 55)  // true 转换之后相等
var result1 = ("55" === 55)  // false 因数据类型不同，返回false
```

22. 条件操作符，也就是三元表达式`xx?xx:xx`
```
var max = (num1 > num2) ? num1 : num2
//以上代码max中储存一个最大的值
```

## 第四章
1. 一个变量从另一个变量复制**基本类型的值**，会创建一个新值，两者不会影响，如：
```
var num1 = 5;
var num2 = num1;

num1 = 10;
console.log(num1)  // 10
console.log(num2)  // 5
```
2. 一个变量从另一个变量复制**引用类型的值**；而两个的指针都指向同一个对象。改变一个会影响另外一个。如：
```
var obj1 = new Object();
var obj2 = obj1;

obj1.name = "tim";
console.log(obj2.name)  // tim
```
3. 使用`instanceof`可以检测一个值的类型，如：
```
var person = new Object();
console.log(person instanceof Object); // true
```
4. 某个执行环境中的代码执行完毕后，改环境被销毁，同时其中保存的变量和函数定义也会被销毁。
5. 全局环境被认为是window对象。其执行环境直到应用退出后，才会被销毁。
6. 内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数。
7. 访问数据就近原则，如果在局部环境内能访问到，就取局部的值，如果访问不到，会逐级向上搜索。
```
var color = "blue";
function getColor() {
    var color = "red";
    return color;
}
console.log(getColor());  // red
```
如果想要访问到全局的color，需要这样写
```
{
    return window.color
}
console.log(getColor()) // blue
```

8. JavaScript具有自动垃圾收集机制。其原理是： 找出那些不再继续使用的变量，然后释放其占用的内存。为此，垃圾收集器会按照固定的时间间隔周期性的执行这一操作。
9. JS中最常用的垃圾收集方式是标记清除。垃圾收集器在运行的时候会给内存中的所有变量加上标记。然后去掉标记。**再被加上标记的变量**视为**准备删除的变量**。最后，垃圾收集器完成内存清除工作。
10. 另外一种不太常见的垃圾收集策略叫做引用计数。意思为跟踪记录每个值被引用的次数。
