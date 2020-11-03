---
title: css-layout
date: 2020-09-09 00:00:58
tags:
	- css
	- layout
	- front-end
	- grid
	- flex
---

# css-layout

## 静态布局

- 静态布局是最为原始的布局方式，没有什么技术性可言，往往是计算机行业刚刚入门的小白使用的布局方式。

- 制作的网页上的**元素尺寸一律以px为单位**。

- 布局特点： 页面上的布局是按最初写代码时候的布局方式进行布局的，常规的pc网站是进行设置了宽度值进行布局的，不会随着pc端的屏幕的大小而变化。

- 优点: 这种布局方式不管是对资深的前端开发工程师还是刚入门的小白来说都是最简单的，最让人容易以接受、学习的，没有我们所说的兼容性的问题。这种布局方式大多用在门户网站和企业的官网上，这些官网的设备的尺寸是固定的，这种布局方式往往是最简单的方法。
- 缺点： 不会随着pc端的屏幕大小而变化。

## 三栏布局

> 左右固定, 中间自适应

```html
<section class="layout float">
  <style type="text/css" media="screen">
    .layout.float .wrapper>div{
      min-height: 100px;
    }
    .layout.float .left{
      float: left;
      width: 300px;
      background: red;
    }
    .layout.float .center{
      background: yellow;
    }
    .layout.float .right{
      float: right;
      width: 300px;
      background: blue;
    }

  </style>
  <article class="wrapper">
    <div class="left"></div>
    <div class="right"></div>
    <div class="center">
      <h1>float布局</h1>
      1.我是float布局的中间部分
      2.我是float布局的中间部分
    </div>
  </article>
</section>


<section class="layout absolute">
  <style type="text/css" media="screen">
    .layout.absolute .wrapper{
      width: 100%;
      margin-top: 20px;
    }
    .layout.absolute .wrapper>div{
      min-height: 100px;
    }
    .layout.absolute .left{
      position: absolute;
      left: 0;
      width: 300px;
      background: red;
    }
    .layout.absolute .center{
      position: absolute;
      left: 300px;
      right: 300px;
      background: yellow;
    }
    .layout.absolute .right{
      position: absolute;
      right: 0;
      width: 300px;
      background: blue;
    }
  </style>
  <article class="wrapper">
    <div class="left"></div>
    <div class="center">
      <h1>absolute布局</h1>
      1.我是absolute布局的中间部分
      2.我是absolute布局的中间部分
    </div>
    <div class="right"></div>
  </article>
</section>


<section class="layout flex">
  <style type="text/css" media="screen">
    .layout.flex .wrapper{
      width: 100%;
      min-height: 100px;
      display: flex;
      margin-top: 140px;
    }
    .layout.flex .left{
      width: 300px;
      background: red;
    }
    .layout.flex .center{
      flex: 1;
      background: yellow;
    }
    .layout.flex .right{
      width: 300px;
      background: blue;
    }
  </style>
  <article class="wrapper">
    <div class="left"></div>
    <div class="center">
      <h1>flex布局</h1>
      1.我是flex布局的中间部分
      2.我是flex布局的中间部分
    </div>
    <div class="right"></div>
  </article>
</section>


<section class="layout table">
  <style type="text/css" media="screen">
    .layout.table .wrapper{
      display: table;
      width: 100%;
      min-height: 100px;
      margin-top: 20px;
    }
    .layout.table .left{
      display: table-cell;
      width: 300px;
      background: red;
    }
    .layout.table .center{
      display: table-cell;
      background: yellow;
    }
    .layout.table .right{
      display: table-cell;
      width: 300px;
      background: blue;
    }

  </style>
  <article class="wrapper">
    <div class="left"></div>
    <div class="center">
      <h1>table布局</h1>
      1.我是table布局的中间部分
      2.我是table布局的中间部分
    </div>
    <div class="right"></div>
  </article>
</section>


<section class="layout grid">
  <style type="text/css" media="screen">
    .layout.grid .wrapper{
      display: grid;
      grid-template-columns: 300px auto 300px;
      grid-template-rows: 100px;
      width: 100%;
      margin-top: 20px;
    }
    .layout.grid .left{
      background: red;
    }
    .layout.grid .center{
      background: yellow;
    }
    .layout.grid .right{
      background: blue;
    }

  </style>
  <article class="wrapper">
    <div class="left"></div>
    <div class="center">
      <h1>grid布局</h1>
      1.我是grid布局的中间部分
      2.我是grid布局的中间部分
    </div>
    <div class="right"></div>
  </article>
</section>

```





## 浮动布局

浮动布局进行调用浮动属性改变页面中元素的位置，浮动布局应该是目前各大网站用的最多的一种布局方式了，但是也特别复杂。浮动元素是脱离文档流的，但不脱离文本流。浮动元素有左浮动（float : left）和右浮动（float : right）两种

```css
.lian{
	width: 90%;
	padding-left: 5%;
}
.lian img{
	float: right;
	margin-top: -180px;
}
.phone ul li{
	list-style: none;
    margin-top: 50px;
    margin-left: 70px;
    color: #808080;
}
.phone ul li img{
	position: absolute;
	margin-left: -80px;
	float: left;
	margin-top: -5px;
}
.view{
	margin-top: 50px;
	margin-left: -5px;
	float: left;
}
.view input{
	width: 120px;
	height: 40px;
	border-radius: 6px;
	border: 1px solid #3CB371;
	background-color: #3CB371;
	font-size: 16px;
	color: white;

}
```

- 优点： 兼容性比较好
- 缺点： 浮动带来的影响比较多，页面宽度不够的时候会影响布局。



## 响应式布局

https://juejin.im/post/5caaa230e51d452b672f9703

响应式布局指的是同一页面在不同屏幕尺寸下有不同的布局。传统的开发方式是PC端开发一套，手机端再开发一套，而使用响应式布局只要开发一套就够，缺点就是CSS比较重。下面是博客网站对不同设备适配后的结果，分别是iPhone5/SE,iphone6/7/8,iphone 6/7/8 plus,ipad pro,dell台式宽屏(1440 X 900)。

响应式设计与自适应设计的区别：响应式开发一套界面，通过检测视口分辨率，针对不同客户端在客户端做代码处理，来展现不同的布局和内容；自适应需要开发多套界面，通过检测视口分辨率，来判断当前访问的设备是pc端、平板、手机，从而请求服务层，返回不同的页面。



### **1. 媒体查询**

CSS3媒体查询可以让我们针对不同的媒体类型定义不同的样式，当重置浏览器窗口大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。

如何选择屏幕大小分割点

如何确定媒体查询的分割点也是一个开发中会遇到的问题，

选择600px,900px,1200px,1800px作为分割点、480px,800px,1400px,1400px

上面的分割方案不一定满足项目中的实际需求，我们可以先用跨度大的分割点进行分割，如果出现不适配的情况可以再根据实际情况增加新的分割点。

移动优先 OR PC优先

不管是移动优先还是PC优先，都是依据当随着屏幕宽度增大或减小的时候，后面的样式会覆盖前面的样式。因此，移动端优先首先使用的是min-width，PC端优先使用的max-width。

### **2.百分比布局**

通过百分比单位，可以使得浏览器中组件的宽和高随着浏览器的高度的变化而变化，从而实现响应式的效果。Bootstrap里面的栅格系统就是利用百分比来定义元素的宽高，CSS3支持最大最小高，可以将百分比和max(min)一起结合使用来定义元素在不同设备下的宽高。

子元素的height或width中使用百分比，是相对于子元素的直接父元素，width相对于父元素的width，height相对于父元素的height；子元素的top和bottom如果设置百分比，则相对于直接非static定位(默认定位)的父元素的高度，同样子元素的left和right如果设置百分比，则相对于直接非static定位(默认定位的)父元素的宽度；子元素的padding如果设置百分比，不论是垂直方向或者是水平方向，都相对于直接父亲元素的width，而与父元素的height无关。跟padding一样，margin也是如此，子元素的margin如果设置成百分比，不论是垂直方向还是水平方向，都相对于直接父元素的width；border-radius不一样，如果设置border-radius为百分比，则是相对于自身的宽度，除了border-radius外，还有比如translate、background-size等都是相对于自身的；

从上述对于百分比单位的介绍我们很容易看出如果全部使用百分比单位来实现响应式的布局，有明显的以下两个缺点：

计算困难，如果我们要定义一个元素的宽度和高度，按照设计稿，必须换算成百分比单位。

各个属性中如果使用百分比，相对父元素的属性并不是唯一的。比如width和height相对于父元素的width和height，而margin、padding不管垂直还是水平方向都相对比父元素的宽度、border-radius则是相对于元素自身等等，造成我们使用百分比单位容易使布局问题变得复杂。

### **3.rem布局**

REM是CSS3新增的单位，并且移动端的支持度很高，Android2.x+,ios5+都支持。rem单位都是相对于根元素html的font-size来决定大小的,根元素的font-size相当于提供了一个基准，当页面的size发生变化时，只需要改变font-size的值，那么以rem为固定单位的元素的大小也会发生响应的变化。 因此，如果通过rem来实现响应式的布局，只需要根据视图容器的大小，动态的改变font-size即可（而em是相对于父元素的）。

rem响应式的布局思想：

一般不要给元素设置具体的宽度，但是对于一些小图标可以设定具体宽度值

高度值可以设置固定值，设计稿有多大，我们就严格有多大

所有设置的固定值都用rem做单位（首先在HTML总设置一个基准值：px和rem的对应比例，然后在效果图上获取px值，布局的时候转化为rem值)

js获取真实屏幕的宽度，让其除以设计稿的宽度，算出比例，把之前的基准值按照比例进行重新的设定，这样项目就可以在移动端自适应了

rem布局的缺点：

在响应式布局中，必须通过js来动态控制根元素font-size的大小，也就是说css样式和js代码有一定的耦合性，且必须将改变font-size的代码放在css样式之前

/*上述代码中将视图容器分为10份，font-size用十分之一的宽度来表示，最后在header标签中执行这段代码，就可以动态定义font-size的大小，从而1rem在不同的视觉容器中表示不同的大小，用rem固定单位可以实现不同容器内布局的自适应。*/

REM布局也是目前多屏幕适配的最佳方式。默认情况下我们html标签的font-size为16px,我们利用媒体查询，设置在不同设备下的字体大小。

### **4.视口单位**

css3中引入了一个新的单位vw/vh，与视图窗口有关，vw表示相对于视图窗口的宽度，vh表示相对于视图窗口高度，除了vw和vh外，还有vmin和vmax两个相关的单位。各个单位具体的含义如下：

vw 相对于视窗的宽度，1vw 等于视口宽度的1%，即视窗宽度是100vw

vh  相对于视窗的高度，1vh 等于视口高度的1%，即视窗高度是100vh

vmin  vw和vh中的较小值

vmax  vw和vh中的较大值

用视口单位度量，视口宽度为100vw，高度为100vh（左侧为竖屏情况，右侧为横屏情况）。例如，在桌面端浏览器视口尺寸为650px，那么 1vw = 650 * 1% = 6.5px（这是理论推算的出，如果浏览器不支持0.5px，那么实际渲染结果可能是7px）。

使用视口单位来实现响应式有两种做法：

1.仅使用vw作为CSS单位

2.搭配vw和rem

### **5.图片响应式**

这里的图片响应式包括两个方面，一个就是大小自适应，这样能够保证图片在不同的屏幕分辨率下出现压缩、拉伸的情况；一个就是根据不同的屏幕分辨率和设备像素比来尽可能选择高分辨率的图片，也就是当在小屏幕上不需要高清图或大图，这样我们用小图代替，就可以减少网络带宽了。

1.使用max-width（图片自适应）:

图片自适应意思就是图片能随着容器的大小进行缩放

2.使用srcset  <img srcset="photo_w350.jpg 1x, photo_w640.jpg 2x" src="C:/new_note/刷题/js/photo_w350.jpg" alt="">

3.使用background-image

4.使用picture标签





## grid布局

[原贴地址](https://juejin.im/post/5f1e70315188252e937c088b#heading-9)

### Grid属性汇总

- 弹性布局可以简便、完整、响应的实现各种页面上的布局。

- 与静态不同的是，使用em或rem单位（lem=16px，1rem=10px）进行相对布局，相对使用百分比更加方便、灵活，相应同时支持浏览器的字体大小调整和缩放的等正常显示。

- 优点：
  1.适应性强，在做多种不同的屏幕分辨率不同的界面是非常使用。
  2.随意按照宽度、比例划分元素的宽高。
  3.可以轻松的改变元素的显示顺序。
  4.网页布局实现快捷，维护起来更加容易。
- 如果做移动端时，如果客户对细微的之处的要求不高，使用弹性布局进行制作是最好的选择，一份css+一份js调节font-size搞定。
- 缺点： 浏览器兼容性较差，只能<u>兼容到IE9及以上</u>。

```css
display: grid | inline-grid;
//行列布局
grid-template-columns: 200px 200px 200px; | repeat(3, 200px) | repeat(auto-fill, 200px)[表示列宽200px, 只要能容纳得下就可以放置] | 200px 2fr 1fr [后面两项分别占有剩下的2/3,1/3] | 1fr 1fr minmax(300px, 2fr)[第三列:300px<=x<=2fr]
grid-template-rows: 200px 200px 200px; | repeat(3, 200px) | 和上个类似
//行列间隔
grid-row-gap:10px;
grid-column-gap:20px;
grid-gap:10px 20px;[等同于上两行]
//定义区域
grid-template-areas:
			". header  header"[.表示空单元格]
    "sidebar content content";[这里定义的六个区域]
	//子元素
	.header{
		grid-area: header;
	}
//控制自动布局
grid-auto-flow: row | column | row dense | column dense;[dense:自动填补空白;row: 表示先行后列]
//控制单元格位置
justify-items:start | end | center | stretch[拉伸];[水平方向]
align-items:start | end | center | stretch;[垂直方向]
place-items:[jusity-item] [align-items];//同时设置水平和垂直方向
//这个是对于单个单元格
justify-self:start | end | center | stretch[拉伸];[水平方向]
align-self:start | end | center | stretch;[垂直方向]
place-self:[jusity-item] [align-items];//同时设置水平和垂直方向

//控制内容区域在容器的位置
justify-content: start | end | center | stretch | 
			space-around[每个项目两侧距离相等,项目间间隔比到容器间隙大一倍] | 
			space-between[项目间隔相等,与容器边框没有间隙] | 
			space-evenly[项目与项目的间隙相等, 项目间与容器边框间间隙相等];
align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
place-content: [justify-content] [align-content]
//定义隐式网格属性[当超出grid-template-xxx的定义就会触发]
grid-auto-columns: 50px;
grid-auto-rows: 50px;
//网格项目所在的四个边框
grid-column-start 属性：左边框所在的垂直网格线
grid-column-end 属性：右边框所在的垂直网格线
grid-row-start 属性：上边框所在的水平网格线
grid-row-end 属性：下边框所在的水平网格线
```



### Grid 布局

`Grid` 布局即网格布局，是一种新的 `CSS` 布局模型，比较擅长将一个页面划分为几个主要区域，以及定义这些区域的大小、位置、层次等关系。号称是最强大的的 `CSS` 布局方案，是目前唯一一种 `CSS` 二维布局。利用 `Grid` 布局，我们可以轻松实现类似下图布局，[演示地址](https://codepen.io/gpingfeng/pen/qBbveKB?editors=1100)



![img](https://user-gold-cdn.xitu.io/2020/7/26/17389591885783dd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### Grid 布局和 flex 布局

讲到布局，我们就会想到 `flex` 布局，甚至有人认为竟然有 `flex` 布局了，似乎没有必要去了解 `Grid` 布局。但 `flex` 布局和 `Grid` 布局有实质的区别，那就是 **`flex` 布局是一维布局，`Grid` 布局是二维布局**。`flex` 布局一次只能处理一个维度上的元素布局，一行或者一列。`Grid` 布局是将容器划分成了“行”和“列”，产生了一个个的网格，我们可以将网格元素放在与这些行和列相关的位置上，从而达到我们布局的目的。

**`Grid` 布局远比 `flex` 布局强大！**

flex布局示例:



![img](https://user-gold-cdn.xitu.io/2020/7/28/173945aadff842d1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



Grid 布局示例：



![Grid 布局](https://user-gold-cdn.xitu.io/2020/7/26/173895918bcb5190?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### [Grid 的一些基础概念]

我们使用 Grid 实现一个小例子，演示 Grid 的一些基础概念，[演示地址](https://codepen.io/gpingfeng/pen/QWyoexm?editors=1100)

```css
<div class="wrapper">
  <div class="one item">One</div>
  <div class="two item">Two</div>
  <div class="three item">Three</div>
  <div class="four item">Four</div>
  <div class="five item">Five</div>
  <div class="six item">Six</div>
</div>

.wrapper {
  margin: 60px;
  /* 声明一个容器 */
  display: grid;
  /*  声明列的宽度  */
  grid-template-columns: repeat(3, 200px);
  /*  声明行间距和列间距  */
  grid-gap: 20px;
  /*  声明行的高度  */
  grid-template-rows: 100px 200px;
}
.one {
  background: #19CAAD;
}
.two { 
  background: #8CC7B5;
}
.three {
  background: #D1BA74;
}
.four {
  background: #BEE7E9;
}
.five {
  background: #E6CEAC;
}
.six {
  background: #ECAD9E;
}
.item {
  text-align: center;
  font-size: 200%;
  color: #fff;
}
```



![img](https://user-gold-cdn.xitu.io/2020/7/26/173895918bfd94e9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



容器和项目：我们通过在元素上声明 `display：grid` 或 `display：inline-grid` 来创建一个网格容器。一旦我们这样做，这个元素的所有直系子元素将成为网格项目。比如上面 `.wrapper` 所在的元素为一个网格容器，其直系子元素将成为网格项目。

网格轨道：`grid-template-columns` 和 `grid-template-rows` 属性来定义网格中的行和列。容器内部的水平区域称为行，垂直区域称为列。上图中 `One`、`Two`、`Three` 组成了一行，`One`、`Four` 则是一列



![行和列](https://user-gold-cdn.xitu.io/2020/7/26/173895918ee0ecb6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



网格单元：一个网格单元是在一个网格元素中最小的单位， 从概念上来讲其实它和表格的一个单元格很像。上图中 `One`、`Two`、`Three`、`Four`...都是一个个的网格单元

网格线：划分网格的线，称为"网格线"。应该注意的是，当我们定义网格时，我们定义的是网格轨道，而不是网格线。Grid 会为我们创建编号的网格线来让我们来定位每一个网格元素。m 列有 m + 1 根垂直的网格线，n 行有 n + 1 跟水平网格线。比如上图示例中就有 4 根垂直网格线。一般而言，是从左到右，从上到下，1，2，3 进行编号排序。当然也可以从右到左，从下到上，按照 -1，-2，-3...顺序进行编号排序



![网格线](https://user-gold-cdn.xitu.io/2020/7/26/17389591934e1560?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### 容器属性介绍

`Grid` 布局相关的属性以及值众多，需要记忆的不少，建议可以跟 `demo` 一起结合起来，边敲代码边理解，再利用一些空闲时间记忆一下。笔者会在介绍每个属性的时候，做个小 `demo` 演示，建议大家可以自己修改看看效果加深记忆

`Grid` 布局属性可以分为两大类，一类是容器属性，一类是项目属性。我们先来看容器属性

### display 属性

[display 属性演示](https://codepen.io/gpingfeng/pen/wvMZwqY)

我们通过在元素上声明 `display：grid` 或 `display：inline-grid` 来创建一个网格容器。声明 `display：grid` 则该容器是一个块级元素，设置成 `display: inline-grid` 则容器元素为行内元素

```css
.wrapper {
  display: grid;
}
```



![块级元素](https://user-gold-cdn.xitu.io/2020/7/26/17389591baa442ef?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



```css
.wrapper-1 {
  display: inline-grid;
}
```



![行内属性](https://user-gold-cdn.xitu.io/2020/7/26/17389591c03b6883?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### grid-template-columns 属性和 grid-template-rows 属性

[grid-template-columns 和 grid-template-rows 属性演示地址](https://codepen.io/gpingfeng/pen/BajEBYq?editors=1100)

`grid-template-columns` 属性设置列宽，`grid-template-rows` 属性设置行高，这两个属性在 `Grid` 布局中尤为重要，它们的值是有多种多样的，而且它们的设置是比较相似的，下面针对 `grid-template-columns` 属性进行讲解

**固定的列宽和行高**

```css
.wrapper {
  display: grid;
  /*  声明了三列，宽度分别为 200px 100px 200px */
  grid-template-columns: 200px 100px 200px;
  grid-gap: 5px;
  /*  声明了两行，行高分别为 50px 50px  */
  grid-template-rows: 50px 50px;
}
```

以上表示固定列宽为 200px 100px 200px，行高为 50px 50px



![固定行高和列宽](https://user-gold-cdn.xitu.io/2020/7/26/17389591c0fc1214?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



**repeat() 函数**：可以简化重复的值。该函数接受两个参数，第一个参数是重复的次数，第二个参数是所要重复的值。比如上面行高都是一样的，我们可以这么去实现，实际效果是一模一样的

```scss
.wrapper-1 {
  display: grid;
  grid-template-columns: 200px 100px 200px;
  grid-gap: 5px;
  /*  2行，而且行高都为 50px  */
  grid-template-rows: repeat(2, 50px);
}
```

**auto-fill 关键字**：表示自动填充，让一行（或者一列）中尽可能的容纳更多的单元格。`grid-template-columns: repeat(auto-fill, 200px)` 表示列宽是 200 px，但列的数量是不固定的，只要浏览器能够容纳得下，就可以放置元素，代码以及效果如下图所示：

```css
.wrapper-2 {
  display: grid;
  grid-template-columns: repeat(auto-fill, 200px);
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389591c300e81a?imageslim)



**fr 关键字**：`Grid` 布局还引入了一个另外的长度单位来帮助我们创建灵活的网格轨道。`fr` 单位代表网格容器中可用空间的一等份。`grid-template-columns: 200px 1fr 2fr` 表示第一个列宽设置为 200px，后面剩余的宽度分为两部分，宽度分别为剩余宽度的 1/3 和 2/3。代码以及效果如下图所示：

```css
.wrapper-3 {
  display: grid;
  grid-template-columns: 200px 1fr 2fr;
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389591ccc256d1?imageslim)



**minmax() 函数**：我们有时候想给网格元素一个最小和最大的尺寸，`minmax()` 函数产生一个长度范围，表示长度就在这个范围之中都可以应用到网格项目中。它接受两个参数，分别为最小值和最大值。`grid-template-columns: 1fr 1fr minmax(300px, 2fr)` 的意思是，第三个列宽最少也是要 300px，但是最大不能大于第一第二列宽的两倍。代码以及效果如下：

```css
.wrapper-4 {
  display: grid;
  grid-template-columns: 1fr 1fr minmax(300px, 2fr);
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389591dc05edac?imageslim)



**auto 关键字**：由浏览器决定长度。通过 `auto` 关键字，我们可以轻易实现三列或者两列布局。`grid-template-columns: 100px auto 100px` 表示第一第三列为 100px，中间由浏览器决定长度，代码以及效果如下：

```css
.wrapper-5 {
  display: grid;
  grid-template-columns: 100px auto 100px;
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389591f2146e1d?imageslim)



### grid-row-gap 属性、grid-column-gap 属性以及 grid-gap 属性

[grid-row-gap 属性、grid-column-gap 属性以及 grid-gap 属性演示地址](https://codepen.io/gpingfeng/pen/jOWRNeg)

`grid-row-gap` 属性、`grid-column-gap` 属性分别设置行间距和列间距。`grid-gap` 属性是两者的简写形式。

`grid-row-gap: 10px` 表示行间距是 10px，`grid-column-gap: 20px` 表示列间距是 20px。`grid-gap: 10px 20px` 实现的效果是一样的

```css
.wrapper {
  display: grid;
  grid-template-columns: 200px 100px 100px;
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}
.wrapper-1 {
  display: grid;
  grid-template-columns: 200px 100px 100px;
  grid-auto-rows: 50px;
  grid-row-gap: 10px;
  grid-column-gap: 20px;
}
```

以上两种写法效果是一样的。



![img](https://user-gold-cdn.xitu.io/2020/7/26/17389591f78de6f2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### grid-template-areas 属性

[grid-area 以及 grid-template-areas演示地址](https://codepen.io/gpingfeng/pen/RwrObEJ?editors=1100)

`grid-template-areas` 属性用于定义区域，一个区域由一个或者多个单元格组成

一般这个属性跟网格元素的 `grid-area` 一起使用，我们在这里一起介绍。 `grid-area` 属性指定项目放在哪一个区域

```css
.wrapper {
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 120px  120px  120px;
  grid-template-areas:
    ". header  header"
    "sidebar content content";
  background-color: #fff;
  color: #444;
}
```

上面代码表示划分出 6 个单元格，其中值得注意的是 `.` 符号代表空的单元格，也就是没有用到该单元格。

```css
.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}

.header {
  grid-area: header;
}
复制代码
```

以上代码表示将类 `.sidebar` `.content` `.header`所在的元素放在上面 `grid-template-areas` 中定义的 `sidebar` `content` `header` 区域中



![img](https://user-gold-cdn.xitu.io/2020/7/26/173895920bbe824a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### grid-auto-flow 

[grid-auto-flow 属性演示地址](https://codepen.io/gpingfeng/pen/MWKRWKj?editors=1100)

`grid-auto-flow` 属性控制着自动布局算法怎样运作，精确指定在网格中被自动布局的元素怎样排列。默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行，即下图英文数字的顺序 `one`,`two`,`three`...。这个顺序由 `grid-auto-flow` 属性决定，默认值是 `row`。

```css
.wrapper {
  display: grid;
  grid-template-columns: 100px 200px 100px;
  grid-auto-flow: row;
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![img](https://user-gold-cdn.xitu.io/2020/7/26/173895921548265c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



细心的同学可能发现了一个问题，就是第五个项目和第六个项目之间有个空白（如下图所示），这个是由于第六块的长度大于了空白处的长度，被挤到了下一行导致的。在实际应用中，我们可能想让下面长度合适的填满这个空白，这个时候可以设置 `grid-auto-flow: row dense`，表示尽可能填满表格。代码以及效果如下所示：



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592211e1d6b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



```css
.wrapper-2 {
  display: grid;
  grid-template-columns: 100px 200px 100px;
  grid-auto-flow: row dense;
  grid-gap: 5px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/173895923612a19b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



可以设置 `grid-auto-flow: column`，表示先列后行，代码以及效果如下图所示：

```css
.wrapper-1 {
  display: grid;
  grid-auto-columns: 100px;
  grid-auto-flow: column;
  grid-gap: 5px;
  grid-template-rows:  50px 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/173895923f11dd83?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### justify-items 属性、align-items 属性以及 place-items 属性

[justify-items 属性、align-items 属性演示地址](https://codepen.io/gpingfeng/pen/zYrXYrz?editors=1100)

`justify-items` 属性设置单元格内容的水平位置（左中右），`align-items` 属性设置单元格的垂直位置（上中下）

下面以 justify-items 属性为例进行讲解，align-items 属性同理，只是方向为垂直方向。它们都有如下属性：

```css
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```

其代码实现以及效果如下：

```css
.wrapper, .wrapper-1, .wrapper-2, .wrapper-3 {
  display: grid;
  grid-template-columns: 100px 200px 100px;
  grid-gap: 5px;
  grid-auto-rows: 50px;
  justify-items: start;
}
.wrapper-1 {
  justify-items: end;
}
.wrapper-2 {
  justify-items: center;
}
.wrapper-3 {
  justify-items: stretch;
}
```

- start：对齐单元格的起始边缘



![image](https://user-gold-cdn.xitu.io/2020/7/26/1738959244947d96?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- end：对齐单元格的结束边缘



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592560e3fc2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- center：单元格内部居中



![image](https://user-gold-cdn.xitu.io/2020/7/26/173895925bd879fa?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- stretch：拉伸，占满单元格的整个宽度（默认值）



![image](https://user-gold-cdn.xitu.io/2020/7/26/1738959270057d0c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### justify-content 属性、align-content 属性以及 place-content 属性

[justify-content 属性、align-content 属性演示地址](https://codepen.io/gpingfeng/pen/qBbwBZx?editors=1100)

`justify-content` 属性是整个内容区域在容器里面的水平位置（左中右），`align-content` 属性是整个内容区域的垂直位置（上中下）。它们都有如下的属性值。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```

下面以 `justify-content` 属性为例进行讲解，`align-content` 属性同理，只是方向为垂直方向

- start - 对齐容器的起始边框
- end - 对齐容器的结束边框
- center - 容器内部居中

```css
.wrapper, .wrapper-1, .wrapper-2, .wrapper-3, .wrapper-4, .wrapper-5, .wrapper-6 {
  display: grid;
  grid-template-columns: 100px 200px 100px;
  grid-gap: 5px;
  grid-auto-rows: 50px;
  justify-content: start;
}
.wrapper-1 {
  justify-content: end;
}
.wrapper-2 {
  justify-content: center;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/173895926d20f5d6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍
- space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔
- space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔
- stretch - 项目大小没有指定时，拉伸占据整个网格容器

```
.wrapper-3 {
  justify-content: space-around;
}
.wrapper-4 {
  justify-content: space-between;
}
.wrapper-5 {
  justify-content: space-evenly;
}
.wrapper-6 {
  justify-content: stretch;
}
复制代码
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/173895927ba770c4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### grid-auto-columns 属性和 grid-auto-rows 属性

[grid-auto-columns 属性和 grid-auto-rows 属性演示地址](https://codepen.io/gpingfeng/pen/zYrXvYZ?editors=1100)

在讲 `grid-auto-columns` 属性和 `grid-auto-rows` 属性之前，先来看看隐式和显示网格的概念

**隐式和显示网格**：显式网格包含了你在 `grid-template-columns` 和 `grid-template-rows` 属性中定义的行和列。如果你在网格定义之外又放了一些东西，或者因为内容的数量而需要的更多网格轨道的时候，网格将会在隐式网格中创建行和列

假如有多余的网格（也就是上面提到的隐式网格），那么它的行高和列宽可以根据 `grid-auto-columns` 属性和 `grid-auto-rows` 属性设置。它们的写法和`grid-template-columns` 和 `grid-template-rows` 完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高

```
.wrapper {
  display: grid;
  grid-template-columns: 200px 100px;
/*  只设置了两行，但实际的数量会超出两行，超出的行高会以 grid-auto-rows 算 */
  grid-template-rows: 100px 100px;
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}
复制代码
```

`grid-template-columns` 属性和 `grid-template-rows` 属性只是指定了两行两列，但实际有九个元素，就会产生隐式网格。通过 `grid-auto-rows` 可以指定隐式网格的行高为 50px



![img](https://user-gold-cdn.xitu.io/2020/7/26/173895927d99af1c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



### 项目属性介绍

### grid-column-start 属性、grid-column-end 属性、grid-row-start 属性以及grid-row-end 属性

[演示地址](https://codepen.io/gpingfeng/pen/PoZgopr)

可以指定网格项目所在的四个边框，分别定位在哪根网格线，从而指定项目的位置

- grid-column-start 属性：左边框所在的垂直网格线
- grid-column-end 属性：右边框所在的垂直网格线
- grid-row-start 属性：上边框所在的水平网格线
- grid-row-end 属性：下边框所在的水平网格线

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  grid-auto-rows: minmax(100px, auto);
}
.one {
  grid-column-start: 1;
  grid-column-end: 2;
  background: #19CAAD;
}
.two { 
  grid-column-start: 2;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 2;
  /*   如果有重叠，就使用 z-index */
  z-index: 1;
  background: #8CC7B5;
}
.three {
  grid-column-start: 3;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 4;
  background: #D1BA74;
}
.four {
  grid-column-start: 1;
  grid-column-end: 2;
  grid-row-start: 2;
  grid-row-end: 5;
  background: #BEE7E9;
}
.five {
  grid-column-start: 2;
  grid-column-end: 2;
  grid-row-start: 2;
  grid-row-end: 5;
  background: #E6CEAC;
}
.six {
  grid-column: 3;
  grid-row: 4;
  background: #ECAD9E;
}
```

上面代码中，类 `.two` 所在的网格项目，垂直网格线是从 2 到 4，水平网格线是从 1 到 2。其中它跟 `.three` （垂直网格线是从3 到 4，水平网格线是从 1 到 4） 是有冲突的。可以设置 `z-index` 去决定它们的层级关系



![img](data:image/svg+xml;utf8,<?xml version="1.0"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1240" height="685"></svg>)



### grid-area 属性

`grid-area` 属性指定项目放在哪一个区域，在上面介绍 `grid-template-areas` 的时候有提到过，这里不再具体展开，具体的使用可以参考演示地址：

[grid-area 以及 grid-template-areas 属性演示地址](https://codepen.io/gpingfeng/pen/RwrObEJ)

### justify-self 属性、align-self 属性以及 place-self 属性

[justify-self 属性/ align-self 属性/ place-self 属性演示地址](https://codepen.io/gpingfeng/pen/ZEQZEJK?editors=1100)

`justify-self` 属性设置单元格内容的水平位置（左中右），跟 `justify-items` 属性的用法完全一致，但只作用于单个项目

`align-self` 属性设置单元格内容的垂直位置（上中下），跟align-items属性的用法完全一致，也是只作用于单个项目

两者很相像，这里只拿 `justify-self` 属性演示，`align-self` 属性同理，只是作用于垂直方向

```css
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
复制代码
.item {
  justify-self: start;
}
.item-1 {
  justify-self: end;
}
.item-2 {
  justify-self: center;
}
.item-3 {
  justify-self: stretch;
}
```

- start：对齐单元格的起始边缘



![image](https://user-gold-cdn.xitu.io/2020/7/26/1738959292160e78?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- end：对齐单元格的结束边缘



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592a0d5a3c0?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



- center：单元格内部居中

  ![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592b1378c8d?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  

- stretch：拉伸，占满单元格的整个宽度（默认值）

  ![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592b895f0ed?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  

### Grid 实战——实现响应式布局

经过上面的介绍，相信大家都可以看出，Grid 是非常强大的。一些常见的 CSS 布局，如居中，两列布局，三列布局等等是很容易实现的。我们接下来看看 Grid 布局是如何实现响应式布局的

### fr 实现等分响应式

[fr 实现等分响应式](https://codepen.io/gpingfeng/pen/wvMZKpB?editors=1100)

`fr` 等分单位，可以将容器的可用空间分成想要的多个等分空间。利用这个特性，我们能够轻易实现一个等分响应式。`grid-template-columns: 1fr 1fr 1fr` 表示容器分为三等分

```css
.wrapper {
  margin: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592bf7e44dd?imageslim)



### repeat + auto-fit——固定列宽，改变列数量

等分布局并不只有 `Grid` 布局才有，像 `flex` 布局也能轻松实现，接下来看看更高级的响应式

上面例子的始终都是三列的，但是需求往往希望我们的网格能够固定列宽，并根据容器的宽度来改变列的数量。这个时候，我们可以用到上面提到 `repeat()` 函数以及 `auto-fit` 关键字。`grid-template-columns: repeat(auto-fit, 200px)` 表示固定列宽为 200px，数量是自适应的，只要容纳得下，就会往上排列，代码以及效果实现如下：

[演示地址](https://codepen.io/gpingfeng/pen/eYJopVE?editors=1100)

```css
.wrapper {
  margin: 50px;
  display: grid;
  grid-template-columns: repeat(auto-fit, 200px);
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592c297495a?imageslim)



### repeat+auto-fit+minmax 去掉右侧空白

上面看到的效果中，右侧通常会留下空白，这是我们不希望看到的。如果列的宽度也能在某个范围内自适应就好了。`minmax()` 函数就帮助我们做到了这点。将 `grid-template-columns: repeat(auto-fit, 200px)` 改成 `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))` 表示列宽至少 200px，如果还有空余则一起等分。代码以及效果如下所示：

[演示地址](https://codepen.io/gpingfeng/pen/dyGLYdQ)

```css
.wrapper {
  margin: 50px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}
```



![auto-auto-minmax.gif](https://user-gold-cdn.xitu.io/2020/7/26/17389592cc3c2bf9?imageslim)



### repeat+auto-fit+minmax-span-dense 解决空缺问题

似乎一切进行得很顺利，但是某天 UI 来说，每个网格元素的长度可能不相同，这也简单，通过 `span` 关键字进行设置网格项目的跨度，`grid-column-start: span 3`，表示这个网格项目跨度为 3。具体的代码与效果如下所示：

```css
.item-3 {
  grid-column-start: span 3;
}
```

[演示地址](https://codepen.io/gpingfeng/pen/BajEoxy?editors=1100)



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592f9da3763?imageslim)



不对，怎么右侧又有空白了？原来是有一些长度太长了，放不下，这个时候就到我们的 `dense` 关键字出场了。`grid-auto-flow: row dense` 表示尽可能填充，而不留空白，代码以及效果如下所示：

```css
.wrapper, .wrapper-1 {
  margin: 50px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px 20px;
  grid-auto-rows: 50px;
}

.wrapper-1 {
  grid-auto-flow: row dense;
}
```



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389593009f7fe7?imageslim)



### Grid 布局兼容性

最后，聊聊 `Grid` 布局兼容性问题，在 [caniuse](https://caniuse.com/#search=grid) 中，我们可以看到的结果如下，总体兼容性还不错，但在 IE 10 以下不支持。个人建议在公司的内部系统运用起来是没有问题的，但 TOC 的话，可能目前还是不太合适



![image](https://user-gold-cdn.xitu.io/2020/7/26/17389592fa541366?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

|                   属性                   |            描述            |
| :--------------------------------------: | :------------------------: |
|                 display                  | grid      \|   inline-grid |
| grid-template-columns/grid-template-rows |       设置列宽/行高        |



## 定位布局

定位布局时利用position属性控制页面元素设置一些不规则布局。
定位元素的各个属性：
1.static 静态定位： HTML元素的默认值，即没有定位，元素出现在正常的流中。

```css
div.static {
    position: static;
    border: 3px solid #73AD21;
}
```


2.fixed 固定定位： 元素的位置相对于浏览器窗口是固定位置。即使窗口是滚动的它也不会移动。Fixed定位使元素的位置与文档流无关，因此不占据空间。Fixed定位的元素和其他元素重叠。

```css
p.pos_fixed{
    position:fixed;
    top:30px;
    right:5px;
}
```

3.relative 相对定位： 相对定位元素的定位是以自身为参照物。对象不可层叠、不脱离文档流，移动相对定位元素，但它原本所占的空间不会改变。通过 top,bottom,left,right 定位。

```css
h2.pos_top
{
    position:relative;
    top:-50px;
}
```

4.absolute 绝对定位 absolute 定位使元素的位置与文档流无关，因此不占据空间。元素和其他元素重叠。通过 top,bottom,left,right 定位。选取其最近一个最有定位设置的父级对象进行绝对定位，如果对象的父级没有设置定位属性，absolute元素将以body坐标原点进行定位。

h2{
    position:absolute;
    left:100px;
    top:150px;
}

5.sticky 粘性定位 基于用户的滚动位置来定位。粘性定位的元素是依赖于用户的滚动，在 position:relative 与 position:fixed 定位之间切换。它的行为就像 position:relative; 而当页面滚动超出目标区域时，它的表现就像 position:fixed，它会固定在目标位置。元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

div.sticky {
    position: -webkit-sticky; /* Safari */
    position: sticky;
    top: 0;
    background-color: green;
    border: 2px solid #4CAF50;
}

6.z-index 因为页面中元素的定位与文档流无关，所以定位的元素可以覆盖在文档流上面。所以z-index属性指定了一个元素的堆叠顺序（哪个元素应该放在前面/后面）。z-index的值必须取正整数，数值越大显示的优先级就越高。 如果两个定位元素重叠，而且还没有指定z - index，name最后定位在HTML代码中的元素将被显示在最前面。



## flex布局

- 弹性布局可以简便、完整、响应的实现各种页面上的布局。

- 与静态不同的是，使用em或rem单位（lem=16px，1rem=10px）进行相对布局，相对使用百分比更加方便、灵活，相应同时支持浏览器的字体大小调整和缩放的等正常显示。

- 优点：
  1.适应性强，在做多种不同的屏幕分辨率不同的界面是非常使用。
  2.随意按照宽度、比例划分元素的宽高。
  3.可以轻松的改变元素的显示顺序。
  4.网页布局实现快捷，维护起来更加容易。
- 如果做移动端时，如果客户对细微的之处的要求不高，使用弹性布局进行制作是最好的选择，一份css+一份js调节font-size搞定。
- 缺点： 浏览器兼容性较差，只能<u>兼容到IE9及以上</u>。

网页布局（layout）是 CSS 的一个重点应用。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071001.gif)

布局的传统解决方案，基于[盒状模型](https://developer.mozilla.org/en-US/docs/Web/CSS/box_model)，依赖 [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) 属性 + [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position)属性 + [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float)属性。它对于那些特殊布局非常不方便，比如，[垂直居中](https://css-tricks.com/centering-css-complete-guide/)就不容易实现。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071002.png)

2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071003.jpg)

Flex 布局将成为未来布局的首选方案。本文介绍它的语法，[下一篇文章](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)给出常见布局的 Flex 写法。网友 [JailBreak](http://vgee.cn/) 为本文的所有示例制作了 [Demo](http://static.vgee.cn/static/index.html)，也可以参考。

以下内容主要参考了下面两篇文章：[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 和 [A Visual Guide to CSS3 Flexbox Properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)。

### 一、Flex 布局是什么？

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。

> ```css
> .box{
> display: flex;
> }
> ```

行内元素也可以使用 Flex 布局。

> ```css
> .box{
> display: inline-flex;
> }
> ```

Webkit 内核的浏览器，必须加上`-webkit`前缀。

> ```css
> .box{
> display: -webkit-flex; /* Safari */
> display: flex;
> }
> ```

注意，设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效。

### 二、基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

容器默认存在两根轴：

​	水平的主轴（main axis）和垂直的交叉轴（cross axis）。

​	主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；

​	交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。



### 三、容器的属性

以下6个属性设置在容器上。

> - flex-direction
> - flex-wrap
> - flex-flow
> - justify-content
> - align-items
> - align-content

#### 3.1 flex-direction属性

`flex-direction`属性决定主轴的方向（即项目的排列方向）。

> ```css
> .box {
> flex-direction: row | row-reverse | column | column-reverse;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

它可能有4个值。

> - `row`（默认值）：主轴为水平方向，起点在左端。
> - `row-reverse`：主轴为水平方向，起点在右端。
> - `column`：主轴为垂直方向，起点在上沿。
> - `column-reverse`：主轴为垂直方向，起点在下沿。

#### 3.2 flex-wrap属性

默认情况下，项目都排在一条线（又称"轴线"）上。`flex-wrap`属性定义，如果一条轴线排不下，如何换行。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071006.png)

> ```css
> .box{
> flex-wrap: nowrap | wrap | wrap-reverse;
> }
> ```

它可能取三个值。

（1）`nowrap`（默认）：不换行。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)

（2）`wrap`：换行，第一行在上方。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

（3）`wrap-reverse`：换行，第一行在下方。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)

#### 3.3 flex-flow

`flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

> ```css
> .box {
> flex-flow: <flex-direction> || <flex-wrap>;
> }
> ```

#### 3.4 justify-content属性

`justify-content`属性定义了项目在主轴上的对齐方式。

> ```css
> .box {
> justify-content: flex-start | flex-end | center | space-between | space-around;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

> - `flex-start`（默认值）：左对齐
> - `flex-end`：右对齐
> - `center`： 居中
> - `space-between`：两端对齐，项目之间的间隔都相等。
> - `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

#### 3.5 align-items属性

`align-items`属性定义项目在交叉轴上如何对齐。

> ```css
> .box {
> align-items: flex-start | flex-end | center | baseline | stretch;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

> - `flex-start`：交叉轴的起点对齐。
> - `flex-end`：交叉轴的终点对齐。
> - `center`：交叉轴的中点对齐。
> - `baseline`: 项目的第一行文字的基线对齐。
> - `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

#### 3.6 align-content属性

`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

> ```css
> .box {
> align-content: flex-start | flex-end | center | space-between | space-around | stretch;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

该属性可能取6个值。

> - `flex-start`：与交叉轴的起点对齐。
> - `flex-end`：与交叉轴的终点对齐。
> - `center`：与交叉轴的中点对齐。
> - `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - `stretch`（默认值）：轴线占满整个交叉轴。

### 四、项目的属性

以下6个属性设置在项目上。

> - `order`
> - `flex-grow`
> - `flex-shrink`
> - `flex-basis`
> - `flex`
> - `align-self`

#### 4.1 order属性

`order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

> ```css
> .item {
> order: <integer>;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

#### 4.2 flex-grow属性

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

> ```css
> .item {
> flex-grow: <number>; /* default 0 */
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

#### 4.3 flex-shrink属性

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

> ```css
> .item {
> flex-shrink: <number>; /* default 1 */
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

#### 4.4 flex-basis属性

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

> ```css
> .item {
> flex-basis: <length> | auto; /* default auto */
> }
> ```

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

#### 4.5 flex属性

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

> ```css
> .item {
> flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
> }
> ```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

#### 4.6 align-self属性

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

> ```css
> .item {
> align-self: auto | flex-start | flex-end | center | baseline | stretch;
> }
> ```

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。



