# javascript 忍者秘籍

## 第三章

1. 立即执行函数（IIFE）的几种写法：

```
// 1. 常用写法
(function() {})()

// 2. 不常用
(function() {}())

// 3. 在javascript库中会常见到。一元操作符也能告知js引擎处理的是表达式
+function() {}()
-function() {}()
!function() {}()
~function() {}()
```

2. IIFE 加上`()`因为 JavaScript 解释器必须能够轻易区分函数声明和函数表达式的区别。如果去掉包裹的`()`，JavaScript 开始解析时便会结束。因为函数需要函数名，没有函数名会报错。加上`()`指明正在处理一个函数表达式而不是语句。
