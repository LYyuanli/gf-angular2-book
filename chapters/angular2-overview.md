## Angular2 Overview

```bash
草稿

先是引言 （承前启后）

然后就用官方的架构讲解7大概念，最后是其他小概念。

如何加入我自己的理解（如 directive 分为三部分（structure, attribute, components）, template语法也是可以概览的，等）
加入目前 ng2 with ts 中的第一章部分
最好替换英文图片为中文
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


### Component


### Template
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



### Medatadata(Annotation)

### Data Binding

### Directive

### Service

### Dependency Injection

### Misc
通过以上的介绍，我们对于构建Angular app的七个部分已经有了解了。 它们是构建Angular应用程序的关键和基础。
一下是一份简短的按照字母表顺序排序的其他Angular 的特性和services. 绝大部分会在后续的章节中有进一步的讲解和使用。

Animation