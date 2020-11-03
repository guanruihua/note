---
title: es6
date: 2020-09-10 10:20:52
tags: 
	- javascript
	- es6
---

# es6

## 数据类型

> 前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）symbol(ES6新增)



## let const

### let

> - 块级作用域:类似于局部变量,只在所处的代码块有效
> - 不可以重复声明
> - 不存在变量提升

```js
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

> var 变量声明 window.variable === variable
>
> ```js
> var age =14;
> console.log(window.age) // 14
> ```
>
> 这样会造成全局变量污染

demo

```js
// 生成十个按钮, 每次点击的时候弹出对应的数字

// 传统方法
var i= 0;
for (i =1; i <= 10; i++) {
  (function(i){
    var btn = document.createElement('button');
    btn.innerText = i;
    btn.onclick = function() {
      alert(i);
    }
    document.body.appendChild(btn);
  })(i);
}

// 使用let 方法
for (let = 1; i<=10; i++){
  var btn = document.createElement('button');
  btn.innerText = i;
  btn.onclick = function() {
		alert(i)
  }
  document.body.appendChild(btn);
}
```





### const

> - 声明一个只读的常量,常量的值不可以改变
>
> - 一定要赋初值
> - 对于符合类型的变量,变量不指向数据,而是指向数据所在的地址

```js
// 使变量不可以更改
var CST = { value: '张三' };
Object.defineProperty(CST, 'value', {
  writable: false
})

Object.seal(CST); // CST也不可以挂载任何变量/或拓展

const PI = 3.1415;
PI // 3.1415

PI = 3;
// TypeError: Assignment to constant variable.
```

> cost变量还是可以赋值的

```js
const foo = {};
foo.prop = 123;

foo.prop
// 123

const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报错
```

## 变量的解构赋值

### 基本用法

```js
var a = 1;
var b = 2;
var c = 3;
//可以写成
var [a, b, c] = [1, 2, 3];
//set结构
let [x, y, z] = new Set(["a", "b", "c"]);
//默认值
[x, y = 'b'] = ['a']; // x='a', y='b'
[x, y = 'b'] = ['a', undefined]; // x='a', y='b'
//对象
var { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"
//字符串
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
let {length : len} = 'hello';
len // 5
```

### 遍历map结构

```js
var map = new Map();
map.set('first','hello');
map.set('second','world');

for(let [key, value] of map){
  console.log(key+"is"+value);
}

//获取键名
for(let [key] of map){...}
//获取键值
for(let [,value] of map){...}
```

### 输入模块的指定方法

```js
const { SourceMapConsumer, SourceNode } = require("source-map");
```

## 字符串拓展

### 字符的Unicode表示法

> `\u0000`——`\uFFFF`之间的字符。超出这个范围的字符，必须用两个双字节的形式表达

```js
"\uD842\uDFB7"
// "𠮷"
"\u20BB7"
// " 7"(这里js理解为"\u20BB+7"=>空格+7)
//放进化括号可以解决以上问题
'\u{1F680}' === '\uD83D\uDE80'
// true
```

#### 六种方式表示一个字符

```js
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```

### codePointAt()

> 普通字符:2个字符(UTF-16格式)
>
> 特殊字符:4个字符(Unicode格式[Unicode码点>0xFFFF])

```js
var s = "𠮷";//0xD842 0xDFB7

s.length // 2
s.charAt(0) // ''
s.charAt(1) // ''
s.charCodeAt(0) // 55362
s.charCodeAt(1) // 57271
```

### at()

```js
'abc'.charAt(0) // "a"
'𠮷'.charAt(0) // "\uD842"

'abc'.at(0) // "a"
'𠮷'.at(0) // "𠮷"
```



### 字符串遍历器

> for ...of可以遍历大于0xFFFF的码点

```js
for (let codePoint of 'foo') {
  console.log(codePoint)
}
// "f"
// "o"
// "o"
```



### includes(), startsWith(), endsWith()

> - indexOf():用来确定一个字符串是否包含在另一个字符串中。
> - **includes()**：返回布尔值，表示是否找到了参数字符串。
>
> - **startsWith()**：返回布尔值，表示参数字符串是否在源字符串的头部。
> - **endsWith()**：返回布尔值，表示参数字符串是否在源字符串的尾部。

```js
var s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

repest()

> 返回一个字符重复n次的新字符

```js
 'x'.repeat(3) // "xxx"
```

### 模板字符串

```js
// 字符串中嵌入变量
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`


//标签模板
alert`123`
// 等同于
alert(123)
```

## symbol

> - 通过Symbol函数生成
>   -  原来就有的字符串
>   -  新增的Symbol类型
> - 每一个symbol都是不相等的
> - 

```js
let s = Symbol();

typeof s
// "symbol"

var mySymbol = Symbol();

var a = {};
a[mySymbol] = 'Hello!';
```

## set和Map数据结构

### Set

> - 每一个成员都是唯一,没有重复的值
> - 遍历操作
>   - keys():返回键名的遍历器
>   - values():返回键值的遍历器
>   - entries():返回键值对的遍历器
>   - forEach():使用回调函数遍历每一个成员

```js
var s = new Set();

[2, 3, 5, 4, 5, 2, 2].map(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4

// 例一
var set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]

// 例二
var items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

// 例三
function divs () {
  return [...document.querySelectorAll('div')];
}

var set = new Set(divs());
set.size // 56

// 类似于
divs().forEach(div => set.add(div));
set.size // 56
```



### Map

> - 只能使用字符串当做键
> - set(key,value):赋值
> - get(key):获取

```js
var data = {};
var element = document.getElementById('myDiv');

data[element] = 'metadata';
data['[object HTMLDivElement]'] // "metadata"

```

```javascript
var m = new Map();
var o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

## 数组拓展

### Array.from()

> `Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。

```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']

Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```

### Array.of()

> 将一组值转换成数组

```js
Array.of(3, 11, 8) // [3,11,8]
```

### copyWithin()

> 指定数组的元素复制到指定位置
>
> ```javascript
> Array.prototype.copyWithin(target, start = 0, end = this.length)
> target（必需）：从该位置开始替换数据。
> start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
> end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。
> 
> [1, 2, 3, 4, 5].copyWithin(0, 3)
> // [4, 5, 3, 4, 5]
> 
> ```





### find()和findIndex()

> 查找数组相应的元素

```js
[1, 4, -5, 10].find((n) => n < 0)
// -5

[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10

```

### fill()

> 给定值填充为一个数组

```js
new Array(3).fill(7)
// [7, 7, 7]
```

### entries()，keys()和values()



```js
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

### includes()

> `Array.prototype.includes`方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的`includes`方法类似。该方法属于ES7，但Babel转码器已经支持

```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true
//第二个参数:匹配比较
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
```

## Proxy和Reflect

### Proxy

> Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。
>
> Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。
>
> ```javascript
> var proxy = new Proxy(target, handler);
> target:拦截目标
> handler:拦截行为
> ```

```js
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});

obj.count = 1
//  setting count!
++obj.count
//  getting count!
//  setting count!
//  2
```

> 对于可以设置、但没有设置拦截的操作，则直接落在目标对象上，按照原先的方式产生结果。
>
> **（1）get(target, propKey, receiver)**
>
> 拦截对象属性的读取，比如`proxy.foo`和`proxy['foo']`。
>
> 最后一个参数`receiver`是一个对象，可选，参见下面`Reflect.get`的部分。
>
> ```js
> var person = {
> name: "张三"
> };
> 
> var proxy = new Proxy(person, {
> get: function(target, property) {
>  if (property in target) {
>    return target[property];
>  } else {
>    throw new ReferenceError("Property \"" + property + "\" does not exist.");
>  }
> }
> });
> 
> proxy.name // "张三"
> proxy.age // 抛出一个错误
> ```
>
> 
>
> **（2）set(target, propKey, value, receiver)**
>
> 拦截对象属性的设置，比如`proxy.foo = v`或`proxy['foo'] = v`，返回一个布尔值。
>
> ```js
> let validator = {
> set: function(obj, prop, value) {
>  if (prop === 'age') {
>    if (!Number.isInteger(value)) {
>      throw new TypeError('The age is not an integer');
>    }
>    if (value > 200) {
>      throw new RangeError('The age seems invalid');
>    }
>  }
> 
>  // 对于age以外的属性，直接保存
>  obj[prop] = value;
> }
> };
> 
> let person = new Proxy({}, validator);
> 
> person.age = 100;
> 
> person.age // 100
> person.age = 'young' // 报错
> person.age = 300 // 报错
> ```
>
> **（3）has(target, propKey)**
>
> 拦截`propKey in proxy`的操作，以及对象的`hasOwnProperty`方法，返回一个布尔值。
>
> **（4）deleteProperty(target, propKey)**
>
> 拦截`delete proxy[propKey]`的操作，返回一个布尔值。
>
> **（5）ownKeys(target)**
>
> 拦截`Object.getOwnPropertyNames(proxy)`、`Object.getOwnPropertySymbols(proxy)`、`Object.keys(proxy)`，返回一个数组。该方法返回对象所有自身的属性，而`Object.keys()`仅返回对象可遍历的属性。
>
> **（6）getOwnPropertyDescriptor(target, propKey)**
>
> 拦截`Object.getOwnPropertyDescriptor(proxy, propKey)`，返回属性的描述对象。
>
> **（7）defineProperty(target, propKey, propDesc)**
>
> 拦截`Object.defineProperty(proxy, propKey, propDesc）`、`Object.defineProperties(proxy, propDescs)`，返回一个布尔值。
>
> **（8）preventExtensions(target)**
>
> 拦截`Object.preventExtensions(proxy)`，返回一个布尔值。
>
> **（9）getPrototypeOf(target)**
>
> 拦截`Object.getPrototypeOf(proxy)`，返回一个对象。
>
> **（10）isExtensible(target)**
>
> 拦截`Object.isExtensible(proxy)`，返回一个布尔值。
>
> **（11）setPrototypeOf(target, proto)**
>
> 拦截`Object.setPrototypeOf(proxy, proto)`，返回一个布尔值。
>
> 如果目标对象是函数，那么还有两种额外操作可以拦截。
>
> **（12）apply(target, object, args)**
>
> 拦截 Proxy 实例作为函数调用的操作，比如`proxy(...args)`、`proxy.call(object, ...args)`、`proxy.apply(...)`。
>
> **（13）construct(target, args)**
>
> 拦截 Proxy 实例作为构造函数调用的操作，比如`new proxy(...args)`。

### Reflect

> `Reflect`对象与`Proxy`对象一样，也是ES6为了操作对象而提供的新API。`Reflect`对象的设计目的有这样几个。
>
> （1） 将`Object`对象的一些明显属于语言内部的方法（比如`Object.defineProperty`），放到`Reflect`对象上。现阶段，某些方法同时在`Object`和`Reflect`对象上部署，未来的新方法将只部署在`Reflect`对象上。
>
> （2） 修改某些Object方法的返回结果，让其变得更合理。比如，`Object.defineProperty(obj, name, desc)`在无法定义属性时，会抛出一个错误，而`Reflect.defineProperty(obj, name, desc)`则会返回`false`。
>
> - Reflect.apply(target,thisArg,args)
> - Reflect.construct(target,args)
> - Reflect.get(target,name,receiver)
>
> ```js
> var obj = {
>   get foo() { return this.bar(); },
>   bar: function() { ... }
> };
> 
> // 下面语句会让 this.bar()
> // 变成调用 wrapper.bar()
> Reflect.get(obj, "foo", wrapper);
> ```
>
> - Reflect.set(target,name,value,receiver)
> - Reflect.defineProperty(target,name,desc)
> - Reflect.deleteProperty(target,name)
> - Reflect.has(target,name)
> - Reflect.ownKeys(target)
> - Reflect.isExtensible(target)
> - Reflect.preventExtensions(target)
> - Reflect.getOwnPropertyDescriptor(target, name)
> - Reflect.getPrototypeOf(target)
> - Reflect.setPrototypeOf(target, prototype)

## Generator

> - 提供异步变成解决方案
>
> - 状态机:封装多个内部状态
> - 特征
>   - function:关键词和函数名之间有一个星号(没有规定位置,只要在这之间都可以)
>   - 内部使用yield(产出)语句[定义状态]

```js
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';//结束
}
/*
	建立后并不执行,
	返回也不是函数运行结果
	而是一个指向内部状态指针对象(遍历对象Iterator Object)
*/


var hw = helloWorldGenerator();
//done:false;表示对象遍历没有结束
hw.next()
// { value: 'hello', done: false }

hw.next()
// { value: 'world', done: false }

hw.next()
// { value: 'ending', done: true }

hw.next()
// { value: undefined, done: true }//表示遍历结束
```



## promise

> （1）对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`Pending`（进行中）、`Resolved`（已完成，又称Fulfilled）和`Rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是`Promise`这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
>
> （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。`Promise`对象的状态改变，只有两种可能：从`Pending`变为`Resolved`和从`Pending`变为`Rejected`。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。就算改变已经发生了，你再对`Promise`对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。
>
> 有了`Promise`对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，`Promise`对象提供统一的接口，使得控制异步操作更加容易。
>
> `Promise`也有一些缺点。首先，无法取消`Promise`，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，`Promise`内部抛出的错误，不会反应到外部。第三，当处于`Pending`状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。
>
> 如果某些事件不断地反复发生，一般来说，使用stream模式是比部署`Promise`更好的选择。

```js
var promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

### Promise.prototype.then()

> - then方法返回的是一个新的Promise实例
> - 第一个回调函数,会将返回结果作为参数,传入第二个回调函数

```js
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```



### Promise.prototype.catch()

> `Promise.prototype.catch`方法是`.then(null, rejection)`的别名，用于指定发生错误时的回调函数。

### Promise.all()

> 将多个Promise实例,包装成一个新的Promise实例
>
> ```js
> var p = Promise.all([p1, p2, p3]);
> 
> /*
> （1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，
> 		此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
> （2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，
> 		此时第一个被reject的实例的返回值，会传递给p的回
> 调函数。
> */
> ```

### Promise.race()

> 将多个Promise实例,包装一个新的Promise实例
>
> ```js
> var p = Promise.race([p1, p2, p3]);
> /*
> 	p1, p2, p3 中有一个实例率先改变状态,p就会跟着改变,先改变的Promise实例的返回值,就返回给p的回调函数
> */
> ```
>
> 

### Promise.resolve()

> 将现有对象转换为Promise对象
>
> `var jsPromise = Promise.resolve($.ajax('/whatever.json'));`

### Promise.reject()

```js
var p = Promise.reject('出错了');
// 等同于
var p = new Promise((resolve, reject) => reject('出错了'))

p.then(null, function (s){
  console.log(s)
});
// 出错了
```



### done()

> Promise对象的回调链，不管以`then`方法或`catch`方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为Promise内部的错误不会冒泡到全局）。因此，我们可以提供一个`done`方法，总是处于回调链的尾端，保证抛出任何可能出现的错误。

```js
asyncFunc()
  .then(f1)
  .catch(r1)
  .then(f2)
  .done();
```



### finally()

>不管状态,都一定会执行

```js
server.listen(0)
  .then(function () {
    // run test
  })
  .finally(server.stop);
```



### Promise.try()

```js
Promise.try(database.users.get({id: userId}))
  .then(...)
  .catch(...)
```



### Promise对象实现Ajax操作的例子



```js
var getJSON = function(url) {
  var promise = new Promise(function(resolve, reject){
    var client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

    function handler() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```

## async, await

> 异步

```javascript
async function main() {
  try {
    var val1 = await firstStep();
    var val2 = await secondStep(val1);
    var val3 = await thirdStep(val1, val2);

    console.log('Final: ', val3);
  }
  catch (err) {
    console.error(err);
  }
}
```

## function

```js
//传统
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);

//ES6
class Point {
  constructor(x, y) {//类似于java的构造函数
    this.x = x;
    this.y = y;
  }
	// 私有方法
  _bar(baz) {
    return this.snaf = baz;
  }
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```



## 代理Proxy

### 语法

```js
let p = new Proxy(target, handler);
```

> `target`: 一个目标对象( 可以是任何类型对象, 包括数组函数等, 甚至另一个代理 ) 用Proxy 来封装
>
> `handler`: 一个对象, 其属性是执行一个操作时定义代理的行为函数

### 代理使用

```js
const obj = {
  a: 10
}
let handler = {
  get: function(target, name){
    console.log('test: ', target, name)
    // test:  {"a":10} a
    // test:  {"a":10} b
    return name in target ? target[name] : 37
  }
}
let p = new Proxy(obj, handler)
console.log(p.a, p.b) // 10 37
```

