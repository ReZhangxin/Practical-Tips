# 代码小仓库

## Array

- [最大值-最小值](#最大值-最小值)
- [排序](#排序)
- [扁平化](#扁平化)
- [数组去重](#数组去重)



## Array

### 最大值-最小值

```js
maxData: function (arr) {
//   return Math.max.apply(null, arr)
  return Math.max(...arr)
}
minData: function (arr) {
//   return Math.min.apply(null, arr);
  return Math.min(...arr)
}
```

[↑返回top](#代码小仓库)

### 排序

```js
const prices = [
    {name:'php',price:199},
    {name:'java',price:499},
    {name:'c++',price:399},
    {name:'javascript',price:666}
]
//数组对象方法排序:
function sortByKey(array,key) {
  return array.sort(function(a,b){
      var x=a[key];
      var y=b[key];
      return ((x<y)?-1:((x>y)?1:0));
  });
}
console.log(sortByKey(prices,'price'))
```

[↑返回top](#代码小仓库)

## 扁平化

```js
// 方法 1
let num = [1, [2, [3, 4]]];

function flatten(arr) {
    let result = [];
    for (let i = 0, len = arr.length; i < len; i++) {
        // Array.isArray()用于确定传递的值是否是一个 Array
        if (Array.isArray(arr[i])) {
        // concat()方法用于合并两个或多个数组。
        // 此方法不会更改现有数组，而是返回一个新数组。
            result = result.concat(flatten(arr[i]))
        }
        else {
            result.push(arr[i])
        }
    }
    return result;
}

console.log(flatten(num))   // [1, 2, 3, 4]
```

[↑返回top](#代码小仓库)

## 数组去重

```js
var array = [1, 2, 1, 1, '1'];

var unique = (a) => [...new Set(a)]

console.log(unique(array)); // [1, 2, "1"]
```

[↑返回top](#代码小仓库)
