# 代码小仓库

## Array

- [最大值-最小值](#最大值-最小值)
- [排序](#排序)




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
