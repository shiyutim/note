 # 正则表达式笔记
 #### 第二章
 1. 正则表达式被简称为模式，他们是有一些字符构成的字符串。这些字符可以是**普通字符和元字符**。
 2. 通过元字符`.`可以匹配除了换行符以外的任意字符。
 ```
let reg = /a.c/;
let str = "abc";
console.log(reg.test(str))  //true
```
#### 第三章
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
 
 #### 第四章
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

#### 第五章
|元字符|说    明|
|:--|--|
|+|匹配1个或多个字符|
该元字符能够匹配最少一个，最多N个字符。
如果要匹配邮箱，就需要使用+。如下：
```
let reg = /\w+@\w+\.\w+/;
let str = "text@test.com"
let result = reg.test(str);
console.log(result);     //true
```
这样可以简单的匹配一个常见邮箱。，如果繁琐点，可以如下设置：
```
let reg = /[\w\.]+@[\w\.]+\.\w+/
```
这样设置可以多匹配几个.来控制地址。
##### *匹配0个或多个字符
|元字符|说    明|
|:--|--|
|*|匹配0个或多个字符|
```
let reg = /\w+[\w\.]*@[\w\.]+\.\w+/
let str = "text@test.com"
let result = reg.test(str);
console.log(result);     //true
```
相比上面开头少了匹配`.`和后面添加了一个`[\w\.]*`，这样设置可以控制`text.`后面和`@`前面这段是否出现。**因为使用`*`可以匹配0个或者多个。**

---
\*与-的区别是：+匹配一个或多个字符，最少要匹配一次；*匹配零个或任意多个字符，可以没有匹配。

---
##### ?匹配0次或1次
|元字符|说    明|
|:--|--|
|?|匹配0次或1次|
比如：
```
let reg = /http://[\w./]+/
let str = "https://www.baidu.com"
let result = reg.test(str);
console.log(result);     //false

如上只能匹配http大头的，如果想要匹配https，可以这样设置

let reg = /https?://[\w./]+/
```

---
##### 设定一个精确的值
如上几个元字符`*+`能够匹配一些不确定的字符，我们没法精确控制个数。
那么使用`{}`可以精确的控制个数
|元字符|说    明|
|:--|--|
|{}|精确的控制个数|
```
let reg = /\w{5}.\w{3}/
let str = "baidu.com"
let result = reg.test(str);
console.log(result);     //true
```

##### 为重复匹配设定一个区间
也就是说，在`{}`这样的基础上，填入几就是控制几个字符。如果填入`{2,5}`这样的话，就是最少出现2次，最多出现5次。

##### 最少匹配几次，或多次
`{3, }`这样设置就是最少出现3次，或多次。

#### 第六章
|元字符|说    明|
|:--|--|
|\b|用来规定边界|
```
let reg = /cat/
let str = "cat cation"
let result = reg.test(str);
console.log(result);     //true
```
如上代码想要匹配cat这个单词，但是例子中两个都能够匹配上。所以想要单独只匹配cat的话，需要使用边界符
```
let reg = /\bcat\b/
let str = "cat cation"
let result = reg.test(str);
console.log(result);     //true
```
另外两个常用的匹配边界`^ and $`

`^`匹配字符串的开头，如：
```
let reg = /^\d/
let str1 = "1234"
let str2 = "a1234"

let result1 = reg.test(str1);
let result2 = reg.test(str2);

console.log(result1)  // true
console.log(result2)  // false
```

相应的，$匹配字符串的结尾。如：
```
//我们把字母换个位置

let reg = /\d$/
let str1 = "1234"
let str2 = "1234a"

let result1 = reg.test(str1);
let result2 = reg.test(str2);

console.log(result1)  // true
console.log(result2)  // false
```

#### 第七章
1. `|`表示或，如：
```
let reg = /19|20/;
let str = "2019";
let result = reg.test(str);
console.log(result); // true

//把2019换成1937，同样返回true

let reg = /19|20/;
let str = "1937";
let result = reg.test(str);
console.log(result); // true
```
2. `()`代表子表达式，就是匹配一个模式。如：
```
let str = "[12.159.46.200]";
let reg = /\d{1,2}\.1\d{2}\.\d{2}\.\d{3}/;
let result = reg.test(str);
console.log(result); // true
```
以上正则表达式为匹配一串IP地址，可以看出有几个重复的地方，就是`xx.`，一共重复出现了三次，所以可以使用`()`来定义一个子表达式，然后定义`{3}`，表示重复三次，如：
```
let str = "[12.159.46.200]";
let reg = /(\d{1,3}\.){3}\d{1,3}/;
let result = reg.test(str);
console.log(result); // true
```
这回使用了`(\d{1,3}\.)`来定义一个子表达式，然后`{3}`表示重复出现3次，来匹配`xx.`或者`xxx.`；最后一个`\d{1,3}`定义最后出现的地址

但是这个还不够严谨，可以定义一些规则来匹配ID地址，如书中所说：
* 任何一个位或2位数字
* 任何一个以1开头的3位数字
* 任何一个以2开头/第二位数字在0~4之间的3位数字
* 任何一个以25开头/第三位数字在0~5之间的3位数字
```
let str = "[12.159.46.200]";
let reg = /(((\d{1,2})|(1\d{2})|(2[0-4]\d)|(25[0-5]))\.){3}((\d{1,2})|(1\d{2})|(2[0-4]\d)|(25[0-5]))/;
let result = reg.test(str);
console.log(result); // true
```

以上的正则表达式需要拆开来看，就比较方便看了。

#### 使用`exec()`有点问题。

####  第八章
1. 回溯引用指的是模式的后半部分引用在前半部分中定义的值表达式。`\1`代表第一个子表达式`\2`代表第二个子表达式。
2. 回溯引用和`()`配合使用。
3. `\0`代表整个正则表达式
##### 在JacaScript里面，需要使用$来替换`\`


#### 第九章
1. 向前查找，意思就是匹配它，但不包含它。表达式为`(?=xxx)`
举个例子：
```
let reg1 = /.+(?=:)/;
let reg2 = /.+(:)/;
let str = "https://";
let result1 = reg1.exec(str);    // https
let result2 = reg2.exec(str);    // https:
```
2. 向前查找指定了一个必须匹配但不在结果中返回的模式。


## String方法：
|方法|描述|
|:--|:--|
|search|检索指定的字符串，返回所在位置的数字。如果没有找到任何匹配，则返回-1|
```
let reg = /\d/
let str = "abc1"
let result = str.search(reg)  // 3
```
|方法|描述|
|:--|:--|
|match|检索字符串内指定的值。返回的是指定的值|
```
let reg = /\d/
let str = "a1b2c3"
let result = str.match(reg)  // 1

//加上g全局搜索
let reg = /\d/g
let str = "a1b2c3"
let result = str.match(reg)  // "1" "2" "3"
```

|方法|描述|
|:--|:--|
|replace|用于替换指定的字符串|
```
let reg = /\d/
let str = "a1b2c3"
let result = str.match(reg, ",")  // a,b2c3

//如果没加g，会只匹配第一个，加上之后
let reg = /\d/g
let str = "a1b2c3"
let result = str.match(reg, ",")  // a,b,c,
```
|方法|描述|
|:--|:--|
|split|用于把字符串分割成字符串数组|
```
let str = "hello"
let result = str.split("")  // ["h", "e", "l", "l", "o"]

let str = "hello"
let result = str.split("", 3) // ["h", "e", "l"]
```

## RegExp方法
|方法|描述|
|:--|:--|
|exec|检索指定的值，并返回找到的值|
```
let reg = /\d/
let str = "hello5"
let result = reg.exec(str)  // 5 
```

|方法|描述|
|:--|:--|
|test|检索指定的值是否匹配某个模式|
```
let reg = /\d/
let str = "hello5"
let result = reg.test(str) // true

let reg = /\d/
let str = "hello"
let result = reg.test(str) // false
```

String方法就是str在前，也就是str.xxx(reg)  xxx是方法

RegExp方法就是reg在前，也就是reg.xxx(str)  xxx是方法