---
title: canvas
date: 2020-09-23 21:43:00
tags:
	- canvas
	- html
	- front-end
---

# canvas

> - 用于绘制图像, 通常用javascript绘制

## canvas基本使用

### canvas表示使用

```
<canvas width="300" height="150">
	不支持canvas标签会显示该内容
</canvas>
```



### canvas方法检查支持性

```js
var canvas = document.getElementById("target")
if ( canvas.getContext ) {
  var ctx = canvas.getContext("2d")
}else{
 	console.log("该浏览器版本过低, 请更换")
}
```





## 矩形

```js
fillRect( x , y , width , height)  //填充以(x,y)为起点宽高分别为width、height的矩形 默认为黑色

strokeRect( x , y , width , height) //绘制一个空心以(x,y)为起点宽高分别为width、height的矩形

clearRect( x, y , width , height ) // 清除以(x,y)为起点宽高分别为width、height的矩形 为透明
```



## 路径

```js
beginPath() 新建一条路径一旦创建成功 绘制命令将转移到新建的路径上
moveTo( x, y ) 移动画笔到(x , y) 点开始后面的绘制工作
closePath() 关闭该路径 将绘制指令重新转移到上下文
stroke() 将绘制的路径进行描边
fill() 将绘制的封闭区域进行填充
```

## 圆弧

```js
arc( x , y , r , startAngle , endAngle ,  anticlosewise ) // 以(x,y)为圆心 r为半径的圆  绘制startAngle弧度 到endAngle弧度的圆弧 anticlosewise默认为false 即顺时针方向 true为逆时针方向

arcTo( x1 , y1 , x2 , y2 , radius ) //根据 两个控制点 (x1,y1) 和 (x2, y2)以及半径绘制弧线 同时连接两个控制点
```

## 曲线

### 一次贝塞尔曲线

> 就是一条直线

![](https://user-gold-cdn.xitu.io/2018/11/26/1674efc1d4d11922?imageslim)



### 二次贝塞尔曲线

```js
quadraticCurveTo( cp1x, cp1y , x ,y )   // (cp1x,cp1y) 控制点    (x,y)结束点
```

![](https://user-gold-cdn.xitu.io/2018/11/26/1674efc1f01a80fc?imageslim)



### 三次贝塞尔曲线

```js
bezierCurveTo( cp1x, cp1y ,cp2x , cp2y ,x , y )//（cp1x,cp1y）控制点1   (cp2x,cp2y) 控制点2  (x,y)结束点
```

![](https://user-gold-cdn.xitu.io/2018/11/26/1674efc1fdd312e3?imageslim)

## 样式添加

```
fillStyle = color
strokeStyle = color 
//color 可以为颜色值、渐变对象(并非样式！！！！)
lineWidth  = value  线宽
lineCap = type （butt 、 round 、square）线条末端样式   依次是方形、圆形&突出、方形&突出
```



![canvas8](https://user-gold-cdn.xitu.io/2018/11/26/1674efc200a1fb4e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



```
lineJoin = type （round 、bevel 、 miter）线条交汇处样式 依次是圆形、平角 、 三角形
```



![canvas9](https://user-gold-cdn.xitu.io/2018/11/26/1674efc203135b97?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



```
ctx.setLineDash([ 实际长度 , 间隙长度 ]) //虚线 setLineDash接受数组
ctx.lineDashOffet  //设置偏移量
```

### 渐变

```
var gradient = ctx.createLinearGradient( x1 ,y1 ,x2 ,y2); //线性渐变
var gradient = ctx.createRadialGradient(x1 ,y1 ,r1 ,x2 ,y2 ,r2);//径向渐变
gradient.addColorStop( position , color )// position:相对位置0~1    color:该位置下的颜色
```

### 透明度

```
ctx.globalAlpha = value (0~1)
```

## 文本

```
fillText( text , x , y , [,maxWidth]) 在(x,y)位置绘制text文本  最大宽度为maxWidth(可选)
strokeText( text ,x ,y ,[,maxWidth]) 在(x,y)位置绘制text文本边框  最大宽度为maxWidth(可选)

font = value               eg:"100px sans-serif"  
```

## 绘制图片

```
drawImage( image , x , y , width , height ) image为图片对象、从(x,y)处放置宽高分别为width height的图片
drawImage( image , sx , sy , swidth , sheight ,dx ,dy ,dwidth ,dheight) 切片前四个是定义图像源的切片位置和大小   后四个是定期切片的目标显示位置大小
```



![canvas10](https://user-gold-cdn.xitu.io/2018/11/26/1674efc21cdeb9b3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



## 状态保存 恢复

```
save()

restore()
```

## 动作

```
translate( x , y ) 将canvas原点的移动到 (x,y)     （save&restore保存初始状态！！！）

rotate( angle ) 顺时针方向旋转坐标轴 angle弧度

scale(x,y) 将图形横向缩放x倍、纵向缩放y倍   （ x、y大于1是放大  小于1为缩放！！！）
```

## 全局合成操作

globalCompositeOperation = type; 

source-over



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc2202ba9d7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas11" style="zoom:50%;" />



source-in



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc231836ca4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas12" style="zoom:50%;" />



source-out



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc230f9efee?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas13" style="zoom:50%;" />



source-atop



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc22fd95ad9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas14" style="zoom:50%;" />



destination-over



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc24023b46d?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas15" style="zoom:50%;" />



destination-in



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc24bb0268a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas16" style="zoom:50%;" />



destination-out



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc257a9972a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas17" style="zoom:50%;" />



destination-atop



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc257bf9efd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas18" style="zoom:50%;" />



xor



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc27398ea8a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas19" style="zoom:50%;" />



copy



<img src="https://user-gold-cdn.xitu.io/2018/11/26/1674efc272df1d1e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="canvas20" style="zoom:50%;" />



## 裁剪

```
clip //只显示裁剪区域内部区域  (使用save & restore 存储canvas状态！！！)
复制代码
```

## 动画

```
clearRect() 清空画布

save&restore 保存恢复canvas状态
复制代码
```

## 定时执行

- setInterval()
- setTimeout()
- requestAnimationFrame()


