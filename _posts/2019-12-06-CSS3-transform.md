---
layout:     post
title:      CSS3-transform
subtitle:   CSS3-transform
date:       2019-12-06
author:     limantang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - CSS
---

# CSS3变形-transform

## 简介
CSS3变形是一些效果的集合, 比如位移, 旋转, 缩放, 倾斜, 每个效果都称为变形函数(**transform-function**)

## CSS变形属性及函数
CSS变形变形允许动态的控制元素, 可以在屏幕周围移动它们, 缩小或者扩大, 旋转, 或者结合起来产生复杂的动画效果
通过CSS变形, 可以让元素生成静态的视觉效果
也可以很容易的结合CSS3的transition和动画的keyframe产生动画效果

CSS3变形中具有X / Y可用的函数

- `tanslateX()`, `translateY()`
- `scaleX()`, `scaleY()`
- `skewX()`, `skewY()`

CSS3 2D变形函数包括:
- `translate()`  接受CSS度量单位
- `scale()`  接受十进制数
- `rotate()`   接受deg角度
- `skew()`  接受deg角度
- `matrix()` 接受6个参数

CSS3 3D变形函数包括
- `rotateX()` X轴的旋转
- `rotateY()` Y轴的旋转
- `rotate3d()`  接受三个参数 分别对应XYZ三个轴的方向
- `translateX()` X轴的移动
- `translateY()` Y轴的移动
- `translate3d(tx, ty, tz)`  接受三个参数 分别对应XYZ三个轴的方向
-  `translateZ()` Z轴的移动, 相当于`translate3d(0, 0, tz)`
- `scaleZ()` Z轴方向的缩放
- `scale3d()`  接受三个参数 分别对应XYZ三个轴的方向
- `matrix3d()`  接受16个参数

理解3D变化的关键一定要在脑中形成三维坐标系
可以简单地认为眼睛垂直屏幕的方向就是Z轴
屏幕中心向左就是X轴
屏幕中心向下就是Z轴

## CSS变形属性
`transform`属性指一组转换函数
`transform-origin`属性指定元素的中心店在哪
`transform-style`2D 3D渲染环境相关

### transform
语法如下
`transform: none | transform-function [transform-function]*`
默认值为none  不进行变形
transform-function  变形函数, 可以添加多个, 多个使用空格分隔

### transform-origin
`transform-origin: offset | x-offset y-offset`
支持百分比, 或者`top left bottom right`这样的值
默认是变形元素的中心
设置变形的中心点
特别注意的是`translate`的变形中心点不受这个值得影响, 只能是元素的中心

### transform-style
`transform-style: flat | preserve-3d`
默认值是`flat ` 处于2D空间中
`preserve-3d`设置元素的所有子元素都处于3D空间中
其实这个属性的作用就是创造3D空间, 3D舞台元素
想要实现3D效果, 这个属性一般都应该设置为`preserve-3d`

### perspective
这个属性设置视角的位置, 可以简单的理解为视距
这个值越大会感觉用户离3D空间Z平面越远, 反之越近
`perspective: 1200px`
假设现在你的显示器上有一张人物图片, 显示器是1000像素宽的显示器
以你的眼睛为视点, 眼睛到显示器的距离就是1.2倍的显示器宽度
那么这张人物图片的3D效果就和你站在1.2个显示器宽度的举例看到的真实效果一致

`perspective`有两种写法
- 可以设置在共同的舞台元素上
- 还可以直接设置在需要变形的元素上

这两种写法是有很大差异的, 最大的差异就是选择哪个元素作为透视元素

### perspective-origin
设置perspective的位置
默认是50% 50%
通过上面的例子来说, 如果是默认值的话
你眼睛(视点)的位置正好在屏幕的中央

### backface-visibility
决定元素绕Y轴旋转180度之后是否可见, 默认是可以
`backface-visibility: visibile | hidden`


这是一个3D正方体的例子

**github地址**
[blog-source-code/index.html at master · neo-to/blog-source-code · GitHub](https://github.com/neo-to/blog-source-code/blob/master/src/css-transform/index.html)

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible” content=“ie=edge”>
  <title>transform示例</title>
  <style>

    @keyframes rotateXYZ {
      0% {
        /* transform: rotate3d(0, 0, 0, 0); */
        transform: rotateX(0) rotateY(0) rotateZ(0);
      }
      100% {
        /* transform: rotate3d(1, 1, 1, 360deg); */
        transform: rotateX(360deg) rotateY(360deg) rotateZ(360deg);
      }
    }
    body {
      padding: 300px;
    }
    .stage-3d {
      perspective: 300px;
      position: relative;
      width: 200px;
      height: 200px;
      /* perspective-origin: 200% -100%; */
      perspective-origin: 50%;
    }
    .cube {
      width: 100%;
      height: 100%;
      margin-top: 100px;
      position: relative;
      transform-style: preserve-3d;
      transform: translateZ(-20px);
      animation: rotateXYZ 10s linear infinite;
    }
    .plane {
      height: 200px;
      width: 200px;
      color: #fff;
      border: 1px solid #999;
      position: absolute;
      opacity: .5;
      text-align: center;
      padding: 90px 0;
      box-sizing: border-box;
    }
    .front {
      transform: translateZ(100px);
      background:red;
      opacity: .5;
    }
    .backend {
      transform: translateZ(-100px);
      background:red;
    }
    .left {
      background: blue;
      transform: rotateY(-90deg) translateZ(100px);
    }
    .right {
      background: blue;
      transform: rotateY(90deg) translateZ(100px);
    }
    .bottom {
      background: green;
      transform: rotateX(-90deg) translateZ(100px);
    }
    .top {
      background: green;
      transform: rotateX(90deg) translateZ(100px);
    }

    
  </style>
</head>
<body>
  
  <div class=“stage-3d”>
    <div class=“cube”>

      <div class=“plane top">top</div>
      <div class="plane bottom">bottom</div>
      <div class=“plane left”>left</div>
      <div class=“plane right">right</div>
      <div class=“plane backend”>backend</div>
      <div class=“plane front”>front</div>
  
    </div>
  </div>
</body>
</html>
```

总结一下通过这个例子学到的几个知识点

- 舞台元素和容器元素分开设置
- 舞台元素只设置视距(perspective)
- 容器元素必须设置`transform-style: preserve-3d`, 否则看不到3d效果
- 容器元素要包含宽高
- 正方体6个面(宽高200px)最开始要放到同一个位置
- 前后两个面通过`translateZ`分别前移100px后移100px
- 左边的面绕Y轴逆时针旋转90度, 此时这个面由和屏幕垂直, **注意这个面的坐标轴也会发生转动**, 所以此时这个面的Z轴相当于没旋转之前的X轴,  所以需要`translateZ(100px)`来移动到左面的位置, 而不是用`translateX`
- 注意`rotate`和`translate`操作顺序
- 其他的几个面原理相同
- `translateZ`很重要, 一定要理解这个操作的意义

这个是一个六面体旋转的例子

[blog-source-code/index.html at master · neo-to/blog-source-code · GitHub](https://github.com/neo-to/blog-source-code/blob/master/src/css-transform/index.html)

```html
<!DOCTYPE html>
<html lang=“en”>
<head>
  <meta charset=“UTF-8”>
  <meta name=“viewport” content=“width=device-width, initial-scale=1.0”>
  <meta http-equiv=“X-UA-Compatible” content=“ie=edge”>
  <title>transform示例</title>
  <style>
    @keyframes zhuanquan {
      0% {
        transform: rotateY(0)
      }
      100% {
        transform: rotateY(360deg);
      }
    }
    .stage-3d-liumian {
      perspective: 800px;
      width: 200px;
      height: 200px;
    }
    .liumian {
      width: 100%;
      height: 100%;
      transform-style: preserve-3d;
      animation: zhuanquan 15s linear infinite;
    }
    .item {
      height: 200px;
      width: 200px;
      color: #fff;
      border: 1px solid #999;
      position: absolute;
      opacity: .5;
      text-align: center;
      padding: 90px 0;
      box-sizing: border-box;
    }
    .one {
      transform: rotateY(0) translateZ(181.4px);
      background:red;
    }
    .two {
      transform: rotateY(60deg) translateZ(181.4px);
      background: green;
    }
    .three {
      transform: rotateY(120deg) translateZ(181.4px);
      background: blue;
    }
    .four {
      transform: rotateY(180deg) translateZ(181.4px);
      background:red;
    }
    .five {
      transform: rotateY(240deg) translateZ(181.4px);
      background: green;
    }
    .six {
      transform: rotateY(300deg) translateZ(181.4px);
      background: blue;
    }

    
  </style>
</head>
<body>
 

  <div class="stage-3d-liumian”>
    <div class=“liumian">

      <div class=“item one”>1</div>
      <div class="item two”>2</div>
      <div class=“item three”>3</div>
      <div class=“item four">4</div>
      <div class="item five">5</div>
      <div class=“item six”>6</div>
  
    </div>
  </div>
</body>
</html>

```
