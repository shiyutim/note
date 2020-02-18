# 算法

## 冒泡排序

冒泡排序比较所有相邻的两个项，如果第一个比第二个大，则交换他们。元素项向上移动至正确的顺序，就好像气泡升至表面一样，冒泡排序因此得名。

> 两两相比，从头遍历至结尾

```javascript
const compare = (array: number[]) => {
  for (let i = 0, l = arr.length; i < l; i++) {
    for (let j = 0, l = arr.length; j < l - 1; j++) {
      if (array[j] > array[j + 1]) {
        swap(arr, j, j + 1)
      }
    }
  }
}

const swap = (array: number[], a: number, b: number) => {
  [array[a], array[b]] = [array[b], array[a]]
}
```

## 快速排序

选择排序算法是一种原址比较排序算法。选择排序大致的思路是找到数据结构中的最小值并将其放在第一位，接着找到第二小的值并将其放在第二位，以此类推。

> 就是遍历每一项，找到最小值的`index`后，在依次调换位置。

```js
const compare = (array: number[]) => {
  const { length } = array

  let indexMin

  for (let i = 0; i < length - 1; i++) {
    indexMin = i
    for (let j = i; j < length; j++) {
      if (array[indexMin] > arr[j]) {
        indexMin = j
      }
    }

    if (i !== indexMin) {
      [array[i], arr[indexMin]] = [array[indexMin], array[i]]
    }
  }

  return array
}
```

## 插入排序
插入排序每次排一个数组项，以此方式构建最后的排序数组。假定第一项已经排序了。接着，他和第二项进行比较——第二项应该是待在原位还是插到第一项之前呢？这样，头两项就已经正确排序，接着和第三项比较（它是该插入到第一、第二还是第三的位置？），以此类推。

```js

const compare = (array: number[]) => {
  let temp
  for (let i = 1; i < array.length; i++) {
    let j = i
    temp = array[i]
    while (array[j - 1] > temp) {
      array[j] = array[j - 1]
      j--
    }
    array[j] = temp
  }
  return array
}
```