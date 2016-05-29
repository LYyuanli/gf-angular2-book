## 2 组件

> *此处可能要先回顾一下之前的hello world例子*

&emsp;&emsp;组件（Component）是构成Angular2应用的基础和核心，了解它是如何工作是非常重要的，因此本书也将组件介绍在最前面。

### 2.1 什么是组件

&emsp;&emsp;组件是编写应用的基本单元，通俗地说，一个组件包装了一个特定的功能，并且组件之间协同工作以组装成一个完整的应用程序。

&emsp;&emsp;举个现实中的例子，一辆汽车中包含各种各样的部件、零件，比如发动机、变速箱、轮胎等等，那么这些便可以理解为组成汽车的`组件`，当然这还不是最小粒度的组件，例如发动机本身也会由众多小零件组合而成。

&emsp;&emsp;那么作为Web应用开发者，怎么去理解组件呢？相信读者都应该用过或者知道jQueryUI、Bootstrap、YUI等一些经典的UI库，即使不知道也没关系，你肯定写过html、css和js。在Web开发中，组件一般是指有着独立的UI界面，并且提供相应的方法，以完成一系列的界面渲染和特定功能交互的代码集合。

&emsp;&emsp;以使用jQueryUI实现一个Dialog组件为例：

![Dialog](https://raw.githubusercontent.com/gf-rd/gf-angular2-book/master/_images/chapters2-2/jquery-dialog-hello-world.png)

&emsp;&emsp;图 2-1 jquery对话框组件

&emsp;&emsp;jQueryUI的Dialog组件代码（部分）：

```javascript
var dialog = $.widget( "ui.dialog", {
    options: {},
    open: function () {},
    close: function () {},
    isOpen: function () {},
    widget: { return this.uiDialog; },
    moveToTop: function () {}
}
```

&emsp;&emsp;使用jQueryUI实现的一个HelloWorld对话框组件代码：

```html
<!doctype html>
<html lang="en">
<head>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.11.4/jquery-ui.js"></script>
  <script>
  // 组件代码javascript部分 start
  $(function() {
    $( "#dialog-" ).dialog({
      height:140,
      buttons: {
        OK: function() {
          $( this ).dialog( "close" );
        },
        Cancel: function() {
          $( this ).dialog( "close" );
        }
      }
    });
  });
  // 组件代码javascript部分 end
  </script>
</head>
<body>
<!-- 组件代码html部分 start -->
<div id="dialog" title="Dialog">
  <p>Hello World!</p>
</div>
<!-- 组件代码html部分 end -->
</body>
</html>
```

&emsp;&emsp;以上代码可以这样理解：

- 首先`$.widget( "ui.dialog" ...`这段代码，表示的是，ui.dialog是一个基础的对话框组件，它是属于jQueryUI库的组件。这个组件提供了对话框的配置、打开、关闭等属性和方法。
- 接下来的html中的代码段，便是使用jQueryUI的开发者，实现了一个“hello world对话框应用。而这个应用中（仅）包含了一个hello world对话框的组件（见上面注释中的`组件代码`部分）。它渲染了一个id为dialog的div，显示了标题、内容，并提供了“OK”和“Cancel”两个按钮给用户操作。

### 2.2 组件化的发展

&emsp;&emsp;前面的内容已经对组件有了初步的了解，下面来了解组件的概念是如何产生的，组件化又是如何发展的。

#### 2.2.1 模块化
&emsp;&emsp;谈到组件化，先要了解`模块化`。

#### 2.2.2 组件化的好处

#### 2.2.3 组件的标准

### 2.3 Angular2的组件
&emsp;&emsp;前面的章节已经介绍了Angular2是什么，以及为什么要使用它。本章的开头也介绍了组件及组件化的概念，在Angular2中，组件是非常重要的组成部分，一种更面向对象的方法来开发Web应用。一般来说，每一个应用程序都有自己的根组件（一般被命名为XxxAppComponent），当应用被启动（bootstrap）时，Angular会从根组件开始启动，并解析组件树。

&emsp;&emsp;如果读者写过Java或者C#，或者其他强面向对象的语言，你会很容易理解“组件”，它实际上是一个类，一个有着自己特定的成员数据，并根据成员数据的特性将自己渲染到屏幕上的类。Angular2也不外乎这些，让我们来看看一个例子：

```typescript
import {Component} from 'angular2/angular2'

@Component({
  selector: 'my-component',
  template: '<div>Hello World, {{name}}</div>'
})
export class MyComponent {
  constructor() {
    this.name = 'Super Man';
  }
}
```

&emsp;&emsp;上面的代码创建了一个叫MyComponent的组件，这个组件有一个'name'的成员数据，它将template里指定的div渲染到了页面上。

&emsp;&emsp;组件是Angular2应用程序的基本构建模块，通过其关联的模板（视图），控制着屏幕的某部分，并与之交互。