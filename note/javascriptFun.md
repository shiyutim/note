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