 # 正则表达式笔记
 ### 第二章
 1. 正则表达式被简称为模式，他们是有一些字符构成的字符串。这些字符可以是**普通字符和元字符**。
 2. 通过元字符`.`可以匹配除了换行符以外的任意字符。
 ```
let reg = /a.c/;
let str = "abc";
console.log(reg.test(str))  //true
```
### 第三章
1. 使用`[]`来匹配字符集合。
```
let reg = /[ns]a/;
let str = "na";
let str2 = "sa";
console.log(reg.test(str))  //true
console.log(reg.test(str2))  //true

```
2. 验证某个模式能不能获取预期的匹配结果并不难，但**验证它不会匹配到你不想要的东西可就没那么困难了。**：我只想匹配`na或者sa`
```
let reg = /[ns]a/;
let str = "cna";
console.log(reg.test(str))  //true

```
3. `[0-9]`能够匹配`0123456789`
也就是说`/[0-9]/`与`/[0123456789]/`等价

其他的还有`/[A-Z]/`/ `/[a-z]/`等

**在实际工作中，最常用的字符区间还是数字字符区间和字母字符区间**
4. `^`元字符，本意是匹配以^开头的字符
```
let reg = /^[0-9]/;
let str = "1n";
console.log(reg.test(str))  //true
```
但是放在`[]`集合里，意思为**取反**。[^x]	匹配除了x以外的任意字符
```
let reg = /[^0-9]/;
let str = "1n";
console.log(reg.test(str))  //true

let reg = /[^0-9]/;
let str = "1";
console.log(reg.test(str))  //false
```
5. 元字符`[]`用来定义一个集合，含义是必须匹配这个集合里面的**任意**字符之一。
6. 在`[]`集合里面放入`^`意为取非。这将把给定的字符集合排除在外。

 `/[^0-9]/`的意思为，除了0到9之外的都将匹配

### 第四章
1. 字符类代表匹配某一类别的字符
* 数字类别

|元字符|说  明|
|:--|--|
|\d|任何一个数字字符(等价于[0-9])|
|\D|任何一个非数字字符(等价于[^0-9])|
```
let reg = /marry\[[\d][\d]\]/;
let str = "marry[10]";
let result = reg.test(str);
console.log(result);          // true


let reg = /marry\[[\d][\D]\]/;
let str = "marry[10]";
let result = reg.test(str);
console.log(result);          // false
 

let reg = /marry\[[\D][\D]\]/;
let str = "marry[ab]";
let result = reg.test(str);
console.log(result);          // true
```
* 字母数字类别

|元字符|说  明|
|:--|--|
|\w|任何一个字母和数字字符(大小写均可)或下划线字符(等价于[a-zA-Z0-9_])|
|\W|任何一个非字母和数字字符或非下划线(等价于[^a-zA-Z0-9_])|
* 空白字符

|元字符|说  明|
|:--|--|
|\s|任何一个空白字符（等价于[\f\n\r\t\v]）|
|\S|任何一个非空白字符（等价于[^\f\n\r\t\v]）|
