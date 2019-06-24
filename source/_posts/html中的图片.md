---
title: html中的图片
date: 2019-06-24 09:24:11
tags: css
---

## img 标签

> 在html中,img元素是 属于replaced element(简称re)的一种, replaced element 元素是一种**表现**不完全受css控制的元素。简而言之，这些元素本身的样式，位置可以通过css控制，但是元素的**内容**却不受css的影响。以img元素为例，img这个元素在html文档中的大小，位置，等等可以通过css控制，但是img的内容就是加载的图片内容是不受css的影响的。

> css3 中有两个属性 object-fit / object-position 是用来处理replaced element 内容的表现，前者控制缩放，后者控制位置。

## object-fit 
> 该属性是用来表示 re元素的内容的 长宽如何适应 re元素本身。

> 以img元素为例说明:

1. object-fit:fill; // 图片填充整个img区域，图片本身长宽比和img长宽比不一致时，图片做拉伸处理，结果就是图片本身的长宽比有可能变化。


2. object-fit:contain; // 图片本身保持自身的长宽比，同时要在img容器中显示全部的图片内容，有可能图片就会缩放。

3. object-fit:cover; // 图片在保持自身长宽比的同时，填充满整个img的content-box区域，为此，图片有可能会缩放，那么超出content-box的部分就被修剪


## object-positioin
> 该属性是用来设置re元素内容相对于content-box 的位置， 值为 position 的数据类型。
![position](/images/Snipaste_2019-06-24_11-14-58.png)



## 实例应用
> 在微信公众号开发中，有个需求是利用wx-jssdk提供的图片api来调用手机的相册获取手机中的图片，添加到页面中并且提供本地预览的jsapi接口，可以直接本地预览图片。

> 具体做法:
1. 因为手机中的图片长宽都不确定的，而且如果是调用手机摄像头拍照，有横拍竖拍等等，总之图片规格尺寸不一。
2. wx-jssdk提供的选择手机图片的接口，是返回一个id值，这个id直接复制给img的src就可以预览图片，所以img元素的长宽是固定的，为了使图片显示不拉伸变形覆盖全部的content-box。
3. object-fit:cover; object-position:center;





