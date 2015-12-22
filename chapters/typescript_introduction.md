## 什么是Typescript?
Javascript是一种弱类型的语言，在开发一些小型项目，UI交互的时候很灵活，方便。
但是当项目变的庞大的时候，就显露出很明显的弊端。
设想你在重构一大堆老代码，没有单元测试。改了一段代码之后不在浏览器里面跑一跑还真的不敢确定是不是有问题。这通常是前端的一个痛点。
静态语言有比较强大的代码重构工具。一些很明显的问题能在编译阶段发现。

Typescript把类型带入了Javascript的世界。它是Javascript的超集，即所有合法的js都是Typescript。但是它可以有类型。
运行的时候Typescript被tsc编译器翻译成可读性很高的Javascript在浏览器执行。

### 如果有很多js代码，项目中不好上手怎么办？
虽然typescript给了你type的能力。不意味着给了你太多的限制。
1. 它支持自动类型推断。一些很明显的类型，编译器可以智能推断出来，比如。**var x = 1;**
2. 好在它的类型是可选的。你完全可以全都写any类型。编译器会对该变量放弃类型检查。
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
可变数目的参数需要使用剩余参数的写法。获得的参数将是一个数组。
```typescript
function max(...nums: number[]) {
	...
}
```

- 箭头函数
这点和ES6一致。箭头函数内部保持和外部一样的this上下文。
```typescript
var Scheduler = {
	queue: [],
	schedule(t: Task) {
		setTimeout(()=> {
			this.queue.push(t);
		}, 0);
	}
};
Scheduler.schedule(new Task());
```

- 重载
js函数支持不同的参数进行重载。例如jquery的css函数
```typescript
css({
	width: '100px'
})
css('width', '100px')
```
可以这样调用。我们可以为该函数声明重载。
```typescript
function css(config: object);
function css(config: string, value: string);
function css(config: any, value?: any) {
	if (typeof config == 'string') {
		...
	} else if (typeof config == 'object') {
		...
	}
}
```
这个函数有两个重载，编译器会判断参数类型是否符合其中一个。

- 装饰器(decorator)

Typescript的装饰器和ES6里面的一致。可以修改已有的类或类的方法，也可以在它们的基础上提供一层封装。
Angular2里面大量使用装饰器，为组件注册元数据。

1. 类的装饰器

我们先来看看类的装饰器，以下面类的装饰器为例：

```typescript
@decorator
class A {}
```

这段代码其实等同于

```typescript
class A {}
A = decorator(A) || A;

function decorator(klass) {
	klass.meta = 'my awesome class';
}
```

Angular里面的装饰器可以传入meta信息，如下：

```typescript
@Component({
	selector: 'my-app'
})
class MyApp {

}
```

Component其实是angular库里面实现的一个装饰器工厂，接受一个meta信息，返回一个装饰器。类似如下实现：

```typescript
function Component(meta) {
	return function (klass) {
		...
	};
}
```

2. 类的方法的装饰器。

还有一种装饰器是类的方法的装饰器。

```typescript
class Person {
	@readonly
	name() { return `${this.first} ${this.last}` }
}
```

以上readonly方法将被如下的方式调用。

```typescript
function readonly(target, name, descriptor){
	descriptor.writable = false;
	return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// descriptor对象的初始值如下
// {
//   value: oneFunction,
//   enumerable: false,
//   configurable: true,
//   writable: true
// };
```

可惜的是由于函数存在提升，没有函数的装饰器。


## 模块
Typescript模块包括内部模块和外部模块两种。

### 内部模块
内部模块创建一个封闭的作用域，供同一个js文件内的代码使用。
(也可以使用 **/// <reference path="utils.js"/>** 引入其他文件的内部模块。)

```typescript
module com.gf.Utils{
	export function foo(msg:string){
		alert(msg);
	}
	export var name = 'some random tools';
}

import Utils = com.osamu.Utils; // alias
Utils.foo('hi')
Utils.name = 'Jack';
```

### 外部模块

外部模块和ES6的模块类似。使用外部模块和文件夹结构，保持合理的组织结构是大型项目必备的。
编译时可以为 *--module* 参数提供 *commonjs*, *amd*, *umd*, *systemjs* 几个值，选择编译为几种模块格式，供不同的加载器使用。
```typescript
// mylib.ts
export function log(msg){
	console.log(msg);
}

// app.ts
import {log} from 'mylib';
log('Hello, world!');

// 可以使用 `tsc --module amd main.ts` 编译
```

## 接口

typescript和其他解释性语言采取了类似的类型系统，duck typing。它听起来像鸭子看起来像鸭子就是鸭子。
而这个类型有可以由接口来描述。它强大到可以描述js内一切东西。

```typescript
interface Name {
    first: string;
    second: string;
}

var name: Name;
name = {
    first: 'Jim',
    second: 'Raynor'
};

name = {           // Error : `second` is missing
    first: 'Jim'
};
name = {           // Error : `second` is the wrong type
    first: 'Jim',
    second: 1337
};
```
第二个和第三个name对象由于却少相应的属性抛出类型不匹配的错误。


### 更多接口描述
Interface可以支持更为复杂的对象描述，如：

```typescript
interface FooType {
	(arg: string):void;	// 可以被当作函数调用 myFunc('hello');
	new (): Object; // 可以被当作构造函数 new myFunc();
	[idx:number]:string; // 支持下标 myFunc[3];
	name: string; // 支持属性 myFunc.name
	name?: number; // 可选属性
	id: string|number // 属性可以是某一种类型
	innerFunc():void; // 成员函数 myFunc.innerFunc();

};

```

### type别名
类型可以通过type关键字声明别名，比如：

```typescript
type StrOrNum = string|number;
type Record = [number, string];
```

### 周围声明
使用Typescript的项目如果需要整合大量已经存在的js代码，需要相应的js库的 *.d.ts* 类型定义文件。

并在引用的文件中声明类型依赖。
```typescript
/// <reference path="node.d.js"/>
```

实在太懒的话，也可以使用
```typescript
declare var process:any;
```
使typescript放弃对外部依赖库的类型校验。

很多常见的库的.d.ts文件开源项目DefinitelyTyped上人已经贡献了，详见下章。

## 泛型(Generic)

泛型是为了提升代码的复用性而开发的，与Java，C#中的泛型类似。
比如我们有个最小堆算法，需要同时支持number和string。这样可以把集合类型改为any。这样就完全放弃了类型检查。
这样实现有很大的瑕疵，而使用泛型解决更为优雅。
我们可以声明一个最小堆适用于number类型 *new MinHeap<number>()* ，
然后声明一个最小堆适用于string类型 *new MinHeap<string>()* 。
类似如下的泛型类：

```typescript
class MinHeap<T> {
    list: T[] = [];
    add(element: T): void {
		...
    }
    min(): T{
        return this.list.length ? this.list[0] : null;
    }
}

var heap1 = new MinHeap<number>();
heap1.add(3);
heap1.add(5);
console.log(heap1.min());

var heap2 = new MinHeap<string>();
heap2.add('a');
heap2.add('c');
console.log(heap2.min());
```

泛型也支持函数。下面zip函数声明了两个泛型类型`T1` `T2`，并把两个数组压缩到一起。


```typescript
function zip<T1, T2>(l1: T1[], l2: T2[]): [T1, T2][] {
    var len = Math.min(l1.length, l2.length);
    var ret = [];
    for (let i = 0; i < len; i++) {
        ret.push([l1[i], l2[i]]);
    }
    return ret;
}
console.log(zip<number, string>([1,2,3], ['Jim', 'Sam', 'Tom']));
```

## Typescript工具
### tsconfig.json
tsc编译器有很多命令行参数，但是都写在命令行上十分繁琐。于是有了 *tsconfig.json* 文件。
当运行 *tsc* 时，编译器从当前目录向上搜索 *tsconfig.json* 文件加载配置，类似于 *package.json* 文件的搜索方式。

我们可以从一个空的tsc文件开始。

```json
{}
```
tsc有合理的默认设置，空的json运气好的话也work。
下面是一个更为复杂的angular环境用的tsc配置。

```json
{
  "compilerOptions": {
    "target": "ES5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules"
  ]
}
```

###DefinitelyTyped
在使用第三方非typescript开发的库的时候，会需要 *.d.ts* 外部接口描述文件。
幸运的是很多这样的描述已经被开发了，并开源在 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
可以使用tsd工具，方便的安装.d.ts文件。
首先安装tsd工具

```bash
npm install tsd -g
```

然后安装 *d.ts* 文件
```bash
tsd install jquery --save
```

###编辑器
typescript可以有非常强大的类型提示。官方推荐VS作为typescript的编辑器，可惜VS对前端开发童鞋实在不习惯。
喜欢IDE的可以试试WebStorm或atom。atom的插件 [atom-typescript](https://atom.io/packages/atom-typescript) 很不错。
