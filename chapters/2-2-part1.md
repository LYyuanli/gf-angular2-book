## 组件

> *此处可能要先回顾一下之前的hello world例子*

&emsp;&emsp;组件（Component）是构成Angular2应用的基础和核心，了解它是如何工作是非常重要的，因此本书也将组件介绍在最前面。

#### 什么是组件
&emsp;&emsp;通俗地说，一个组件包装了一个特定的功能，并且组件之间协同工作以组装成一个完整的应用程序。

&emsp;&emsp;作为Web应用开发者的你都应该用过或者知道jQueryUI、Bootstrap、YUI等一些经典的UI库，即使不知道也没关系，你肯定写过html、css和js。在Web开发中，组件一般是指有着独立的UI界面，并且提供api，以完成一系列的界面渲染和特定功能的交互的模块组成。

&emsp;&emsp;以实现一个Dialog组件为例：
![Dialog](/Users/liangjz/Desktop/ng2book-images/ng2-book-component-1-dialog.png)
&emsp;&emsp;图 2-1 NgModel双向绑定效果图

&emsp;&emsp;jQueryUI的Dialog组件代码（部分）：这个组件提供了对话框的配置、打开、关闭等属性和api。它渲染了一个id为dialog的div，显示了标题、内容，并提供了“OK”和“Cancel”两个按钮给用户操作，这个组件提供了5个api——open、close、isOpen、widget、moveToTop——给用户调用。

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

```html
<!doctype html>
<html lang="en">
<head>
  <link rel="stylesheet" href="//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css">
  <script src="//code.jquery.com/jquery-1.10.2.js"></script>
  <script src="//code.jquery.com/ui/1.11.4/jquery-ui.js"></script>
  <script>
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
  </script>
</head>
<body>
<div id="dialog" title="Dialog">
  <p>Hello World!</p>
</div>
</body>
</html>
```


