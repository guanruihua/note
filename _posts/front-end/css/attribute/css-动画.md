---
title: css-动画
date: 2020-10-09 15:19:48
tags: 
	- css
	- 动画
---

# css动画

## 浏览器渲染原理

[![0DhCRO.md.png](https://s1.ax1x.com/2020/10/09/0DhCRO.md.png)](https://imgchr.com/i/0DhCRO)

### 浏览器渲染过程

1. 根据html标记构建DOM树
2. 根据CSS构建css树(CSSDOM)
3. 将两棵树合并成一棵渲染树(render tree)
4. layout布局(文档流, 盒模型, 大小等)
5. paint绘制(边框颜色, 背景颜色等)
6. compose合成(根据层叠关系展示画面)

### 更新样式的三种方式

#### JS / CSS > 样式 > 布局 > 绘制 > 合成



![img](https://user-gold-cdn.xitu.io/2020/5/4/171dde4a96e82fe1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 根据浏览器的渲染原理，若是开发者**更新了样式**（即元素的几何属性，类似于宽高，位置等）
- 则浏览器会检查所有属性然后重新绘制，最后再合成。



#### JS / CSS > 样式 > 绘制 > 合成



![img](https://user-gold-cdn.xitu.io/2020/5/4/171dde4fe149e0a2?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 如果开发者只是更新了`paint only`的属性（例如背景，文字颜色等）
- 由于不影响页面布局，则浏览器直接执行绘制。



#### JS / CSS > 样式 > 合成



![img](https://user-gold-cdn.xitu.io/2020/5/4/171dde5405781ebe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 在开发者只是更改**一个既不更改布局也不需要绘制的属性时**，
- 浏览器将只执行合成，例如动画和`transform`。

## CSS动画(transform, transition, animation)

### transform

> `transform: translate(位移)|scale(缩放)| rotete(旋转)| skew(倾斜)`
>
> - 不支持inline元素, 使用时候需要变成block

```css
transform:translate(x,y);
transform:translateX(x);
transform:translateY(y);
transform:translateZ(z);/*需要在父容器上加上perspective元素 */
transform:translate3d(x,y,z);
```



#### scale

```css
transform: scaleX(x);
transform: scaleY(y);
transform: scale(x, y);
transform: scale(整数放大倍数);
```

#### rotate

> 旋转

```css
rotate([<angle>|<zero>])
rotateZ([<angle>|<zero>])
rotateX([<angle>|<zero>])
rotateY([<angle>|<zero>])
```



#### skew

> 歪斜

```css
skewX([<angle>|<zero>])
skewY([<angle>|<zero>])
skew(([<angle>|<zero>],[<angle>|<zero>]? )
```



### transition

> 语法: `transition:属性名 时长 延迟 => transition; left 200ms linear 2s`
>
> - 可以使用`all`表示所有属性, 常用过渡方式: `linear(匀速), ease(缓慢), ease-in(淡入), ease-out(淡入),ease-in-out(淡入淡出)`
> - 不是所有元素都可以使用过渡的: 
>   - `display:none <--->display: block;`, 一般使用`visibility:visible<--->visibility: hidden;`实现元素的显示和隐藏



### animation

- keyframes的写法

```css
@keyframes 属性名 {
    from{
        transform:translate(20px,30px);
    }
    }
    to{
    transform:translate(30px,40px);
    }
}
复制代码
```

```css
@keyframes 属性名{
    0%{
        
    }
    50%{
        
    }
    100%{
        
    }
}
```

- animation写法

animation:属性名 时长 过度方式 延迟 次数 方向 填充模式 是否暂停;

1. 过渡方式同transition,linear,ease...
2. 次数：3 ，2.4或infinite
3. 方向：reverse（反向），alternate（交替），alternate-reverse（反向交替）
4. 填充模式：both，forwards（forwards可以让动画停在结尾处），backwards，none
5. 是否暂停：pause,running
6. 时长：1s，100ms















