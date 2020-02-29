# JS面试题
#### document load和document ready的区别
* load 是当页面所有资源加载后（包括图片、CSS文件、JS文件等）,如果图片资源较多，加载时间较长，onload后等待执行的函数需要等待较长时间。
* ready（jquery）是当DOM文档树加载完成后执行函数，所以会**比load较快的执行**。
---
#### == 和 === 的区别
* `==`称作**相等运算符**,用来比较两个操作数是否相等。操作符会先转换操作数，然后再比较它们的相等性；
* `===`称作**严格相等运算符**，操作符在比较之前不会转换操作数。如果类型不一样，就会返回`false`。
---
#### Javascript语言里的对象可以分为三种类型
* 用户定义对象：由程序员自行创建的对象
* 内建对象：内建在JS语言里的对象，如`Array、Math、和date等`
* 宿主对象： 由浏览器提供的对象
---
#### 三种DOM方法获取元素节点
* 通过元素ID `getElementById`
* 通过标签名字 `getElementsByTagName`
* 通过类名 `getElementsByClassName`
---
#### nodeType属性总共有12种可取值。其中三种具有使用价值：
* 元素节点的nodeType属性值是1
* 属性节点的nodeType属性值是2
* 文本节点的nodeType属性值是3
---
#### Javascript中的定时器有哪些? 他们的区别及用法是什么？
* `setTimeout()`  只会执行一次
* `setInterval()`  会一直重复执行
---
#### 如何用原生JS给一个按钮绑定两个onclick事件
```
var btn4 = document.getElementById("btn4");
btn4.addEventListener("click",hello1);
btn4.addEventListener("click",hello2);
function hello1(){
     alert("hello 1");
}
function hello2(){
     alert("hello 2");
}
```
---
#### 数组去重
* 利用`indexOf()`的特性，如果要检索的字符串值没有出现，则该方法返回-1。
```
var arr = [1, 2, 4, 5, 6, 3, 5, 3, 2];
var item = [];
for(var i=0;i<arr.length;i++) {
    if(item.indexOf(arr[i]) == -1) {
        item.push(arr[i]);
    }
}
console.log(item);
```
---
#### 数组排序
* 因为`sort()`方法默认使用字符编码的顺序进行排序。所以需要使用一个函数来帮助排序。若a 小于 b，返回一个小于0的值，a在b前面。
```
var arr = [1, 2, 4, 5, 6, 3, 5, 3, 2, 100,205];
    function sortArr(a, b) {
        return a-b
    }
    console.log(arr.sort(sortArr));
```
---
#### document.write和innerHTML的区别：

* `document.write()`会直接将内容写入页面的内容流中，会导致页面全部重绘
* `innerHTML`将内容写入某个DOM节点，不会导致页面全部重绘。
---

#### xml和json的区别，请用四个词语来形容
* JSON相对于XML来讲，数据的体积小，传递的速度更快些
* JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互
* XML对数据描述性比较好；
* JSON的速度要远远快于XML
---
#### JS中有哪几种数据类型
* `Undefined、Null、Boolean、Number、String`。
* 还有一种复杂数据类型 `Object`,`Object`本质上是由一组无序的名值对组成的。
---
#### undefined和null的区别
* `undefined`：在使用var声明变量但未对其加以初始化时，这个变量的值就是`underfined`。
* `null`：表示一个空对象指针。使用`typeof`操作符 会得到`object`。
* `null == undefined`进行比较会返回`true`。尽管有这样的关系，但他们的用途完全不同。任何情况下都没有必要把一个变量的值设置为`undefined`。可是`null`却相反，只要保存对象的变量还没有真正的保存对象，就应该明确的让该变量保存`null`值。这样可以有利于区分`null`和`undefined`
---
#### eval() 的作用
* 把**字符串**参数解析成**JS代码**并运行，返回执行的结果。
---
#### 什么是内存泄漏
* 内存泄漏是指一块被分配的内存既不能被使用，也不能被回收。
* 清空内存通常有两种形式，即标记清除和引用计数。通常**标记清除**的使用**较为广泛**。
---
#### JS的那些操作会造成内存泄漏
* 意外的全局变量引起的内存泄漏
* 闭包引起的内存泄漏
* 没有清理的DOM元素引用
* 被遗忘的定时器或者回调
* 子元素存在引用引起的内存泄漏
---
#### 怎样添加、移除、移动、复制、创建和查找节点？
* 创建新节点
    * `createDocumentFragment()` //创建一个DOM片段
    * `createElement()` //创建一个具体的元素
    * `createTextNode()` //创建一个文本节点
* 添加、移除、替换、插入
    * `appendChild()` //添加
    * `removeChild()` //移除
    * `replaceChild()` //替换
    * `insertBefore()` //插入
* 查找
    * `getElementsByTagName()` //通过标签名称
    * `getELementByName()`//通过元素的Name属性的值
    * `getElementById()`//通过元素Id，唯一性
---
#### 计算一个数组的和
* 方法一：
```
var arr = [1, 2, 3, 4, 5, 6];
var item = 0;
for(var i=0;i<arr.length;i++) {
    item+=arr[i];
}
console.log(item);
```
* 方法二：
```
var btn = document.getElementById("btn4");
    var arr = [1, 45, 3, 54, 25, 3]
    var item = 0;
        function add(num) {
            for(var i=0;i<num.length;i++) {
                item+=num[i];
            }
            console.log(item);
        }
        add(arr)
```
---
#### 事件绑定的方式
* 嵌入dom
```
<button onclick="func()"></button>
```
* 直接绑定
```
btn.onclick = function() {}
```
* 监听事件
```
btn.addEventListener('click',function(){})
```
---
#### 有一个函数，参数是一个函数，返回值也是一个函数，返回的函数功能和入参的函数相似，但这个函数只能执行3次，再次执行无效，如何实现？
这个题目考察闭包的使用。最后结果只能执行三次。
```
function sayHi() {
    console.log("hi!")
}
function threeTime(fn) {
    let items = 0;
    return () => {
        if(items++ < 3) {
            fn();
        }   
    }
}

const newFn = threeTime(sayHi);
newFn();
newFn();
newFn();
newFn();
newFn();
```

#### 使用原生JS，动态的改变元素文字颜色和背景色，并在一定时间后停止
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #box {
            width: 200px;
            height: 200px;
            color: yellow;
            background-color: #ff0000;
        }
    </style>
</head>
<body>
    <div id="box">
        <p id="text">Hello World</p>
    </div>
    <script>    
        var box = document.getElementById('box');
        //这里执行对元素文字和背景的转换
        function active () {
            var textColor = getStyle(box, 'color');
            var textBg = getStyle(box, 'backgroundColor');
            console.log(textColor);
            console.log(textBg);
            
            box.style.color = textBg;
            box.style.backgroundColor = textColor;
        }
        //把定时器赋值给h
        var h = setInterval(active, 2000);
        //在5秒之后执行操作
        setTimeout((function() {
            //清除定时器
            clearInterval(h)
        }), 5000);


        //获取元素样式
        function getStyle(obj, attr) {
            if(window.getComputedStyle) {
                return getComputedStyle(obj)[attr];
            }else {
                return obj.currentStyle[attr];
            }
        };    
    </script>
</body>
</html>
```
