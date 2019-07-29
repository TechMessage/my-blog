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

7. any 任意类型，动态类型
> ts在个js中添加了变量类型检查的同时，也提供了一个any的类型，这个类型就和js中的变量是相似的，动态类型；相当于以一方面给js提供个变量的静态类型特性，另一方变也保留了js的动态特性。

8. void 空类型
> void 类型用来表达函数没有返回值的情况

```
function warnUser(): void {
    console.log("This is my warning message");
}
```

9. null , undefind 类型

> null类型 只有一个值null; undefined类型也只有一个值undefined。这两个类型单独作用不大，这两个类型默认是其它类型的子类型，意味着其它类型可以赋值null或undefined。

10. never 类型

> 这个类型用来 表示当某个函数中直接抛出异常时，返回值类型，或者一个函数陷入无限循环中，不会终止

```
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(message);
}

// Inferred return type is never
function fail() {
    return error("Something failed");
}

// Function returning never must have unreachable end point
function infiniteLoop(): never {
    while (true) {
    }
}

```

11. object 类型

> object 类型不是原始数据类型


12. type assertions 类型断言（类型转换)

> 你可以对确定的类型进行类型转换，有两种语法
```
// 1 
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;

// 2 
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;

```


### Variable Declaration 变量声明

> let 和 const在es6中引入的关键字用来声明变量和常量,后者声明变量只能赋值一次，不能二次赋值。在es6之前只有var关键字是用来声明变量的，var声明变量有一些不好的特性，会给代码编写造成误导，特别是变量提升的特性。

* var 声明变量

> 首先明确的是变量作用域仅仅和变量的声明有关，于函数的执行上下文无关;只有全局和函数才能形成作用域，变量的访问是从当前函数中以此往上层函数递归直至到全局的顺序。

```
var a = 12

function f() {
    var message = "Hello, world!";
    return message;
}

```
> 全局声明的a变量，它的作用域就是全局的，在任何地方都可以访问；函数f中声明的变量message，它的作用域仅仅在函数中，换句话中在函数f中才可以使用变量message。


* 闭包
> 闭包简而言之就是夸作用域访问变量的能力
```
function f() {
    var a = 10;
    return function g() {
        var b = a + 1;
        return b;
    }
}

var g = f();
g(); // returns '11'
g = null; //释放闭包内存
```
> 分析上面代码: 函数f中声明了变量a和函数g, g函数中访问到a变量，并且g函数作为f函数返回值；在全局执行f()调用，将返回值赋值给全局的g变量，全局的g变量就可以访问到函数g中的a变量。其实从变量作用域的角度来看，a变量的是函数f中声明的，它的访问应该仅仅局限在函数f中，但是通过将f中的g返回出去，其中g中访问了a，那么相当于将a给暴露出去了。这就形成了闭包的过程。a变量的内存始终没有释放掉，因为它需要被全局的g访问到，那么可以全局的g执行完后，手动赋值null，那么就可以释放了。

```
for (var i = 0; i < 10; i++) {  
    setTimeout(() => {
        console.log(`${i}次循环`, i)
    }, 10);
}


// 上面的for循环代码块等价于

var i;
for(i = 0; i<10;i++){
    .....
}

// var 声明变量都是有变量提升的，而且没有块的概念，存在于函数中或全局中
// setTimeout是异步执行的，所以只有在for循环都执行完了，才会执行setTimeout中的函数，此时i=10


```
> 上面的代码在执行时输出都是10，因为var 声明的变量是函数的，不是在for循环的这个代码块中的


> 因为var 声明变量带来的诸多问题，所以在es6中引入了新的关键字let const 来声明变量

1. let 声明变量是块级别的，block scope ,哪些是代码块呢？for循环，if-else, try..catch 简言之就是带有{ }的
2. 也没有变量提升的特性,意味着不能先使用后声明，这里的先后是代码的顺序
3. 不能重复声明相同的变量，在一个代码块中


### interface
> typescript相较于js最明显的就是变量的类型检查机制，那么interface就是ts中用来解决变量的类型定义的，准确来说是对象类型的数据的类型声明的

1. 声明某个对象
```
interface People {
    name: string,
    age: number
}

```
> 声明一个People类型的对象，包含两个必要的属性name,age而且只能包含这两个属性

2. 如果对象中的某个属性可有可无，那么对应的属性后跟?
```
interface People {
    name: string,
    age: number,
    job?:string
}

```

3. 如果对象中某个属性值是readonly的，不能改写，那么在属性前带上readonly

```
interface People {
    readonly sex: string,
    name: string,
    age: number,
    job?: string,
}
```

4. interface 来定义函数接口,只需要函数的签名（参数列表及参数类型和返回值类型）
```
interface getFullname {
    (first: string, last: string): string
}
```


5. interface可以描述 索引类型的对象，意思是一个数组的访问方式，通过索引来访问值，但是需要规定索引的类型和值得类型;如果索引类型是number，那么意味着可以用数组或者对象来赋值给这个interface的变量，如果索引类型是string，那么只能是数组类赋值。

```


interface my {
    [index: number]: string
}

let l: my = {
    1: '1',
    2: '2'
}

let m: my = ['1', '2', '3']


interface you {
    [index: string]: string
}

let y: you = {
    1: '1',
    2: '1',
    3: '1'
}
```

6. interface 描述类
```
interface ClockInterface {
    currentTime: Date;
}

class Clock implements ClockInterface {
    currentTime: Date = new Date();
    constructor(h: number, m: number) { }
}

```

### class

> js是基于原型继承，这一点没有变，class的写法只是一种语法糖

```
class Person {
    name: string  // 成员属性
    constructor(name: string) {  //构造函数
        this.name = name
    }
    getName() {   //原型方法
        return this.name;
    }
}

```
> class的继承通过extends 显示声明，并且需要在子类的构造器中首先执行super()来执行父类的构造器









