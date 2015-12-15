# Typescript 语言简介

## 什么是Typescript?
Javascript是一种弱类型的语言，在开发一些小型项目，UI交互的时候很灵活，方便。
但是当项目变的庞大的时候，就显露出很明显的弊端。
设想你在重构一大堆老代码，没有单元测试。改了一段代码之后不在浏览器里面跑一跑还真的不敢确定是不是有问题。这通常是前端的一个痛点。
静态语言有比较强大的代码重构工具。一些很明显的问题能在编译阶段发现。

Typescript把类型带入了Javascript的世界。它是Javascript的超集，即所有合法的js都是Typescript。但是它可以有类型。
运行的时候Typescript被tsc编译器翻译成可读性很高的Javascript在浏览器执行。

### 如果有很多js代码，项目中不好上手怎么办？
虽然typescript给了你type的能力。不意味着给了你太多的限制。
好在它的类型是可选的。你完全可以全都写any类型。编译器会对该变量放弃类型检查。
即使类型匹配失败，仍然会生成javascript。你可以逐渐把js代码慢慢迁移到typescript上。

### 基本类型
Typescript提供了boolean, number, string, array, enum, any, void几种基本类型。

```typescript
var flag: boolean = true;
var s: string = 'hello';
var n: number = 123;

enum Color {Red = 1, Green, Blue};
var color: Color = Color.Green;

function log(msg: string): void {
	console.log(`${new Date().toUTCString()} ${msg}`);
}
```

## 类

类的语法和ES6的Class类似，有constructor，可以继承。这里列举几点不同。
### 属性声明
ES6的class属性是直接赋值给this.varName声明的，typescript里面需要显示声明。
```typescript
class Point{
	x: number;
	y: number;
}
```
### 构造函数属性声明
属性也可以在构造函数中添加public, private描述声明。
```typescript
class Point{
	constructor (public x:number, public y:number){}
}
```

### 支持public, private, static描述
ES6的static只支持在函数上声明，而typescript支持方法和属性。

```typescript
class Popup{
    static inst: Popup;
    constructor() {
        if (!Popup.inst) {
            Popup.inst = this;
        }
    }
    static getInstance() {
        return new Popup();
    }
}

Popup.getInstance();
```

## 函数
- 可选/默认参数
```typescript
function reset(hard?: boolean) {
	if (hard) {
		resetDB();
	}
	resetUI();
}
reset();
reset(true);


```


- 剩余参数

- 箭头函数
这点和ES6一致。箭头函数内部保持和外部一样的this上下文。

- 重载
## 模块


## 接口

# Generic #

Generic classes are only generic over their instance side rather than their static side, so when working with classes, static members cannt use the class's type parameter.

## Typescript工具

https://atom.io/packages/atom-typescript

https://github.com/DefinitelyTyped/DefinitelyTyped
