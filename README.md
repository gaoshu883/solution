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
## nwjs:node-remote配置

```JSON
  "node-remote": ["http://localhost"]
  "node-remote": ["<all_urls>"]
```
## 检测动态DOM元素成功插入文档

收集到两种思路：
+ 假设动态插入的DOM元素d1，利用document.body.contains(d1)进行存在性判断，如果包含，则说明已成功插入，如果不包含，延迟100ms继续判断，依此循环，具体参考：[https://stackoverflow.com/questions/220188/how-can-i-determine-if-a-dynamically-created-dom-element-has-been-added-to-the-d](https://stackoverflow.com/questions/220188/how-can-i-determine-if-a-dynamically-created-dom-element-has-been-added-to-the-d)
+ 利用CSS3动画特性，假设DOM元素d1，附带某种动画效果，则全局监听`animationstart`事件，利用`event.animationName`进行判断，具体内容参考：[I Want a DAMNodeInserted Event!](http://www.backalleycoder.com/2012/04/25/i-want-a-damnodeinserted/)

## AJAX请求返回302等错误码

出现这种情况，一般为post请求（需要身份认证），一种情形是：服务器判断用户身份失败，则重定向到登录页面。如果开发过程中的ajax请求出现这类错误，可以考虑以下几点：
+ 发送请求时的参数不全或错误，比如缺少cookie，content-type，referer等字段，post data错误等
+ 请求是否必须为post类型，个别情况下修改为get请求则成功（极端）

## 判断文本长度（汉字1，其他0.5）

当用户在文本框或文本域中进行输入操作的时候，往往需要进行文本字数统计，一些情况下要求啊、汉字算一个，英文或其他可输入符号两个算一个

```Javascript
function calcTextLen(msg) {
  let tempArr = [...msg];
  let pattern = /[\u4e00-\u9fa5]/;
  let len = 0; // 缓存总长
  tempArr.forEach(item => {
    if (pattern.test(item)) {
      len++;
    } else {
      len = len + 0.5;
    }
  });
  return Math.ceil(len);
}
```

## 解析url
```JavaScript
/* 
 * @param {string} url eg: http://www.lu3xiang.com?id=1&name=lucy
 * @returns eg: {id:'1', name: 'lucy'}
 */
function getRequest(url) {
  let theRequest = {};
  if (url.indexOf('?') != -1) {
    let str = url.substr(url.indexOf('?') + 1);
    let strs = str.split('&');
    for (var i = 0; i < strs.length; i++) {
      theRequest[strs[i].split('=')[0]] = unescape(strs[i].split('=')[1]);
    }
  }
  return theRequest;
}
```
