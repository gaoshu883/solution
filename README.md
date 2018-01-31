# solution
there is a collection of solving problems

## 一组对象去重
输入：
```Javascript
let arr = [{
  name: '111',
  value: 'hello'
}, {
  name: '222',
  value: 'world'
}, {
  name: '111',
  value: 'hello'
}];
console.log(removeDuplicateObject(arr));
```
输出：
```Javascript
[{name: '111',value: 'hello'}, {name: '222',value: 'world'}];
```
一组对象去重`removeDuplicateObject`方法的一种实现
```Javascript
function removeDuplicateObject (arr) {
  let temp = arr.map((item) => {
    return JSON.stringify(item);
  });
  temp = Array.from(new Set(temp));
  return temp.map((item) => {
    return JSON.parse(item);
  });
}
```
