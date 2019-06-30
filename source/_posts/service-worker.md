---
title: service worker
date: 2019-06-30 22:19:57
tags: js
---

## web worker

> web workder 是一种简单的方式来执行脚本(在主线程之外)，worker线程可以执行一些任务而不会影响到用户的的交互，因为worker不是在主js线程执行的。

> workder的执行上下文环境是 DedicatedWorkerGlobalScope或者SharedWorkerGlobalScope，不是window。 在worker线程你可以执行任意的代码，除了不能操作dom,也不能使用window下的属性和方法，毕竟上下文环境不是window

> 在主js线程和worker线程之间数据的传输是通过message system(消息系统)， 通过postMessage()方法来传递数据，通过onmessage 事件来监听消息。


> worker 反过来也可以 生成新的worder,只要这些worker是被通过一个父页面的管理的同源的。通过worker是可以使用ajax来做network的请求的


## dedicated workders

> dedicated worker(专一 worker), 这种worker只能在它的执行脚本中访问它本身，其它脚本不能访问。

