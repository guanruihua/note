---
title: javascript-question
date: 2020-09-13 14:56:02
tags: 
	- javascript
	- question
	- front-end
---

# javascript-question



## parseInt(0.0000008) === 8？

### IEEE 754

JavaScript 的数字系统是采用 IEEE 754，一开始看到这个问题，以为是 IEEE 754 导致的问题。

常见的问题有浮点数比较：

```js
console.log((0.1 + 0.2) == 0.3);  // false
console.log((0.1 + 0.2) === 0.3); // false
console.log(0.1 + 0.2); // 0.30000000000000004
123
```

后来发现这问题并不会导致 `parseInt(0.0000008)` 变成 `8`，那么问题就可能在 `parseInt` 这个函数上。

```basic
## parseInt
> `parseInt(string, radix)`
12
```

`parseInt` 接受两个参数，第一个参数是要转换的字符串（忽略空白）；第二个参数是基数。

例如：

```js
parseInt('   12', 10);  // 12
parseInt('12**', 10);   // 12
parseInt('12.34', 10);  // 12
parseInt(12.34, 10);    // 12
1234
```

最后一个例子让我们看到 `parseInt` 可以将数字类型转换成整数，但最好别这么做。

再来看下面这个例子：

```js
parseInt(1000000000000000000000.5, 10); // 1
```

为什么会这样呢？

`parseInt` 的第一个类型是字符串，所以会将传入的参数转换成字符串，也就是 `String(1000000000000000000000.5)` 的结果为 `'1e+21'`。`parseInt` 并没有将 `'e'` 视为一个数字，所以在转换到 `1` 后就停止了。

这也就可以解释 `parseInt(0.0000008) === 8`：

```js
String(0.000008);  // '0.000008'
String(0.0000008); // '8e-7'
12
```

从上面的程式码可以看出，小于 `0.0000001`（1e-7） 的数字转换成 `String` 时，会变成科学记号法，再对这个数进行 `parseInt` 操作就会导致这个问题发生。

### 结论

> 不要将 `parseInt` 当做转换 `Number` 和 `Integer` 的工具。

再补上一些悲剧：

```js
parseInt(1/0, 19);      // 18
parseInt(false, 16);    // 250
parseInt(parseInt, 16); // 15
parseInt("0x10");       // 16
parseInt("10", 2);      // 2
12345
```





## 标签相关

html中定义六个属性

```latex
1. async 属性: 表示立即下载脚本，但不会影响页面的其他操作。[规定脚本将被异步执行]
2. charset 属性: 规定在外部脚本把文件中使用的编码不同。
3. defer 属性: 表示脚本可以延迟到文档被解析和显示之后再执行。只有对外部脚本有效。
4. src 属性: 表示包含要执行代码的外部文件。
5. type 属性: 规定了脚本的MIME属性[内容属性]
6. language 属性: 已废弃。
```

## 图片的格式



### jpg 格式

```
使用的是一种失真压缩标准格式，24bit色彩，不支持动画，不支持透明色
```

- jpeg的格式的压缩方式是破坏性资料性的压缩。即图片在经过压缩的过程中会遭到可见的破坏，一张图片经过多次的上传和下载，图片会逐渐失真。

优势：

```
 1. 支持摄影图像和写实图像的高级压缩，并且可以利用压缩比例来控制文件的大小。
2. 占用的存储较少
```

劣势：

```tex
1. 有损的压缩会导致图片数据的质量下降。
2. 在编辑和重新保存的时候，失真的效果会积累。
3. 不适合所含颜色较少的，颜色差异较少的图片。
```

### png 格式

```
是一种可移植网络格式，使用的是无损数据格式。
```

优势：

```
 1. 可以在保证不失真的情况，尽可能的压缩图片的大小。
2. 可以存储灰度图像，可以设置透明色
```

劣势：

```
 压缩方式是无损压缩，但是图片文件较大，不适合运用在web应用上。
 
 
```

**总的来说，PNG不适合任何地方，因为这个格式是的图片文件会较大。而JPG就可以使用大部分场景。**

### webp格式

```
一种加快图片的加载速度的图片，压缩图片的体积大约为jpeg的三分之二，并能解决服务器的服务器宽带资源和数据空间。
```





## localStorage

- 特点:

1. 存储到浏览器的会话中, localStorage的数据可以长期保存
2. localStorage的键值对是以字符串的形式存储
3. localStorage 目前是支持IE8以上的浏览器
4. 解决了cookie存储空间不足的问题 cookie最大4k localStorage 最大为5M
5. 特定于页面的协议

- 添加&&修改

```js
/*
 * key存在时, 则是修改key对应的value
 */
localStorage.setItem('test','this is a test');
```

- 读取

```
localStorage.getItem('test');
```

- 删除

```
localStorage.removeItem('test');
```

- 删除全部 localStorage

```
localStorage.clear();
```

## 闭包

- 问题 :

```js
for(let i = 0; i<5;i++){
    // 在此处写代码 实现每一秒输出一个数字
}
```

- 解决:

使用闭包

```js
for(let i = 0; i<5;i++){
    (function (i){
    settimeout(()=>{
        console.log(i);
    })
    
    },(i+1)*1000)(i);
}
```





## 给滚动事件添加deBounce(防抖)

> 在操作结束后的一段时间内执行一次 

```js

/****************我是分割线********************/
export defalut ComponentDemo extends React.PureComponent{
  constructor(props){
    super(props);
    this.debounce = this.debounce.bind(this);
    this.scrollHandler = this.scrollHandler.bind(this);
  }

  debounce(func,time){
    let timer = null;
    return function(){
      clearTimeOut(timer);
      timer = settimeout(()=>{
        func();
      })
    }
  }
  scrollHandler(){
    /** 函数处理**/
  }
  componentDidMount(){
    window.addEventListern('scroll',this.debounce(()=>this.scrollHandler()),300);
  }
  /** @desc 通常来说,添加了监听事件,就要移除滚动,如果是单页面就不需要移除 , 页面销毁后 , 监听事件也会被移除*/
  componentWillUnmoun(){
    window.removeEventListern('scroll',this.sdebounce(()=>this.scrollHandler(),300))
  }
}
```



## 函数参数默认值

### es6实现

```js
  var b = 2;
  function f1(a = b){
    console.log(a)
  }
     
  // 调用方法
  f1(1) // 1
  f1() // 不给方法f1()传参，a就等于b ，即等于2 打印的值就是2
  
```

- 使用 es6实现参数默认值，参数变量就是为默认声明的，所以不能使用 let const 继续对这个变量声明。

### es5实现

```js
  var b = 2;
  function f1(a){
      a = a || b
   console.log(a);
  }
  f1(1)// 1
  f1()// 2 不传参数的时候 a就等于b，即等于2 
```

## 获取URL?后的参数

```js
/**
   * 获取url后的 id 文章id
   */
  function getUrlData() {
    var url = window.location.search; //url中?之后的部分
    url = url.substring(1); //去掉?
    var dataObj = {};
    if (url.indexOf('&') > -1) {
      url = url.split('&');
      for (var i = 0; i < url.length; i++) {
        var arr = url[i].split('=');
        dataObj[arr[0]] = arr[1];
      }
    } else {
      url = url.split('=');
      dataObj[url[0]] = url[1];
    }
    /**
     * 获取url id的值
     */
    if (dataObj.id) {
      return dataObj.id;
    }else{
        return "没有这个属性"
    }
  }
  console.log(getUrlData());
```



## 监听器监听自定义事件

### 创建event的对象实例, 表示事件类型（createEvent事件）

```
var event = document.createEvent("HTMLEvents");
```

- UIEvents UI 事件,用于触摸屏设备
- MouseEvents 鼠标事件
- MutationEvents Dom结构发生改变触发的事件
- HTMLEvents Html事件

### 初始化event对象的属性(initEvent事件)

```
// eventType事件名，canBubble是否冒泡，cancelable是否可以使用preventDefault取消事件
event.initEvent(eventType事件名, canBubble, cancelable);
```

- eventType 可以是已经定义好的事件，例如click、submit等，经过初始化后可以直接通过对应的操作进行触发。事件类型如果是自定义的，就需要使用dispachEvent事件进行触发。

### 触发自定义事件(dispachEvent事件)

```
// 返回值为 布尔值
// 当event.cancalable为 false，都会返回true。
target.dispachEvent(event);
```

## 浏览器的怪异模式和标准模式

> 怪异模式的产生: 早起没有固定的标准, 导致浏览器都是自己写自己, 没有固定的标准

|                 | 标准模式                | 怪异模式                                                     |
| --------------- | ----------------------- | ------------------------------------------------------------ |
| 解析方式        | 按照W3C标准解析         | 使用浏览器自己的方式解析                                     |
| 盒模型          | W3C的标准模型           | IE盒子模型                                                   |
| Table元素中字体 | font 属性可以继承       | 不可以从父级继承                                             |
| 内联元素的尺寸  | 无法定义自己的宽度      | 定义width 和height 都可以影响到与拿书的尺寸                  |
| 元素溢出        | overflow默认值为visible | 元素大小由内容界定, 溢出不会裁剪,<br>元素框自动调整, 包括溢出内容 |



## null-undefine-NaN

```js
console.log(typeof null);      // 输出 object
console.log(typeof NaN);      //输出number
console.log(typeof undefined);  //输出undefined
```



## json相关

> json 是一种轻量级数据格式, 独立于编程语言来表示和存储数据
> json字符串 => json对象 : `JSON.parse("{'a':'hello'}")`
> json对象 => json字符串 : `JSON.stringify({'a':123})` 



## ajax和flash的优缺点

```
Ajax
  Ajax的优势：1.可搜索性 2.开放性 3.费用 4.易用性 5.易于开发。
  Ajax的劣势：
    1.它可能破坏浏览器的后退功能   
    2.使用动态页面更新使得用户难于将某个特定的状态保存到收藏夹中 ，不过这些都有相关方法解决。

Flash
  Flash的优势：1.多媒体处理 2.兼容性 3.矢量图形 4.客户端资源调度
  Flash的劣势：
  	1.二进制格式 
  	2.格式私有 
  	3.flash 文件经常会很大，用户第一次使用的时候需要忍耐较长的等待时间  
  	4.性能问题
```



## web Worker

> ​    		web Worker 本质是一个线程，在UI主线程之外并发执行的线程，主要解决耗时的JS任务, 不占用浏览器自身进程, 不影响页面的性能.
>
> 
>
> 首先了解浏览器的线程模型是怎样的？
>
> ​		程序：计算机可以执行的代码，存在**磁盘**中 --- 这是静止的（比如这是买的一块地皮）；
>
> ​		进程：把 **程序** 调入到内存中，等待被**CPU**执行 --- 这是活动的（这是在地皮上建起来的几个工厂）；
>
> ​		线程：是CPU执行 **进程** 代码的基本单位 --- 相当于生产任务(这是在工厂中进行生产的生产线)；
>
> 
>
> 而 进程 与 线程 的关系是：进程是操作系统分配内存的基本单位，线程处于进程内部，是CPU执行代码的基本单位，一个进程中至少有一个线程，也可以有多个（就比如在一个工程内，可以有一条生产线，也可以有多条生产线），多个线程间并发执行，从宏观上看是‘同时’执行，微观上看是‘轮流’执行。


> **拿chrome中的线程模型举例**
>
> 
>
> ​		1.chrome 中发起HTTP请求最多可以使用6个并发线程；
>
> ​		2.而负责向页面中执行绘制任务(HTML/CSS/JS/事件处理代码)的只有1个线程 --- UI主线程，如果碰到耗时的代码就有问题了，解决的办法：创建一个新的线程，去执行耗时的JS任务 -- 与UI主线程并发执行
>
> 
>
> Worker 线程的缺点：浏览器禁止Worker线程操作任何BOM 和 DOM对象，不能使用Worder加载类似jQuery.js文件。



## Cookie

```js
export const setCookie = function setCookie(name, value) {
    // var Days = 30; 
    var exp = new Date();
    exp.setTime(exp.getTime() + 120 * 60 * 1000);
    document.cookie = name + "=" + escape(value) + ";expires=" + exp.toGMTString() + ";path=/";
}

//读取cookies 
export const getCookie = function getCookie(name) {
    var arr, reg = new RegExp("(^| )" + name + "=([^;]*)(;|$)");
    if (arr = document.cookie.match(reg))
        return unescape(arr[2]);
    else
        return null;
}

//删除cookies 
export const delCookie = function delCookie(name) {
    var exp = new Date();
    exp.setTime(exp.getTime() - 1);
    var cval = getCookie(name);
    if (cval != null)
        document.cookie = name + "=" + cval + ";expires=" + exp.toGMTString() + ";path=/brand";
    document.cookie = name + "=" + cval + ";expires=" + exp.toGMTString() + ";path=/   ";

}
//使用示例 
// setCookie("name","hayden"); 
// alert(getCookie("name")); 
```





## 数组下标问题

```js
var arr = [];
arr["a"] = 1;
console.log(arr.length);   // 0
arr['2'] = 2;
console.log(arr.length);   // 3
arr.length = 0;
console.log(arr);          // [a:1]
arr.length//0
arr['a']//1
```



​			javascript 数组下标值的范围为0到2的32次方 对于给定的数字下标值,如果不在这个范围内 js 就会把这个值转为字符串 并当做一个数组对象存储, 而不是一个数组元素 但是如果下标值在合法范围之内 无论是数字型字符串还是数字 都转换为数字, array["100"] = array[100];
​			使用字符串当做下标是 其实就相当于给该数组对象中存储了一个属性 由于给数组对象添加一个属性时 数组的长度始终为0

