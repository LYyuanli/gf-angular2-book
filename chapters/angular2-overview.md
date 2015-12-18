## Angular2 Overview

```bash
草稿
先是引言 （承前启后）
然后就用官方的架构讲解7大概念，最后是其他小概念。
加入中文示例图片
```

### 引言
Angular 2 是一个帮助我们用 html 和 javascript 构建客户端程序的开发框架。 框架有几个相互配合的库组成，有些是核心库有些是可选的库。
我们的application应用程序由：
- 使用Angularized模板创作HTML模板
- 书写组件类来管理模板
- 利用services添加应用逻辑
- 用Angular's boostrapper 来启动top root 组件

启动后的Angular程序，在浏览器中展示应用内容，通过我们的提供的指令来响应用户的交互。
我们在高纬度通过俯视看这些坐标型的概念来获得全局认识，详细的讲解会在后续的章节逐步开展。
一个Angular2的应用程序一般有以下7个主要的部分组成：

`<Todo: 图>`


### 组件
一个组件控制着一部分我们称之为view的屏幕内容。应用外围包含导航链接的壳，heroes 列表，hero 编辑器等，他们全是被组件component控制的视图。
我们在一个类中定义组件的应用逻辑来支持视图的展示，通过一系列的熟悉和方法的API定义，组件类来和view视图做交互

列入， HeroListComponent，拥有heros属性，它是通过一个服务返回heros数据的数组。同时，它也有 selectHero() 方法来设置 selectedHero 属性，当用户在列表中点击一个具体hero时。这样component类的如下：

```js
export class HeroListComponent {
  constructor(service: HeroService) {
    this.heroes = service.getHeroes();
  }
  heroes:Hero[];
  selectedHero:Hero;
  selectHero(hero: Hero) { this.selectedHero = hero; }
}
```

当用户在应用程序中移动浏览时，angular 会创建，更新，销毁组件。当然我们开发者可以通过 lifecycle hooks 钩子在组件的生命周期的关键时间点插入特定的处理


### 模板
我们通过component相应的template来定义它的视图。template就是以html的形式告诉Angular如何渲染component
绝大部分的模板看起来很像html，除了部分特殊的语法。以下是我们的HeroList组件的模板

```html
<h2>Hero List</h2>
<div *ng-for="#hero of heroes" (click)="selectHero(hero)">
  {{hero.name}}
</div>
<hero-detail *ng-if="selectedHero" [hero]="selectedHero"></hero-detail>
```

`<h2>`和`<div>`的标签我们很熟悉了，但是*ng-for, {‌{hero.name}}, (click), [hero], 和 `<hero-detail>` 是什么鬼。它们是Angular的模板语法的一部分， 我们在后续学习中会慢慢熟悉它们。
我们先把注意力集中在最后一行。 `<hero-detail>` 标签个代表HeroDetailCopment的自定义元素。



### 元数据（标注）
metadata，告诉angular如何处理一个类
我们现在回头看下之前定义的 HeroListComponent 的代码，我们发现它仅仅就是一个类，没有什么痕迹标明它是什么框架，或是angular相关的。
事实上如果我们不告诉angular它是一个component的话，从代码上看它就仅仅是一个普通的class
我们通过 metadata 告诉 angular 这段代码是指 HeroListComponent 组件定义
在 typescript 中最简单是通过decorator装饰器来附加 metadata 信息。 这是 HeroListComponent 的metadata例子

```js
@Component({
  selector:    'hero-list',
  templateUrl: 'app/hero-list.component.html',
  directives:  [HeroDetailComponent],
  providers:   [HeroService]
})
export class HeroesComponent { ... }
```
装饰器就是一个方法，所以装饰器一般也有配置参数。 @Component 装饰器就需要一个配置对象来给angular提供如何创建和展示组件和它对应视图的信息。

我们在看下其他可能的 @Component 配置选项：
selector:
templateUrl:
directives:
providers: 是组件所需的服务的依赖注入的提供者providers数组。正是通过这个属性angular知道该组件的构造器需要 `HeroService` 服务提供展示所需要的 heros 数据数组。

@Component 函数传入配置对象后，转换为附加在组件类定义上的元数据metadata。angular 在运行时通过发现元数据来知道如何做正确的事情。

template模板，metadata元数据， 和组件一起描述了视图。
随着我们不断了解angular2，我们也逐步学习其他通过metadata decorators 元数据装饰器来指导angular行为的常用decorators，如：@Injectable, @Input, @Output, @RouterConfig 等

### 数据绑定
不借助框架，我们需要手动把数据值更新到html的控件中和把用户的交互转变为值变化和方法调用。手工写这种推拉的更新逻辑非常费时，而且容易出错。正如熟练的jQuery程序员证明的那样是场噩梦！
angular支持数据绑定，一种协调同步模板和组件其他部分的机制。通过在模板中加入binding绑定的markup标记，我们告诉angular如何把两个部分组合在一起。
在angular中，有四种形式的数据绑定语法。 每种形式都需要有个方向可以是指向DOM，或者是来自DOM，或者是双向的。正如图表展示的那样：
`<Todo: 图>`

在 example 模板中， 我们展示了三种数据绑定的语法格式：

```html
<div ... >{{hero.name}}</div>
<hero-detail ... [hero]="selectedHero"></hero-detail>
<div ... (click)="selectHero(hero)></div>
```

{{hero.name}}  这种是字符串内插，来在div 标签中显示组件的hero.name 属性
[hero] 是属性绑定，把selectedHero 属性值从HeroListComponent 传递到 HeroDetailComponent 组件的 hero 属性下。
(click) 是事件绑定，当用户点击 hero的名字时候调用组件的selectHero方法

双向数据绑定是第四种重要的绑定形式，通过 ng-model 指令directive把属性和事件绑定结合起来。在HeroDetailComponent的模板中有个例子

```html
<input [(ng-model)]="hero.name">
```

angular 每个javascript 事件循环中一次性处理全部的数据绑定，从应用的组件树根部开始，深度优先。具体细节我们在后续章节有阐述，现在看起来数据绑定在模板和组件间 和 父子组件之间的通讯都起着非常重要的作用。

### 指令
我们的angular模板是动态的。 当angular渲染模板时，它把根据directive提供的指示来把模板变成DOM
指令是配有指令元数据的类。 在typescript中，我们通过@Directive装饰器来给类添加元数据。
我们已经了解了一种形式的指令：Component。 组件就是一个拥有模板，通过@Componenter而不是@Directive 来提供模板导向的特性。
还有其他两种，我们称为 结构 和 属性attribute的指令。

Todo：
- structural directive
- attribute directive


### 服务
Service 是个很宽泛的概念，来封装应用所需要的任意值，方法和特性。
虽然任何代码都可以成为service，但通常，一个服务有一个特定聚焦的目的。譬如：

- 日志服务
- 数据服务
- message bus消息总线
- 税收计算器
- 应用配置功能

Angular本身没有对service有特殊的定义，没有所谓的基础类，没有用于注册service的地方。
但services对Angular也是至关重要的，因为我们的组件式services的使用消费大户
我们通常保持组件类组件精简轻量，它本身不去从服务器拉取数据，不做用户数输入的验证，不直接把日志信息达到console中。他们把这些任务委派给 services
一个好的组件拥有属性和方法来用于数据绑定，同时把一些通用的业务委托给services
Angular 不强制约束限制这样的原则，即使你可能写一个3k多行的大杂烩的巨型组件
但是它帮助我们实施时遵守这样的原则，譬如通过依赖注入让那些处理应用业务逻辑的services可以方便的被组件使用。


### 依赖注入
依赖注入是类在创建新的实例时提供它所需的全部依赖的一种声明方式。绝大部分的依赖是服务。angular通过依赖注入机制给component提供它们所需要的服务。
在 TypeScript 中，Angular 通过查看组件的构建函数的参数获得组件所需要的services，譬如 HeroListComponent 的构建函数需要 HeroService，代码如下：

```js
constructor(service: HeroService) {
  this.heroes = service.getHeroes();
}
```
当Angular创建该组件时，它首先通过向`Injector`请求所需要的service实例. 
Injector是维持存放着它创建的各服务实例的容器
Injector 通过 `Provider` 来创建新的服务实例
Provider 是用来创建service的代码方法

我们可以在应用组件树的任意的层级注册providers，通常我们在启动bootstrap应用的根组件出注册，这样整个应用的其他地方都可以用同一个服务实例。

```js
bootstrap(AppComponent, [
  BackendService, HeroService, Logger
]);
```

同样，我们可以在特定组件层级来注册：通过annotation语法

```js
bootstrap(AppComponent, [
  BackendService, HeroService, Logger
]);
```
更详细的依赖注入请见后续的章节一探究竟~


### Misc
通过以上的介绍，我们对于构建Angular app的七个部分已经有了解了。 它们是构建Angular应用程序的关键和基础。
一下是一份简短的按照字母表顺序排序的其他Angular 的特性和services. 绝大部分会在后续的章节中有进一步的讲解和使用。

#### Animation
面向未来的动画库，使得开发者可以很容易的给组件行为加动画，而不需要过多了解动画技术或css的知识

#### Bootstrap
用来配置和启动应用程序的根组件的方法

#### Change Detection
Angular 内部如何知道组件属性改变和何时去更新页面显示。 Angular如合理利用 zones 机制去拦截异步行为和实施它的脏检查策略

#### Component Router
利用该Service，用户像浏览器通过urls跳转一样，在多屏应用中浏览跳转切换页面。

#### Events
DOM触发事件，同样组件和服务也可以触发。Angular 提供了用于发布和订阅事件的机制，该机制包括了[RxJS 观察者提议](https://github.com/zenparsing/es-observable)的实现

#### Forms
通过HTML为基础的验证和脏检查，支持复杂数据条目的场景

#### HTTP
通过 Angular HTTP Client客户端，和服务器通信来拉取数据，提交保存数据和调用服务器端的方法。

#### Lifecycle Hooks
通过实现生命周期钩子的接口，我们开发者可以在组件生命周期的关键时刻（如从创建到销毁）插入自己的行为

#### Pipes
用来转化格式化数据来显示的服务。在模板层使用pipes管道来提升用户体验，譬如，下方展示了 currency 现金的管道表达式：`price | currency: 'USD':true` 来把价格为42.33格式化为`$42.33`

#### Testing
Angular提供的测试库可以和框架本身来交互，从而可以方便的给我们的应用程序做单元测试
