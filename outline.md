## 序1

> 梁总

## 序2

> 业界牛人，NG高手

## 前言

1. 本书的背景
> TODO

2. 本书的读者
> TODO

3. 本书的组织
> TODO

4. 致谢
> TODO

## 目录

1. 常规目录部分
2. 参考资料

## 第一章 Angular2 入门
> 章首说明，说明NG2背景

1.1 走进前端新时代  
> TODO

1.2 Angular2 基本概念  
1.3 TypeScript语言简介  
1.4 快速上手  

> 总结：本章讲述了什么内容，通过本章内容，学习到什么，同时能带出第二章的一些内容前奏

## 第二章 深入理解
5. 服务  
      5.1 服务介绍  
              5.1.1 什么是服务  
                  - 简单描述什么是服务，服务在系统中的作用：服务为系统提供了基础功能，通过独立的接口跟功能给外部调用  
           5.1.2 NG2中的Service（Injectable）  
            - 描述NG2中的服务概念：介绍内置service（http等）跟自定义service（每个class都    可以是一个单例可服用的服务，通过@Injectable()注解标示，component可直接 注入）  
           5.1.3 NG2中的service跟NG1中的service   
            - 对比NG2跟NG1关于service的区别：  
                NG1：factory，service，provider                         
                NG2：class  
     5.2 Http  
          5.2.1 Http client介绍 （1000字内）  
            - 介绍客户端与服务端通讯的方式：XHR，JSONP，Fetch  
            - 介绍NG2中的http服务  
          5.2.1 结合通讯录例子编写用http模块实现的例子 （详细，step by step）  
            - 编写从服务端获取通讯录列表并展示在ui中例子  
          5.2.2 Http与observable  
          - 带一下NG2中的返回obserable对象  
      5.3 响应式编程  //TODO:（可以把第九章的响应式编程搬过去）  
          5.3.1 什么是响应式编程  
          5.3.2 为什么要响应式编程  
      5.4 Rxjs  
          5.4.1 什么是rxjs  
            - 响应式编程的js实现，观察者模式的改写  
            - 介绍rxjs开发的套路，具体包含几部分 
              - Rx.Observable.create()  
              - Rx.Observer.create()  
              - subscribe()    
          5.4.2 rx操作符  
            - 介绍rx操作符的工作流程，结合珠宝图（简单即可，毕竟这不是rxjs的书）  
            - NG2中常用的几种即可，包括map(结合http)，fromevent(用click事件作为例子)  
            - 普通数据类型跟observable对象的转换：使用from转换，用to还原  
          5.4.3 NG2中rxjs  
            - 描述NG2中如何使用rxjs（rxjs过于庞大，ng2只使用简约版）  
            - 结合通讯录例子中的通讯列表讲解NG2中rxjs，根据官网的例子改造即可  
          5.4.4 observble 与 promise  
            - promise只是obserable的弱化版，用toPromise(success, fail)可简单实现转化  
            - 用通讯录例子改造成promise（可参照官网的例子）  
          5.4.5 jsonp  
            - 简单介绍jsonp  
            - 改造通讯录例子，用jsonp方式实现（参照官网即可）  
      references：  
        https://angular.io/docs/ts/latest/guide/server-communication.html#!#rxjs  
        https://angular.io/docs/ts/latest/tutorial/toh-pt4.html  
        https://docs.angularjs.org/guide/services   
        http://www.tutorialspoint.com/angularjs/angularjs_services.htm  
        http://reactivex.io/rxjs/  
## 第三章 实战

## 参考资料
> TODO
