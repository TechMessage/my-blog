---
title: typescript
date: 2019-07-24 09:43:02
tags: ts
---

# typsescript学习笔记
### [官网文档](http://www.typescriptlang.org/docs/handbook/basic-types.html)

> typecript是js的超集，不是新的语言，需要编译为js文件才可以在浏览器或者Node端执行


## 5分钟快速上手

1. 安装
>  npm  install -g typescript

2. 代码
```

// hello.ts
function greeter() {
    console.log('hello, world')
}

greeter()

```

3. 编译
> tsc hello.ts  ==> 生成 hello.js

## handbook
> 基本操作手册


### Basic Types 基本类型
> typescript支持所有js中数据类型，

1. boolean 类型
```
let isDone:boolen = false;
```

2. number 
>  在js中所有的数字类型都是浮点数，统一为number类型
```
let a:number = 10
let b:number = 0xfa11 //16进制
let c:number = 0b1010 //2进制
let d:number = 0o744 //8进制

```
3. string
```
let s:string = 'hello world'
```

4. array
> ts中的数组，限定了数组元素的类型
```
let list:number[] = [1,2,3]; //限定了数字类型数据，数组内元素只能为数字
let list:Array<number> = [1,2,3]; //限定了数字类型数据，数组内元素只能为数字
```

5. tuple 元组类型
> 限定长度和每个索引位置元素的类型的数组
```
let x:[string, number] = ['1', 2]
```

6. enum 枚举类型
> ts中的枚举类型类似map，定义一组一一对应key-value对应关系，包装起来
```
enum Code {
    SUCCESS = 1002,
    ERROR = 1003,
    EXCEPTION = 1004
}

let c: Code;

switch (c) {
    case Code.SUCCESS:
        
        break;
    case Code.ERROR:

        break;
    case Code.EXCEPTION:

        break;

    default:
        break;
}
```
