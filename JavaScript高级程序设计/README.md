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


#### 第五章 引用类型
1. 新对象是使用new操作符后跟一个构造函数来创建的。构造函数本身就是一个函数，只不过该函数是出于**创建新对象**的目的而定义的。
2. `Array.isArray()`可以判断是不是数组
```
var list = []
Array.isArray(list)    // true
```
3. `join()`方法能使用不同的分隔符来构建这个字符串。
```
let str = ["hello", "world"];
let result = str.join(",") // hello,world
```
4. `push()`可以添加任意数量的值，把它们添加到数组的末尾，并返回数组的长度。
5. `pop()`从数组末尾移除最后一项，返回移除的项。
6. `shift()`移除数组的第一项，并返回该项。
7. `unshift()`在数组的前端添加任意项。
8. `reverse()`方法反转数组项的顺序。
9. `sort()`方法也会对数组进行排序，但是是按字符串进行的比较。所以需要定义一个方法。
```
function compare(value1, value2) {
    if(value1 < value2) {
        return -1
    }else if(value > value2) {
        return 1
    }else {
        return 0;
    }
}

var values = [1, 3, 5, 10]
values.sort(compare)
```

```
function compare(value1, value2) {
    return value2 - value1
}
```
10. `concat()`方法将参数添加到数组的末尾。
11. `slice()`方法将返回指定参数位置的值。如果有两个参数，则返回起始和结束位置之间的项，但不包括结尾位置的项。
```
var colors = ["red", "yellow", "blue", "orange"];
var colors2 = colors.slice(1); // ["yellow", "blue", "orange"]
var colors3 = colors.slice(1, 3);  // ["yellow", "blue"]
```
12. `splice()`方法能够进行：
* 删除：`splice(1, 2)`1是要删除位置，2是删除项数。
* 插入：`splice(1, 0, "red", "green")`1是要插入的位置，0是要删除的项，剩下两个是要插入的项
* 替换：`splice(1, 2, "red", "green")`1是起始位置，2是要删除的项，剩下两个是要替换的项
13. `indexOf()`和`lastIndexOf()`是用来查找的。接收两个参数，要查找的项和表示查找起点位置的索引。`indexOf()`从前向后查找，`lastIndexOf()`相反。如果没找到，返回-1。
14. 迭代方法
* `every()`,对每一项进行判断，如果都符合条件，返回true,否则返回false
* `some()`，对每一项进行判断，只要其中一项符合条件，就返回true。
* `filter()`，对数组进行遍历，返回符合条件的值。这个方法对查询符合某些条件的数组项非常有用。
* `map()`，能够对数组中的每一项进行相对应的操作。
* `forEach()`方法能够对数组中的每一项运行传入的函数。
15. 递归方法：
* `reduce()`,这个方法接收四个参数。可以用来求和
    * `prev`前一个值
    * `cur`当前值
    * `index`项的索引
    * `array`数组对象
```
let arr = [1, 45, 3, 54, 25, 3];
let item = 0;
item = arr.reduce(function(prev, cur, index, array) {
    return prev + cur
}
```
* `reduceRight()`，方法相同，遍历方向相反。
16. `Date.now()`获取当前的时间戳。使用`+new Date()`方法同样能获取到。
17. 使用不带圆括号的函数名是访问函数指针，而不是调用函数。
18. 如果创建了两个同名函数，**第二个会覆盖掉第一个**
19. 函数的`length`属性定义了函数参数的个数。
20. `apply()/call()/bind()`能够改变this的指向。
21. `.toFixed(2)`转换小数点后两位。
22. `toExponential(2)`返回以指数表示法表示的数值的字符串形式。
23. `toPrecision(2)`返回最合适的格式。
24. `charAt()`返回指定位置的值。
25. `concat()`可以拼接字符串。
>虽然这个方法是专门用来拼接字符串的方法，但在实践中使用更多的还是`+`，使用`+`在大多数情况下都比使用`concat()`方法要简便易行。
26. `trim()`方法能够返回去掉前置和后置的空格之后的值。
27. `toUpperCase()`转换大写`toLowerCase()`转换小写
28. `split()`方法能够将指定的分隔符把字符串分割。
29. `localeCompare()`方法能够比较两个字符串，然后返回特定的值。
30. `Math.max()`返回指定数组的最大值。`Math.min()`返回指定数组的最小值。
31. 舍入方法
* `Math.ceil()`向上舍入
* `Math.floor()`向下舍入
* `Math.round()`标准舍入
32. `Math.random()`方法返回一个大于等于0小于1的一个随机数。

#### 第六章
1. ECMAScript中有两种属性：
* 数据属性
    * `Configurable`表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
    * `Enumerable`表示能否通过`for-in`循环返回属性。
    * `Writable`表示能否修改属性的值
    * `Value`包含这个属性的数据值

修改属性默认的特性，必须使用`Object.defineProperty()`方法。
```
var person = new Object();
Object.defineProperty(person, 'age', {
    Vallue: '20'
})
```
* 访问器属性
    * `Configurable`表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
    * `Enumerable`表示能否通过`for-in`循环返回属性
    * `Get`在读取属性时调用的函数。
    * `Set`在写入属性时调用的函数。

```
var person = {
    _year: 2019    //_（下划线）是一种记号，表示只能通过对象访问的属性。
}
Object.defineProperty(person, 'year', {
            get: function() {
                return this._year
            },
            set: function(newValue) {
                if(newValue > 2019) {
                    this._year = newValue;
                    this.edition += newValue - 2019;
                } 
            }
        });
person.year = 2029
console.log(person)
```
3. `Object.defineProperties()`方法可以一次定义多个属性。
4. `Object.getOwnPropertyDescriptor()`方法可以取得给定属性的描述符。
5. `isPrototypeof()`方法判断对象之前是否存在关系。
6. `Object.getPrototypeOf()`方法返回Prototype的值。
7. `HasOwnProperty()`方法可以判断属性是否来自于实例。
8. `Object.keys()`方法返回一个包含所有可枚举属性的字符串数组。
9. `Object.getOwnPropertyNames()`无论是否可枚举的属性都被返回。
10. ECMAScript支持面向对象编程，可以采用下列模式创建对象
* 工厂模式
* 构造函数模式
* 原型模式
11. JavaScript主要通过原型链实现继承。

#### 第七章
1. 闭包是指有权访问另一个函数作用域中的变量的函数。创建闭包的常见方式，就是在一个函数内部创建另一个函数。
2. this对象是在运行时基于函数的执行环境绑定的。在全局环境中，this等于window，而当函数被作为某个对象的方法调用时，this等于那个对象。
3. 可以通过`call()`和`apply()`改变函数的执行环境。
4. 每个函数在被调用时都会自动取得两个特殊的变量：this和arguments。内部函数在搜索这两个变量时，只会搜索到其活动对象为止，因此永远也不可能`直接访问`外部函数中的这两个变量。
5. 内存泄漏。如果闭包的作用域链中保存着一个HTML元素，那么就意味着该元素将无法被销毁。可以手动把引用的变量设置为null。
6. 初始化未经声明的变量，总是会创建一个全局变量。

#### 第八章 BOM
1. 全局变量不能通过delete操作符删除，而直接在window对象上定义的属性可以被删除。
2. 表示窗口相对于屏幕左边和上边的位置。
* screenLeft/screenX
* screenTop/screenY
```
let leftPos = (typeof window.screenLeft == "number") ? window.screenLeft : window.screenX;

let topPos = (typeof window.screenTop == "number") ? window.screenTop : window.screenY;
```
3. window.moveTo(x, y)/window.moveBy(x, y) 可以对窗口进行移动。
4. document.documenElement.clientWidth/document.documentElement.clientHeight 可以取得页面视口的信息。
5. 对于移动设备，window.innerWidth/window.innerHeight保存着可见视口，也就是屏幕上可见页面的大小。
6. window.resizeTo(x, y)/window.resizeBy(x, y)调整窗口的大小。
7. `window.open()`可以打开一个特定的URL。接收四个参数：
* 要加载的RUL
* 窗口目标
* 一个特性字符串
* 表示新页面是否取代浏览器历史记录中当前加载页面的布尔值
8. window.close()可以关闭新打开的窗口。
9. `setTimeout()/setInterval()`定时器。第二个参数为指定的时间，因为js是单线程语言，所以经过该时间后指定的代码不一定会执行。JavaScript有一个任务队列，这些任务队列会按照他们添加到队列的顺序执行。第二个参数就是告诉过多长时间把当前任务添加到队列中。如果队列是空的，那么添加的代码会立即执行；如果队列不是空的，那么就会等前面的代码执行完了之后才会执行。
10. `clearTimeout()/clearInterval()`清除定时器。
```
var h = setTimeout(function() {
    console.log(1)
}, 2000)

clearTimeout(h)
```
11. 系统对话框
* alert()显示确定按钮
* confirm()显示一个确定和取消按钮。点击确定返回true，点击取消和x返回flase。这种模式经常在用户想要执行删除操作的时候使用。
* prompt()显示输入框
12. 
|属性名|例子|说明|
|:--|:--|:--:|
|hash|"#contents"|返回URL中的hash|
|host|"www.wrox.com:80"|返回服务器名称和端口号|
|href|"http://www.wrox.com|返回当前加载页面的完整url。而location对象的toString()方法也返回这个值|
|pathname|"/WileyCDA"|返回url中的目录和（或）文件名|
|port|"8080"|返回url中指定的端口号|
|protocol|"http:"|返回页面使用的协议|
|search|"?q=javascript"|返回url的查询字符串|

13. 返回url中的参数
```
function getQueryStringArgs() {
            //取得查询字符串并去掉开头的问号
            var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
            //保存数据的对象
            args = [],
            
            //取得每一项
            items = qs.length ? qs.split("&") : [],
            item = null,
            name = null,
            value = null,
            i = 0,
            len = items.length;

            for(i=0;i<len;i++) {
                item = items[i].split("=");
                name = decodeURLComponent(item[0]);
                value = decodeURLComponent(item[1]);

                if(name.length) {
                    args[name] = value;
                }
            }
            return args;
        }

        //使用
        var args = getQueryStringArgs();
        console.log(args["a"]);
```
14. window.assign()可以立即打开一个新的URL。
15. 通过这几个方法修改url会在浏览器的历史记录里生成一条记录，因此用户通过单击*后退*按钮都会导航到前一个页面。使用`replace()`方法可以阻止这种行为，不会再历史记录里生成新记录。**调用replace方法后，用户不能回到前一个页面。**
16. `window.reload()`方法是重新加载当前显示的页面。如果页面自上次请求以来并没有改变过，页面就会从浏览器缓存中重新加载。如果想要强制从服务器重新加载，则需要这样定义`window.reload(true)`。
17. history对象保存着用户上网的历史记录。
18. 使用`go()`方法可以在用户的历史记录中任意跳转。
```
history.go(-1)
history.go(2)
history.go(1)
```
19. back()/forward()方法可以实现后退和前进。
20. `history.length == 0` 可以测试用户是否一开始就打开了你的页面。

#### 第十章 DOM
1. nodeName保存的是元素的标签名
```
if(xxx.nodeType == 1 ) {
    let value = xxx.nodeName
}
//如果xxx是元素的话，把标签名赋值给value
```
2. 通过节点的previousSibling和nextSibling属性可以访问同一列表中的其他节点。
* 列表中第一节点的previousSibling的属性值为null（因为本身是第一个节点，没有在上一个节点）
* 列表中最后一个节点的nextSibling的属性值同样为null（因为是最后一个节点，并没有在下一个节点了）。
```
if(somenode.nextSibling === null) {
    //说明是最后一个节点
    //任何操作
} else if (somenode.previousSibling === null) {
    //说明是第一个节点
    //任何操作
}
```
3. 父节点(parentNode)的firstChild/lastChild分别指向childNodes的第一个和最后一个节点。
* firstChild == somenode.childNodes[0]
* lastChild == somenode.childNodes[somenode.childNodes.length-1]
4. `hasChildNodes()`方法在节点包含一个或多个子节点的情况下返回true
5. `appendChild()`方法用于向childNodes()列表的末尾添加一个节点。
6. `insertBefore()`方法用于把节点放到指定位置。接收两个参数，第一个是要插入的节点，第二个是位置。
```
somenode.insertBefore(newnode, somenode.firstChild)
```
7. `replaceChild()`方法可以替换节点。接收两个参数，第一个是要插入的节点，第二个是要替换的节点。
8. `removeChild()`方法可以移除节点。
9. documentElement属性始终指向html元素。
10. document.body属性指向body
11. document.title获取文档的标题
12. namedItem()可以通过元素的name属性取得集合中的项
13. 在radio中，为了确保发送给浏览器的值正确，需要radio设置相同的name。使用document.getElementsByName()可以获取。
14. 集合API
* `document.anchors`包含文档中所有带name特性的<a>元素
* `document.forms`包含文档中所有的<form>元素
* `document.images`包含文档中所有的<img>元素
* `document.links`包含文档中所有带href的<a>元素
15. `window.onload`在页面完全加载之后延迟执行函数。
16. `element.tagName()`/`element.nodeName`可以获取元素的标签名。但是返回的是大写的标签名，所以最好需要转为小写：element.tagName.toLowerCase()
17. `div.className`包含了元素的类名。
18. `getAttribute()`返回元素的信息。