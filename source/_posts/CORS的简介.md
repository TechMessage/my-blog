---
title: CORS的简介
date: 2019-07-04 23:57:32
tags:  CORS
---
## 学习顺便翻译
[MDN原文](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)


## 概述
> CORS (cross-origin resources sharing) (跨域资源共享) 是一机制：可以在http请求中的headers中添加字段来然浏览器获取访问跨域资源的能力。

1. 是一种机制
2. 浏览器的行为
3. 解决的是跨域访问资源问题
4. 主要是后端的接口相应要设置相应的header 字段： Access-Control-Allow-Origin

> 前提

Q:  何为跨域？  
A:  a网站的客户端页面脚本中 访问了b网站的资源； a和b不同域名，不同端口，不同协议，三者满足其一视为跨域   

Q:  为何需要解决跨域问题？  
A:  出于安全的考虑，浏览器默认是进制客户端脚本跨域访问资源，XMLHttpRequest遵循[同源策源](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) 

Q:  cors解决了啥？  
A:  基于上面的问题，cors的机制就是在response的headers中添加特定的字段，允许不同域的客户端访问


Q:  需要用到cors的http请求资源的类型？ 
```
A:  1.基于XMLHttpRequest的ajax请求
    2.css中@font-face引入别人的字体
    3.WebGL texture
    4.canvas 调用 drawImage() 

```







