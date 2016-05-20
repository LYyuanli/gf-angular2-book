# 书籍周边

## 1. 内容周边

## 1.1 编写内容放置

- github地址：https://github.com/gf-rd/gf-angular2-book
- 章节内容放置在『chapter』文件夹，如第二部分第三章文件名："2.3-模板.md"。
- 统一用Markdown来书写

### 1.2 图片放置

图片放置在『_images』文件夹（画图工具可见浪的writing-tools）。

引用地址：
- https://github.com/(user)/(repo)/raw/master/path/to/image.gif
- 或者在github上选中图片，点击『raw』能获取到类似于cdn的图片地址

### 1.3 图片与表格注解
- 图号/表号（按章节编排顺序）
- 图题/表题（对图片或表格的简单描述）

#### 图号和图题放置在图片下方
```

[alt text](http://imageurl)

图 3-1 NgModel双向绑定效果图

```

#### 表题表号放置在上方

```

表 3-1 数据绑定类型

| 标题1 | 标题2 |

```

## 2. 内容要求

### 2.1 不使用人称视角

// 不好

在模板表达式里，我们是不能引用到任何全局命名空间中的成员

// 好

模板表达式里是不能引用任何全局命令空间中的成员

### 2.2 不要口语化表述

// 不好

1. `[(ngModel)]`会自动地完成了属性绑定和时间绑定，碉堡了有木有。。。
2. 现在我们知道了DI这种叼炸天的特性。。。
3. XX亮瞎你的眼睛

// 好

1. `[(ngModel)]`会自动地完成了属性绑定和时间绑定
2. 现在我们知道依赖注入这个强大的特性
3. 去掉之

### 2.3 设问句使用？

// 自问自答形式

设置DOM对象的属性值，Angular2推荐使用DOM对象属性绑定，但为啥还会有HTML元素属性绑定呢？原因是...

结论：可以使用

### 2.4 关于demo引用

// 不好

// 不要在使用官网的Hero例子了

```
    ```html
    <div *ngFor="#hero of heroes">{{hero.fullName}}</div>
    ```
```
    
// 好

// 咱们的通讯录Demo

// https://github.com/gf-rd/ng2-contacts-demo

```
    ```html
    <li *ngFor="#contact of contacts">
      <a [routerLink] = "['ContactDetail',{id:contact.id}]">
        <label class="contact-name">{{ contact.name }}</label>
        <span class="contact-tel">{{ contact.telNum }}</span>
      </a>
    </li>
    ```
```

### 2.5 章节开头
需要以一段话做章节铺垫，已段落形式，不以列表形式。

作用：
1. 简单带过上一章的中心内容
2. 为本章描述做开篇引导

### 2.6 章节结尾
概括本章讲述的重点，内容点以列表形式给出

格式类似：

本章我们学习了XXX（核心概括），关键点有：

1. 属性绑定
2. 事件绑定
2. 表单
3. PIPE
4. ...

## 3. 格式要求

### 3.1 目录层次

// 不好
```
### 3.2.1 属性绑定
#### 3.2.1.1 单向数据流
#### 3.2.1.1.1 第五级标题
```

// 好
```
# 3 模板
## 3.2 数据绑定
### 3.2.1 属性绑定
#### 单向数据流
##### 第五级标题
```

层次结构：篇-章-节-小节-小小节

### 3.2 段落开头不需要空两格

// 不好

[空格][空格]模板主要的形态是HTML，实际上HTML正是Angular模板的默认使用语言，绝大部分的HTML语法在模板中也都是适用的，除了`<script>`标签，`<script>`标签主要是为了防止Javascript脚本注入的可能性...

// 好

模板主要的形态是HTML，实际上HTML正是Angular模板的默认使用语言，绝大部分的HTML语法在模板中也都是适用的，除了`<script>`标签，`<script>`标签主要是为了防止Javascript脚本注入的可能性...

### 3.3 代码块加上PL标识

// 不好

```
    ```
    import { Component, Pipe } from "angular2/core";
    @Pipe({ name:  "anyPipeName" })
    class anyPipeNamePipe { ... }
    ```
```

// 好

```
    ```js
    import { Component, Pipe } from "angular2/core";
    @Pipe({ name:  "anyPipeName" })
    class anyPipeNamePipe { ... }
    ```
```

### 3.4 代码缩进2空格

```js
import {Component} from 'angular2/core'
@Component({
  selector: 'hero-birthday',
  template: `<p>The hero's birthday is {{ birthday | date:"MM/dd/yy" }}</p>`
})
export class HeroBirthday {
  birthday = new Date(1988,3,15); // April 15, 1988
}
```

更多Style Guide请查看官网
https://angular.io/docs/ts/latest/guide/style-guide.html

### 3.5 行内代码片段

// 不好

和模板表达式一样，模板声明也不能引用任何全局对象，如window和document，同样也无法调用console.log或是Math.min。

// 好

和模板表达式一样，模板声明也不能引用任何全局对象，如`window`和`document`，同样也无法调用`console.log`或是`Math.min`。


