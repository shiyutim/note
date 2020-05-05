# JavaScript 常用函数


## 获取地址栏指定的参数

```js
function getQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return unescape(r[2]); return null;
}
```

## 返回指定范围内的值

```js
function roundNum(smlNum, larNum) {
    return Math.round((larNum - smlNum) * Math.random() + smlNum)
}
```

## 深拷贝

```js
const assign = (newVal, oldVal) => {
    for(let k in oldVal) {
        let item = oldVal[k]

        if(item instanceof Array) {   // Array的判断必须在Object的前面，因为Array instance Object 为true
            newVal[k] = []                    
            assign(newVal[k], item)
        } else if (item instanceof Object) {
            newVal[k] = {}
            assign(newVal[k], item)
        } else {
            newVal[k] = item
        }
    }
}
```

## 比较两个数的大小

```js
/*
* 升序
*/
function compare(a, b) {
    return a - b
}
arr.sort(compare)

/*
* 降序
*/

function compare(a, b) {
    return b - a
}
arr.sort(compare)

/*
* 比较对象中的值
*/ 

function compare(propertyName) {
    return function(a, b) {
        let value1 = a[propertyName]
        let value2 = b[propertyName]
        return value1 - value2
    }
}
```



## 加密字符串

```javascript

const encode = str => btoa(encodeURIComponent(str))


const decode = str => decodeURIComponent(atob(str))


let code = encode('My name is shiyutim')
let result = decode(code)
```



## 判断值的类型

```js
function estimateType(value){
    return Object.prototype.toString.call(value).replace(/^.{8}(.+)]$/, (m,$1)=> $1.toLowerCase());
}

// toString.call([]) "[object Array]" 截取后面的值即可
// 其他同理

```

## 数组去重（包含多维数组）

```js
let result = []
/**
*  @arr 要去重的数组
*  @target 接收去重后的数组
*/
function  uniqueArr(arr, target) {
    if(!target) return
    if(!(arr instanceof Array)) return
	
    // 写法一
    arr.forEach(i => {

        if(Array.isArray(i)) {
            return uniqueArr(i, target)
        }

        if(!target.includes(i)) {
            target.push(i)
        }
    })
    
    // 写法二
    //    arr.forEach(i => Array.isArray(i) ? uniqueArr(i, target) : target.includes(i) ? '' : target.push(i))
}

uniqueArr([1, 2, 3, [1, 2, 3, [324, 234, 13]] ,[1, 2 ,3, 9, 8]], result)
```

