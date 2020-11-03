---
title: javascript-demo
date: 2020-09-13 14:56:02
tags:
  - javascript
  - demo
  - front-end
---

# javascript-demo

## 数组转换为带层级的数据

原数据

```js
var arr=[
    "root/",
    "root/a/",
    "root/a/new_b.png",
    "root/a/qa/",
    "root/a/qa/新建文本文档 (3).txt",
    "root/asdfasdfasdfasdfasdfasdfasdf.txt",
    "root/b.png",
    "root/instqj_gfzqhk.exe",
    "root/jupyter_notebook.png",
    "root/new_b.png",
    "root/output/new_b.png",
    "root/soffice.exe",
    "root/ti/asdfasdfasdfasdfasdfasdfasdf.txt",
    "root/watermark.zip",
    "root/中华人民共和国国民经济和社会发展 第十三个五年规划纲要 .pdf",
    "root/国务院发布《中国制造2025》%28全文%29.pdf",
    "root/新建文本文档 (3).txt",
    "root/新建文本文档.txt",
    "root/沧海一声笑.docx",
    "root/理光C2011SP.exe"
]
```



目标数据类型

```js
const treeData = [{
  title: '0-0',
  key: '0-0',
  children: [{
    title: '0-0-0',
    key: '0-0-0',
    children: [
      { title: '0-0-0-0', key: '0-0-0-0' },
      { title: '0-0-0-1', key: '0-0-0-1' },
      { title: '0-0-0-2', key: '0-0-0-2' },
    ],
  }];
```



```js
const pathToTree = (input) => {
  var output = [];
  for (var i = 0; i < input.length; i++) {
      var chain = input[i].split("/");
      var currentNode = output;
      for (var j = 0; j < chain.length; j++) {
          if (chain[j] === '') {
              break;
          }
          var wantedNode = chain[j];
          var lastNode = currentNode;
          for (var k = 0; k < currentNode.length; k++) {
              if (currentNode[k].title == wantedNode) {
                  currentNode = currentNode[k].children;
                  break;
              }
          }

          if (lastNode == currentNode) {
              var newNode = currentNode[k] = { key: input[i], title: wantedNode, children: [] };
              currentNode = newNode.children;
          } else {
              delete currentNode.children
          }
      }
  }
  return output;
}

var arr=[
  "root/",
  "root/a/",
  "root/a/new_b.png",
  "root/a/qa/",
  "root/a/qa/新建文本文档 (3).txt",
  "root/asdfasdfasdfasdfasdfasdfasdf.txt",
  "root/b.png",
  "root/instqj_gfzqhk.exe",
  "root/jupyter_notebook.png",
  "root/new_b.png",
  "root/output/new_b.png",
  "root/soffice.exe",
  "root/ti/asdfasdfasdfasdfasdfasdfasdf.txt",
  "root/watermark.zip",
  "root/中华人民共和国国民经济和社会发展 第十三个五年规划纲要 .pdf",
  "root/国务院发布《中国制造2025》%28全文%29.pdf",
  "root/新建文本文档 (3).txt",
  "root/新建文本文档.txt",
  "root/沧海一声笑.docx",
  "root/理光C2011SP.exe"
]

console.log(pathToTree(arr))
```



## 数组

### 数组扁平化

>  数组扁平化是指将一个多维数组变为一个一维数组

```JavaScript
const arr = [1, [2, [3, [4, 5]]], 6]; // => [1, 2, 3, 4, 5, 6]
```

#### flat()

> 会按照一个可指定的深度递归遍历数组, 并将所有元素于遍历到的子数组中的元素合并为一个型数组返回
>
> Array.prototype.flat([depth])
>
> - depth : 可选 默认1 (指定要提取嵌套数组的结构深度)
>   - Infinity : **可展开任意深度的嵌套数组**
> - 返回值 : 一个包含数组与值数组中的所有元素的新数组
>
> 

```javascript
const res = arr.flat(Infinity);
```

#### 堆栈stack



```js
 const flatten = (arr) => {
   const stack = [...arr];
   const res = [];
   while (stack.length) {
     const next = stack.pop();
     if (Array.isArray(next)) {
    	 stack.push(...next)
     } else {
     	res.push(next);
     }
   }
   res.reverse();
   return res;
 }
```





#### 正则

> 但数据类型都会变为字符串

```javascript
const res1 = JSON.stringify(arr).replace(/\[|\]/g, '').split(',');
const res2 = JSON.parse('[' + JSON.stringify(arr).replace(/\[|\]/g, '') + ']');
```



#### reduce

```javascript
const flatten = arr => {
  return arr.reduce((pre, cur) => {
    return pre.concat(Array.isArray(cur) ? flatten(cur) : cur);
  }, [])
}
const res = flatten(arr);
```

#### 函数递归

```javascript
const res = [];
const fn = arr => {
  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      fn(arr[i]);
    } else {
      res.push(arr[i]);
    }
  }
}
fn(arr);
```

### 数组去重

```javascript
const arr = [1, 1, '1', 17, true, true, false, false, 'true', 'a', {}, {}];
// => [1, '1', 17, true, false, 'true', 'a', {}, {}]
```

#### Set

```javascript
const res1 = Array.from(new Set(arr));
```

#### 两层for循环+splice

```javascript
const unique1 = arr => {
  let len = arr.length;
  for (let i = 0; i < len; i++) {
    for (let j = i + 1; j < len; j++) {
      if (arr[i] === arr[j]) {
        arr.splice(j, 1);
        // 每删除一个树，j--保证j的值经过自加后不变。同时，len--，减少循环次数提升性能
        len--;
        j--;
      }
    }
  }
  return arr;
}
```

#### indexOf

```javascript
const unique2 = arr => {
  const res = [];
  for (let i = 0; i < arr.length; i++) {
    if (res.indexOf(arr[i]) === -1) res.push(arr[i]);
  }
  return res;
}
```

#### include

```javascript
const unique3 = arr => {
  const res = [];
  for (let i = 0; i < arr.length; i++) {
    if (!res.includes(arr[i])) res.push(arr[i]);
  }
  return res;
}
```

#### filter

```javascript
const unique4 = arr => {
  return arr.filter((item, index) => {
    return arr.indexOf(item) === index;
  });
}
```

#### Map

```javascript
const unique5 = arr => {
  const map = new Map();
  const res = [];
  for (let i = 0; i < arr.length; i++) {
    if (!map.has(arr[i])) {
      map.set(arr[i], true)
      res.push(arr[i]);
    }
  }
  return res;
}
```

### 类数组转化为数组

>  类数组是具有**length**属性，但不具有数组原型上的方法。常见的类数组有**arguments**、DOM操作方法返回的结果。

#### Array.from

```javascript
Array.from(document.querySelectorAll('div'))
```

#### Array.prototype.slice.call()

```javascript
Array.prototype.slice.call(document.querySelectorAll('div'))
```

#### 扩展运算符

```javascript
[...document.querySelectorAll('div')]
```

#### 利用concat

```javascript
Array.prototype.concat.apply([], document.querySelectorAll('div'));
```

#### Array.prototype.filter()



![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/804ee51d522746c3b219548d038413c2~tplv-k3u1fbpfcp-zoom-1.image)



```javascript
Array.prototype.filter = function(callback, thisArg) {
  if (this == undefined) {
    throw new TypeError('this is null or not undefined');
  }
  if (typeof callback !== 'function') {
    throw new TypeError(callback + 'is not a function');
  }
  const res = [];
  // 让O成为回调函数的对象传递（强制转换对象）
  const O = Object(this);
  // >>>0 保证len为number，且为正整数
  const len = O.length >>> 0;
  for (let i = 0; i < len; i++) {
    // 检查i是否在O的属性（会检查原型链）
    if (i in O) {
      // 回调函数调用传参
      if (callback.call(thisArg, O[i], i, O)) {
        res.push(O[i]);
      }
    }
  }
  return res;
}
```

> `>>>`无符号右移



#### Array.prototype.map()



![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b099cf3e06bc4421abac4dc460a13c17~tplv-k3u1fbpfcp-zoom-1.image)



```javascript
Array.prototype.map = function(callback, thisArg) {
  if (this == undefined) {
    throw new TypeError('this is null or not defined');
  }
  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }
  const res = [];
  // 同理
  const O = Object(this);
  const len = O.length >>> 0;
  for (let i = 0; i < len; i++) {
    if (i in O) {
      // 调用回调函数并传入新数组
      res[i] = callback.call(thisArg, O[i], i, this);
    }
  }
  return res;
}
```

#### Array.prototype.forEach()

> `forEach`跟map类似，唯一不同的是`forEach`是没有返回值的。



```javascript
Array.prototype.forEach = function(callback, thisArg) {
  if (this == null) {
    throw new TypeError('this is null or not defined');
  }
  if (typeof callback !== "function") {
    throw new TypeError(callback + ' is not a function');
  }
  const O = Object(this);
  const len = O.length >>> 0;
  let k = 0;
  while (k < len) {
    if (k in O) {
      callback.call(thisArg, O[k], k, O);
    }
    k++;
  }
}

```

#### Array.prototype.reduce()



![img](data:image/svg+xml;utf8,<?xml version="1.0"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="800" height="600"></svg>)



```javascript
Array.prototype.reduce = function(callback, initialValue) {
  if (this == undefined) {
    throw new TypeError('this is null or not defined');
  }
  if (typeof callback !== 'function') {
    throw new TypeError(callbackfn + ' is not a function');
  }
  const O = Object(this);
  const len = this.length >>> 0;
  let accumulator = initialValue;
  let k = 0;
  // 如果第二个参数为undefined的情况下
  // 则数组的第一个有效值作为累加器的初始值
  if (accumulator === undefined) {
    while (k < len && !(k in O)) {
      k++;
    }
    // 如果超出数组界限还没有找到累加器的初始值，则TypeError
    if (k >= len) {
      throw new TypeError('Reduce of empty array with no initial value');
    }
    accumulator = O[k++];
  }
  while (k < len) {
    if (k in O) {
      accumulator = callback.call(undefined, accumulator, O[k], k, O);
    }
    k++;
  }
  return accumulator;
}
```

#### Function.prototype.apply()

第一个参数是绑定的this，默认为`window`，第二个参数是数组或类数组

```javascript
Function.prototype.apply = function(context = window, args) {
  if (typeof this !== 'function') {
    throw new TypeError('Type Error');
  }
  const fn = Symbol('fn');
  context[fn] = this;

  const res = context[fn](...args);
  delete context[fn];
  return res;
}
```

#### Function.prototype.call()

于`call`唯一不同的是，`call()`方法接受的是一个参数列表

```javascript
Function.prototype.call = function(context = window, ...args) {
  if (typeof this !== 'function') {
    throw new TypeError('Type Error');
  }
  const fn = Symbol('fn');
  context[fn] = this;

  const res = context[fn](...args);
  delete context[fn];
  return res;
}
```

#### Function.prototype.bind

```javascript
Function.prototype.bind = function(context, ...args) {
  if (typeof this !== 'function') {
    throw new Error("Type Error");
  }
  // 保存this的值
  var self = this;

  return function F() {
    // 考虑new的情况
    if(this instanceof F) {
      return new self(...args, ...arguments)
    }
    return self.apply(context, [...args, ...arguments])
  }
}
```



## 函数防抖

> 多次触发只执行最后一次

当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，如果设定时间到来之前，又触发了事件，就重新开始延时。也就是说当一个用户一直触发这个函数，且每次触发函数的间隔小于既定时间，那么防抖的情况下只会执行一次。

```js
function debounce(fn, wait) {
    var timeout = null;      //定义一个定时器
    return function() {
        if(timeout !== null) 
                clearTimeout(timeout);  //清除这个定时器
        timeout = setTimeout(fn, wait);  
    }
}
// 处理函数
function handle() {
    console.log(Math.random()); 
}
// 滚动事件
window.addEventListener('scroll', debounce(handle, 1000));
```



## 函数节流

> 多次触发变成间隔执行

当持续触发事件时，保证在一定时间内只调用一次事件处理函数，意思就是说，假设一个用户一直触发这个函数，且每次触发小于既定值，函数节流会每隔这个时间调用一次
用一句话总结防抖和节流的区别：防抖是将多次执行变为最后一次执行，节流是将多次执行变为每隔一段时间执行
实现函数节流我们主要有两种方法：时间戳和定时器
例如

```js
var throttle = function(func, delay) {
    var prev = Date.now();
    return function() {
        var context = this;   //this指向window
        var args = arguments;
        var now = Date.now();
        if (now - prev >= delay) {
            func.apply(context, args);
            prev = Date.now();
        }
    }
}
function handle() {
    console.log(Math.random());
}
window.addEventListener('scroll', throttle(handle, 1000));
```

这个节流函数利用时间戳让第一次滚动事件执行一次回调函数，此后每隔1000ms执行一次，在小于1000ms这段时间内的滚动是不执行的
再举一个定时器的例子：

```js
var throttle = function(func, delay) {
    var timer = null;
    return function() {
        var context = this;
        var args = arguments;
        if (!timer) {
            timer = setTimeout(function() {
                func.apply(context, args);
                timer = null;
            }, delay);
        }
    }
}
function handle() {
    console.log(Math.random());
}
window.addEventListener('scroll', throttle(handle, 1000));
```

当触发事件的时候，我们设置了一个定时器，在没到1000ms之前这个定时器为null，而到了规定时间执行这个函数并再次把定时器清除。也就是说当第一次触发事件，到达规定时间再执行这个函数，执行之后马上清除定时器，开始新的循环，那么我们看到的效果就是，滚动之后没有马上打印，而是等待1000ms打印，有一个延迟的效果，并且这段时间滚动事件不会执行函数。
单用时间戳或者定时器都有缺陷，我们更希望第一次触发马上执行函数，最后一次触发也可以执行一次事件处理函数

```js
var throttle = function(func, delay) {
  var timer = null;
  var startTime = Date.now();  //设置开始时间
  return function() {
    var curTime = Date.now();
    var remaining = delay - (curTime - startTime);  //剩余时间
    var context = this;
    var args = arguments;
    clearTimeout(timer);
    if (remaining <= 0) {      // 第一次触发立即执行
      func.apply(context, args);
      startTime = Date.now();
    } else {
      timer = setTimeout(func, remaining);   //取消当前计数器并计算新的remaining
    }
  }
}
function handle() {
  console.log(Math.random());
}
 window.addEventListener('scroll', throttle(handle, 1000));
```



## 函数珂里化

> 指的是将一个接受多个参数的函数 变为 接受一个参数返回一个函数的固定形式，这样便于再次调用，例如f(1)(2)

经典面试题：实现`add(1)(2)(3)(4)=10;` 、 `add(1)(1,2,3)(2)=9;`

```javascript
function add() {
  const _args = [...arguments];
  function fn() {
    _args.push(...arguments);
    return fn;
  }
  fn.toString = function() {
    return _args.reduce((sum, cur) => sum + cur);
  }
  return fn;
}
```

## 模拟new操作

3个步骤：

1. 以`ctor.prototype`为原型创建一个对象。
2. 执行构造函数并将this绑定到新创建的对象上。
3. 判断构造函数执行返回的结果是否是引用数据类型，若是则返回构造函数执行的结果，否则返回创建的对象。

```javascript
function newOperator(ctor, ...args) {
  if (typeof ctor !== 'function') {
    throw new TypeError('Type Error');
  }
  const obj = Object.create(ctor.prototype);
  const res = ctor.apply(obj, args);

  const isObject = typeof res === 'object' && res !== null;
  const isFunction = typeof res === 'function';
  return isObject || isFunction ? res : obj;
}
```

## instanceof

`instanceof`运算符用于检测构造函数的`prototype`属性是否出现在某个实例对象的原型链上。

```javascript
const myInstanceof = (left, right) => {
  // 基本数据类型都返回false
  if (typeof left !== 'object' || left === null) return false;
  let proto = Object.getPrototypeOf(left);
  while (true) {
    if (proto === null) return false;
    if (proto === right.prototype) return true;
    proto = Object.getPrototypeOf(proto);
  }
}
```

## 原型继承

这里只写寄生组合继承了，中间还有几个演变过来的继承但都有一些缺陷

```javascript
function Parent() {
  this.name = 'parent';
}
function Child() {
  Parent.call(this);
  this.type = 'children';
}
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;
```

## Object.is

`Object.is`解决的主要是这两个问题：

```js
+0 === -0  // true
NaN === NaN // false

const is= (x, y) => {
  if (x === y) {
    // +0和-0应该不相等
    return x !== 0 || y !== 0 || 1/x === 1/y;
  } else {
    return x !== x && y !== y;
  }
}
```

## Object.assign

`Object.assign()`方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象（请注意这个操作是浅拷贝）

```javascript
Object.defineProperty(Object, 'assign', {
  value: function(target, ...args) {
    if (target == null) {
      return new TypeError('Cannot convert undefined or null to object');
    }
    
    // 目标对象需要统一是引用数据类型，若不是会自动转换
    const to = Object(target);

    for (let i = 0; i < args.length; i++) {
      // 每一个源对象
      const nextSource = args[i];
      if (nextSource !== null) {
        // 使用for...in和hasOwnProperty双重判断，确保只拿到本身的属性、方法（不包含继承的）
        for (const nextKey in nextSource) {
          if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
            to[nextKey] = nextSource[nextKey];
          }
        }
      }
    }
    return to;
  },
  // 不可枚举
  enumerable: false,
  writable: true,
  configurable: true,
})
```

## 深拷贝

递归的完整版本（考虑到了Symbol属性）：

```javascript
const cloneDeep1 = (target, hash = new WeakMap()) => {
  // 对于传入参数处理
  if (typeof target !== 'object' || target === null) {
    return target;
  }
  // 哈希表中存在直接返回
  if (hash.has(target)) return hash.get(target);

  const cloneTarget = Array.isArray(target) ? [] : {};
  hash.set(target, cloneTarget);

  // 针对Symbol属性
  const symKeys = Object.getOwnPropertySymbols(target);
  if (symKeys.length) {
    symKeys.forEach(symKey => {
      if (typeof target[symKey] === 'object' && target[symKey] !== null) {
        cloneTarget[symKey] = cloneDeep1(target[symKey]);
      } else {
        cloneTarget[symKey] = target[symKey];
      }
    })
  }

  for (const i in target) {
    if (Object.prototype.hasOwnProperty.call(target, i)) {
      cloneTarget[i] =
        typeof target[i] === 'object' && target[i] !== null
        ? cloneDeep1(target[i], hash)
        : target[i];
    }
  }
  return cloneTarget;
}
```

## 20.Promise

实现思路：[Promise源码实现](https://juejin.im/post/6860037916622913550)

```javascript
const PENDING = 'PENDING';      // 进行中
const FULFILLED = 'FULFILLED';  // 已成功
const REJECTED = 'REJECTED';    // 已失败

class Promise {
  constructor(exector) {
    // 初始化状态
    this.status = PENDING;
    // 将成功、失败结果放在this上，便于then、catch访问
    this.value = undefined;
    this.reason = undefined;
    // 成功态回调函数队列
    this.onFulfilledCallbacks = [];
    // 失败态回调函数队列
    this.onRejectedCallbacks = [];

    const resolve = value => {
      // 只有进行中状态才能更改状态
      if (this.status === PENDING) {
        this.status = FULFILLED;
        this.value = value;
        // 成功态函数依次执行
        this.onFulfilledCallbacks.forEach(fn => fn(this.value));
      }
    }
    const reject = reason => {
      // 只有进行中状态才能更改状态
      if (this.status === PENDING) {
        this.status = REJECTED;
        this.reason = reason;
        // 失败态函数依次执行
        this.onRejectedCallbacks.forEach(fn => fn(this.reason))
      }
    }
    try {
      // 立即执行executor
      // 把内部的resolve和reject传入executor，用户可调用resolve和reject
      exector(resolve, reject);
    } catch(e) {
      // executor执行出错，将错误内容reject抛出去
      reject(e);
    }
  }
  then(onFulfilled, onRejected) {
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : value => value;
    onRejected = typeof onRejected === 'function'? onRejected:
      reason => { throw new Error(reason instanceof Error ? reason.message:reason) }
    // 保存this
    const self = this;
    return new Promise((resolve, reject) => {
      if (self.status === PENDING) {
        self.onFulfilledCallbacks.push(() => {
          // try捕获错误
          try {
            // 模拟微任务
            setTimeout(() => {
              const result = onFulfilled(self.value);
              // 分两种情况：
              // 1. 回调函数返回值是Promise，执行then操作
              // 2. 如果不是Promise，调用新Promise的resolve函数
              result instanceof Promise ? result.then(resolve, reject) : resolve(result);
            })
          } catch(e) {
            reject(e);
          }
        });
        self.onRejectedCallbacks.push(() => {
          // 以下同理
          try {
            setTimeout(() => {
              const result = onRejected(self.reason);
              // 不同点：此时是reject
              result instanceof Promise ? result.then(resolve, reject) : reject(result);
            })
          } catch(e) {
            reject(e);
          }
        })
      } else if (self.status === FULFILLED) {
        try {
          setTimeout(() => {
            const result = onFulfilled(self.value);
            result instanceof Promise ? result.then(resolve, reject) : resolve(result);
          });
        } catch(e) {
          reject(e);
        }
      } else if (self.status === REJECTED){
        try {
          setTimeout(() => {
            const result = onRejected(self.reason);
            result instanceof Promise ? result.then(resolve, reject) : reject(result);
          })
        } catch(e) {
          reject(e);
        }
      }
    });
  }
  catch(onRejected) {
    return this.then(null, onRejected);
  }
  static resolve(value) {
    if (value instanceof Promise) {
      // 如果是Promise实例，直接返回
      return value;
    } else {
      // 如果不是Promise实例，返回一个新的Promise对象，状态为FULFILLED
      return new Promise((resolve, reject) => resolve(value));
    }
  }
  static reject(reason) {
    return new Promise((resolve, reject) => {
      reject(reason);
    })
  }
}

```

## 21.Promise.all

`Promise.all`是支持链式调用的，本质上就是返回了一个Promise实例，通过`resolve`和`reject`来改变实例状态。

```javascript
Promise.myAll = function(promiseArr) {
  return new Promise((resolve, reject) => {
    const ans = [];
    let index = 0;
    for (let i = 0; i < promiseArr.length; i++) {
      promiseArr[i]
      .then(res => {
        ans[i] = res;
        index++;
        if (index === promiseArr.length) {
          resolve(ans);
        }
      })
      .catch(err => reject(err));
    }
  })
}

```

## 22.Promise.race

```javascript
Promise.race = function(promiseArr) {
  return new Promise((resolve, reject) => {
    promiseArr.forEach(p => {
      // 如果不是Promise实例需要转化为Promise实例
      Promise.resolve(p).then(
        val => resolve(val),
        err => reject(err),
      )
    })
  })
}

```

## 23.Promise并行限制

就是实现有并行限制的Promise调度器问题。

详细实现思路：[某条高频面试原题：实现有并行限制的Promise调度器](https://juejin.im/post/6854573217013563405)

```javascript
class Scheduler {
  constructor() {
    this.queue = [];
    this.maxCount = 2;
    this.runCounts = 0;
  }
  add(promiseCreator) {
    this.queue.push(promiseCreator);
  }
  taskStart() {
    for (let i = 0; i < this.maxCount; i++) {
      this.request();
    }
  }
  request() {
    if (!this.queue || !this.queue.length || this.runCounts >= this.maxCount) {
      return;
    }
    this.runCounts++;

    this.queue.shift()().then(() => {
      this.runCounts--;
      this.request();
    });
  }
}
   
const timeout = time => new Promise(resolve => {
  setTimeout(resolve, time);
})
  
const scheduler = new Scheduler();
  
const addTask = (time,order) => {
  scheduler.add(() => timeout(time).then(()=>console.log(order)))
}
  
  
addTask(1000, '1');
addTask(500, '2');
addTask(300, '3');
addTask(400, '4');
scheduler.taskStart()
// 2
// 3
// 1
// 4

```

## 24.JSONP

script标签不遵循同源协议，可以用来进行**跨域请求**，优点就是兼容性好但仅限于GET请求

```javascript
const jsonp = ({ url, params, callbackName }) => {
  const generateUrl = () => {
    let dataSrc = '';
    for (let key in params) {
      if (Object.prototype.hasOwnProperty.call(params, key)) {
        dataSrc += `${key}=${params[key]}&`;
      }
    }
    dataSrc += `callback=${callbackName}`;
    return `${url}?${dataSrc}`;
  }
  return new Promise((resolve, reject) => {
    const scriptEle = document.createElement('script');
    scriptEle.src = generateUrl();
    document.body.appendChild(scriptEle);
    window[callbackName] = data => {
      resolve(data);
      document.removeChild(scriptEle);
    }
  })
}

```

## 25.AJAX

```javascript
const getJSON = function(url) {
  return new Promise((resolve, reject) => {
    const xhr = XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Mscrosoft.XMLHttp');
    xhr.open('GET', url, false);
    xhr.setRequestHeader('Accept', 'application/json');
    xhr.onreadystatechange = function() {
      if (xhr.readyState !== 4) return;
      if (xhr.status === 200 || xhr.status === 304) {
        resolve(xhr.responseText);
      } else {
        reject(new Error(xhr.responseText));
      }
    }
    xhr.send();
  })
}

```

## 26.event模块

实现node中回调函数的机制，node中回调函数其实是内部使用了**观察者模式**。

> 观察者模式：定义了对象间一种一对多的依赖关系，当目标对象Subject发生改变时，所有依赖它的对象Observer都会得到通知。

```javascript
function EventEmitter() {
  this.events = new Map();
}

// 需要实现的一些方法：
// addListener、removeListener、once、removeAllListeners、emit

// 模拟实现addlistener方法
const wrapCallback = (fn, once = false) => ({ callback: fn, once });
EventEmitter.prototype.addListener = function(type, fn, once = false) {
  const hanlder = this.events.get(type);
  if (!hanlder) {
    // 没有type绑定事件
    this.events.set(type, wrapCallback(fn, once));
  } else if (hanlder && typeof hanlder.callback === 'function') {
    // 目前type事件只有一个回调
    this.events.set(type, [hanlder, wrapCallback(fn, once)]);
  } else {
    // 目前type事件数>=2
    hanlder.push(wrapCallback(fn, once));
  }
}
// 模拟实现removeListener
EventEmitter.prototype.removeListener = function(type, listener) {
  const hanlder = this.events.get(type);
  if (!hanlder) return;
  if (!Array.isArray(this.events)) {
    if (hanlder.callback === listener.callback) this.events.delete(type);
    else return;
  }
  for (let i = 0; i < hanlder.length; i++) {
    const item = hanlder[i];
    if (item.callback === listener.callback) {
      hanlder.splice(i, 1);
      i--;
      if (hanlder.length === 1) {
        this.events.set(type, hanlder[0]);
      }
    }
  }
}
// 模拟实现once方法
EventEmitter.prototype.once = function(type, listener) {
  this.addListener(type, listener, true);
}
// 模拟实现emit方法
EventEmitter.prototype.emit = function(type, ...args) {
  const hanlder = this.events.get(type);
  if (!hanlder) return;
  if (Array.isArray(hanlder)) {
    hanlder.forEach(item => {
      item.callback.apply(this, args);
      if (item.once) {
        this.removeListener(type, item);
      }
    })
  } else {
    hanlder.callback.apply(this, args);
    if (hanlder.once) {
      this.events.delete(type);
    }
  }
  return true;
}
EventEmitter.prototype.removeAllListeners = function(type) {
  const hanlder = this.events.get(type);
  if (!hanlder) return;
  this.events.delete(type);
}

```

## 27.图片懒加载

可以给img标签统一自定义属性`data-src='default.png'`，当检测到图片出现在窗口之后再补充**src**属性，此时才会进行图片资源加载。

```javascript
function lazyload() {
  const imgs = document.getElementsByTagName('img');
  const len = imgs.length;
  // 视口的高度
  const viewHeight = document.documentElement.clientHeight;
  // 滚动条高度
  const scrollHeight = document.documentElement.scrollTop || document.body.scrollTop;
  for (let i = 0; i < len; i++) {
    const offsetHeight = imgs[i].offsetTop;
    if (offsetHeight < viewHeight + scrollHeight) {
      const src = imgs[i].dataset.src;
      imgs[i].src = src;
    }
  }
}

// 可以使用节流优化一下
window.addEventListener('scroll', lazyload);

```

## 28.滚动加载

原理就是监听页面滚动事件，**分析clientHeight**、**scrollTop**、**scrollHeight**三者的属性关系。

```javascript
window.addEventListener('scroll', function() {
  const clientHeight = document.documentElement.clientHeight;
  const scrollTop = document.documentElement.scrollTop;
  const scrollHeight = document.documentElement.scrollHeight;
  if (clientHeight + scrollTop >= scrollHeight) {
    // 检测到滚动至页面底部，进行后续操作
    // ...
  }
}, false);

```

一个Demo：[页面滚动加载的Demo](https://github.com/SherrybabyOne/Demos/blob/master/Interview/JavaScript/滚动加载.html)

## 29.渲染几万条数据不卡住页面

渲染大数据时，合理使用**createDocumentFragment**和**requestAnimationFrame**，将操作切分为一小段一小段执行。

```javascript
setTimeout(() => {
  // 插入十万条数据
  const total = 100000;
  // 一次插入的数据
  const once = 20;
  // 插入数据需要的次数
  const loopCount = Math.ceil(total / once);
  let countOfRender = 0;
  const ul = document.querySelector('ul');
  // 添加数据的方法
  function add() {
    const fragment = document.createDocumentFragment();
    for(let i = 0; i < once; i++) {
      const li = document.createElement('li');
      li.innerText = Math.floor(Math.random() * total);
      fragment.appendChild(li);
    }
    ul.appendChild(fragment);
    countOfRender += 1;
    loop();
  }
  function loop() {
    if(countOfRender < loopCount) {
      window.requestAnimationFrame(add);
    }
  }
  loop();
}, 0)

```

## 30.打印出当前网页使用了多少种HTML元素

一行代码可以解决：

```javascript
const fn = () => {
  return [...new Set([...document.querySelectorAll('*')].map(el => el.tagName))].length;
}

```

值得注意的是：DOM操作返回的是**类数组**，需要转换为数组之后才可以调用数组的方法。

## 31.将VirtualDom转化为真实DOM结构

这是当前SPA应用的核心概念之一

```javascript
// vnode结构：
// {
//   tag,
//   attrs,
//   children,
// }

//Virtual DOM => DOM
function render(vnode, container) {
  container.appendChild(_render(vnode));
}
function _render(vnode) {
  // 如果是数字类型转化为字符串
  if (typeof vnode === 'number') {
    vnode = String(vnode);
  }
  // 字符串类型直接就是文本节点
  if (typeof vnode === 'string') {
    return document.createTextNode(vnode);
  }
  // 普通DOM
  const dom = document.createElement(vnode.tag);
  if (vnode.attrs) {
    // 遍历属性
    Object.keys(vnode.attrs).forEach(key => {
      const value = vnode.attrs[key];
      dom.setAttribute(key, value);
    })
  }
  // 子数组进行递归操作
  vnode.children.forEach(child => render(child, dom));
  return dom;
}

```

## 32.字符串解析问题

```javascript
var a = {
    b: 123,
    c: '456',
    e: '789',
}
var str=`a{a.b}aa{a.c}aa {a.d}aaaa`;
// => 'a123aa456aa {a.d}aaaa'

```

实现函数使得将str字符串中的`{}`内的变量替换，如果属性不存在保持原样（比如`{a.d}`）

类似于模版字符串，但有一点出入，实际上原理大差不差

```javascript
const fn1 = (str, obj) => {
    let res = '';
    // 标志位，标志前面是否有{
    let flag = false;
    let start;
    for (let i = 0; i < str.length; i++) {
        if (str[i] === '{') {
            flag = true;
            start = i + 1;
            continue;
        }
        if (!flag) res += str[i];
        else {
            if (str[i] === '}') {
                flag = false;
                res += match(str.slice(start, i), obj);
            }
        }
    }
    return res;
}
// 对象匹配操作
const match = (str, obj) => {
    const keys = str.split('.').slice(1);
    let index = 0;
    let o = obj;
    while (index < keys.length) {
        const key = keys[index];
        if (!o[key]) {
            return `{${str}}`;
        } else {
            o = o[key];
        }
        index++;
    }
    return o;
}
```


作者：洛霞
链接：https://juejin.im/post/6875152247714480136
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## hasOwnProperty使用场景

```js
var obj1 = {
  a: 1,
  b: 2
}

var obj2 = Object.create(obj1)
obj2.c = 3;
obj2.d = 4;

for (let i in obj2) { // 这样会把obj的原型遍历出来
  console.log(obj2[i]) 
}// 3, 4, 1, 2

for (let i in obj2) {
  if ( obj2.hasOwnProperty(i)) {  // 可以过滤掉原型的变量
  	console.log(obj2[i])  
  }
}// 3, 4
```



## 闭包

> 闭包 : 是由函数以及生命该函数的词法环境组合而成
>
> - 能够读取其他函数内部变量的函数
> - 子函数在外调用,
> - 子函数所在的父函数所在的父函数的作用域不会释放

### 特点

> - 让外部函数可以访问内部变量
>
> - 局部变量可以常驻在内存中
>
> - 可以避免使用全局变量,防止全局变量污染
>
> - 会造成内存泄露(有一块内存空间被长期占用,而不被释放)



```js
function makeAdder(x) {
  return function(y) {//闭包可以访问其所在的外部函数的变量和参数,即使外部函数寿命终结了
    return x + y;
  };
}

var add5 = makeAdder(5);//每执行一次都会创建一块内存空间
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```



```js
var add = function(x) { 
  var sum = 1; 
  var tmp = function(x) { 
      sum = sum + x; 
      return tmp;    
  } 
  tmp.toString = function() { 
      return sum; 
  }
  return tmp; 
} 
alert(add(1)(2)(3));     //6
```



```js
var lis = document.getElementsByTagName("li");
for(var i=0;i<lis.length;i++){
  (function(i){
      lis[i].onclick = function(){
           console.log(i);
      };
  })(i);       //事件处理函数中闭包的写法
}  
```





## 创建和继承



es5

```js
function Animal(name){
  this.name = name || 'Animal'
  this.sleep = function(){
    console.log(this.name + '正在睡觉');
  }
}
Animal.prototype.eat = function(food){
  console.log(this.name + '正在吃' +food);
}
Animal.prototype.nikename = 'aaa';
```



```js
var obj = Object.create({x:1,y:2});//obj继承了属性x和y
```





es6

```js
class Animal(name){
  this.name = name || 'Animal'
  function sleep(){
    console.log(this.name + '正在睡觉');
  }
  function eat(food){
  		console.log(this.name + '正在吃' +food);
	}
}
```





## 模态框(随鼠标移动的窗口)

> 场景: 一个div盒子里面装有一个title的表单
>
> 实现:这个模态框是被鼠标拖拽走

```js
//获取元素的标题,添加监听事件,当鼠标摁下事件触发
document.querySelector('title').addEventListener('mousedown', function(e){
    let x =  e.pageX - login.offsetLeft;
    let y = e.pageY - login.offsetTop;
  //鼠标移动时候,,把鼠标的坐标减去盒子的坐标就是模态框的left和top值
    document.addEventListener('mousemove', move);
    function move(e){
        login.style.left = e.pageX - x +'px';
        login.style.top = e.pageY -  y  +'px';
    } 
//当鼠标弹起,让鼠标把移动事件移除
    document.addEventListener('mouseup', function(){
        document.addEventListener('mousemove', move);
    })
})
```



## 数组去重

```js
 function qc(arr){
   var obj={};
   for(val of arr){
   obj[val]=val;
   }
   arr=[];
   var i=0;
   for(var val in obj){
   arr[i++]=val;
   }
   return arr;	
 }
```

