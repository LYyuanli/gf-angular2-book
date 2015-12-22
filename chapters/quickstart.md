# 快速开始

提供了JavaScript以及TypeScript两种语言版本的实例，相关代码可以从[这里下载](../codes/quickstart-js.zip)

## 一、使用JavaScript快速开始

### 环境准备
- 已经安装好最新稳定版 __node__ 以及 __npm__

### 步骤

>1. 创建工程目录
>2. 安装相关类库
>3. 在入口文件app.js中编写程序
>4. 浏览器执行

- 创建工程目录

  ```bash
  mkdir angular2-quickstart-js
  cd    angular2-quickstart-js
  ```
- 安装相关类库

  创建 __package.json__ 文件

  ```bash
  npm init
  ```

  安装最新版Angular 2，目前最新版本号是2.0.0-alpha.48

  ```bash
  npm install angular2@latest --save

    angular2@2.0.0-alpha.48 node_modules/angular2
    ├── reflect-metadata@0.1.2
    ├── zone.js@0.5.8 (es6-promise@3.0.2)
    └── rxjs@5.0.0-alpha.14
  ```

  最终package.json文件内容是这样的：

  ```javascript
  {
    "name": "angular2-quickstart",
    "version": "1.0.0",
    "main": "app.js",
    "dependencies": {
      "angular2": "^2.0.0-alpha.48"
    }
  }
  ```

- 在入口文件app.js中编写程序

  创建index.html以及app.js

  > **index.html入口文件**
  >
  > 加载Angular 2开发库，ng将作为全局对象暴露在外

  ```html
  <html>
    <head>
      <title>QuickStart</title>
      <script src="node_modules/angular2/bundles/angular2.sfx.dev.js"></script>
      <script src="app.js"></script>
    </head>
    <body>
      <my-app></my-app>
    </body>
  </html>
  ```
  > **app.js主文件**
  >
  > 相关资源加载完毕后，以匿名函数立即执行的方式执行，避免命名的全局污染

  ```javascript
  (function() {
    var AppComponent = ng
      .Component({
        selector: 'my-app',
        template: '<h1>Hello World!</h1>'
      })
      .Class({
        constructor: function () { }
      });
    document.addEventListener('DOMContentLoaded', function() {
      ng.bootstrap(AppComponent);
    });
  })();
  ```
- 在浏览器中执行

  在chrome浏览器中执行，最终展示效果：

  `Hello World!`

## 二、使用TypeScript快速开始

### 环境准备
- 已经安装好最新稳定版 __node__ 以及 __npm__

### 步骤

>1. 创建工程目录
>2. 创建并编辑package.json文件
>3. 创建并编辑tsconfig.json文件
>4. 安装相关类库
>5. 创建工程主要文件
>6. 浏览器执行

- 创建工程目录

  ```bash
  mkdir -p angular2-quickstart-ts/app
  cd    angular2-quickstart-ts
  ```
- 创建并编辑package.json文件

  ```javascript
    {
      "name": "angular2-quickstart-ts",
      "version": "1.0.0",
      "dependencies": {
        "angular2": "latest",
        "systemjs": "0.19.6",
        "es6-promise": "^3.0.2",
        "es6-shim": "^0.33.3",
        "reflect-metadata": "0.1.2",
        "rxjs": "5.0.0-beta.0",
        "zone.js": "0.5.10"
      },
      "devDependencies": {
        "typescript": "^1.7.3"
      }
    }

  ```

- 创建并编辑tsconfig.json文件

```javascript
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
