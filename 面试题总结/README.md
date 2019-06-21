# CSS面试题
#### 阐述清除浮动的几种方式
1. 父级DIV定义`height`。
    * 原理：父级`div`手动定义`height`，就解决了父级`div`无法自动获取高度的问题。
    * 优点：简单、代码少、容易掌握。
    * 缺点：只适合固定高度的布局，要给出精确高度，如果高度和父级`div`不一样时，会产生问题。
2. 在浮动元素后面添加空`div`标签：**`clear:both`**
    * 原理：添加一个空`div`,利用css提供的`clear:both`清除浮动，让父级`div`能够自动获取到高度。
    * 优点：简单、代码少、**浏览器支持好**、不容易出现怪问题
3. 在浮动元素后面添加`<br clear="all">`
    * 优点：比空标签语义稍强，代码量较少。
    * 缺点：同样有违结构与表现的分离，不推荐使用。
4. 父级`div`定义`overflow: hidden`
    * 原理：必须定义`width`，同时不能定义`height`,使用时，浏览器会自动检查浮动区域的高度。
    * 优点：简单、代码少、浏览器支持好。
5. 通过给父级元素添加`::after`伪元素。
    * 原理：通过块级元素的换行属性。
    ```
    .container::after {
        content: "";
        display: block/table;
        clear: both;
    }
    ```
---
#### css选择器有哪些？选择器的权重优先级？
##### 选择器类型
|名字|代码|
|:-|:-:|
|ID|#id|
|class|.class|
|标签|P|
|通用|*|
|属性|[type="text"]|
|伪类|:hover|
|伪元素|::first-line|
|子选择器、相邻选择器||
#### 权重计算规则
|等级|名字|权值|
|:-|:-:|:-:|
|第一等|内联样式，如:style=""|1000|
|第二等|ID选择器，如:#content|100|
|第三等|类选择器，如:.content|10|
|第四等|类型选择器和伪元素选择器,如: div/p|1|
|第五等|通配符、子选择器、相邻选择器等,如:*>+|0|
||继承的样式没有权值||
* `!important`表示强制应用该样式，例如：`button{ width: 150px !important;}`，与以上的选择器相遇时，强制使用此样式;
* 如果比较后权重相同，那么后者覆盖前者，后渲染的胜出；
* 内联样式  > id选择器样式 > 类选择器样式 > 元素选择器样式；
* CSS选择器的使用，应该尽量避免使用 !important 和 内联样式；id通常也是与class区分开使用，前者多用于JS中的结点定位，后者多用于CSS选择器。
* 重中之重，1000/100/10/1这种权值系数的比较方式只是便于理解，真实情况下10个class并不能逆转1个id。

#### CSS样式覆盖规则
* 由于继承而发生样式冲突时，最近祖先获胜。
* 继承的样式和直接指定的样式冲突时，直接指定的样式获胜。
* 直接指定的样式发生冲突时，样式权值高获胜。
* 样式权值相同时，后者获胜。
* `!important`的样式属性不被覆盖。
---
#### display: none visibility hidden 区别？
* `display: none`彻底消失，不在文档流中占位，浏览器也不会解析该元素。
* `visibility: hidden`是视觉上消失了，可以理解为透明度为0的效果，在文档流中占位。
---
使用`visibility: hidden`比`display: none`**性能上要好**，`display: none`切换显示时，页面**产生回流**，（当页面中的一部分元素需要改变规模尺寸、布局、显示隐藏等，页面重新构建，此时就是回流。所有页面第一次加载时需要产生一次回流），而`visibility`切换是否显示时则**不会引起回流**。



# JS面试题
#### document load和document ready的区别
* load 是当页面所有资源加载后（包括图片、CSS文件、JS文件等）,如果图片资源较多，加载时间较长，onload后等待执行的函数需要等待较长时间。
* ready（jquery）是当DOM文档树加载完成后执行函数，所以会**比load较快的执行**。
---
#### == 和 === 的区别
* `==` 操作符会先转换操作数，然后再比较它们的相等性；
* `===` 操作符在比较之前不会转换操作数。
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
```
var arr = [1, 2, 4, 5, 6, 3, 5, 3, 2, 100,205];
        var item = [];
        function sortArr(a, b) {
            return a-b
        }
        console.log(arr.sort(sortArr));
```
---
#### document.write和innerHTML的区别：
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
* 把字符串参数解析成JS代码并运行，返回执行的结果。
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
