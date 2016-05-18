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
6 依赖注入  
	6.1 什么是依赖注入  
			- 阐述软件设计中依赖注入这种设计模式  
			- 大型OO框架必备，面向接口编程  
			- 解耦，工厂模式的升华  
	6.2 Angular2中的依赖注入   
		6.2.1 为什么需要依赖注入  
			- angular的最大亮点  
			- 组件（服务）间很方便相互调用  
			- 方便单元测试编写  
			- 结合通讯录的产品设计一个例子，一步一步解释依赖注入以及介绍必要性（目前的版本已经不错，改造为统一的通讯录例子即可）  
		6.2.2 Angular2跟Angular1依赖注入对比  
			- Angualr1中依赖注入存在问题  
				- Internal Cache(内建缓存)：依赖一般是被当做单例对待，任何一个服务在整个应用的生命周期中都应该只被创建一次。
				- Synchronous by default(默认异步)：Angular 1中的服务创建不是异步创建的。
				- Namespace collision(命名空间冲突)：在应用的生命周期中某个”type”的token是唯一的，如果我们自定义了一个名为Car的服务，而引入的第三方框架中也存在着同名的Car的服务，那么整个系统就会存在问题  
				- Built into the framework(框架内建)：Angular 1的依赖注入是内建的，我们无法单独的进行使用。  
			- Angular2的依赖注入是一个完全的重写，解决了NG1中存在的痛点  
		 6.2.3 Angular2中依赖注入几个定义  
			 - Injector(注入器)：Injector就类似于Spring里面的ApplicationContext，提供了一						系列的接口以供依赖实例的创建。  
			 - Binding(绑定)：Binding的作用在于告诉Injector如何去为某个依赖创建实例。一个					Binding需要映射到一个工厂类型的方法。  
			 -	Dependence(依赖)：一个Dependence是某个对象被创建的类型。  
	6.3 Angular2中如何使用依赖注入  
		6.3.1 组件注入Service：结合通讯录实现一个简单的组件依赖注入demo，参照官网的实现步骤 ![](media/14628038696047/14628070347950.jpg)￼  

		
		- 结合例子如何注入：通过bootstrap全局注入或在组件中通过provider注入，组件的构造函数可以直接获取singleton实例（angular在看到构造函数的参数时，会去组件的metadata中找prodiver，匹配后初始化一个单一实例，【**这里先不要去讲层级注入，先让读者浅显易懂即可，可以提到后面会讲层级注入**】）  
		- Angular2的注入实现讲解：![](media/14628038696047/14628081907519.jpg)￼  

		6.3.2 Service注入Service: Service依赖另一个service时候如何实现注入，可参考官网结合通讯录的场景设计一个demo![](media/14628038696047/14628083516263.jpg)￼  

		6.3.3 介绍optional injection：Ng2中如何实现可选的依赖注入  
	6.4 Provider  
		6.4.1 什么是provider  
			- provider提供了一个运行时的注入  
			- 注入器根据provider初始化实例  
		6.4.2 provider使得NG2的注入灵活，解耦 ![](media/14628038696047/14628087058882.jpg)￼  
		6.4.3 介绍几种provider：![](media/14628038696047/14628088565501.jpg)￼  
		6.4.4 provider声明依赖项：![](media/14628038696047/14628090445630.jpg)￼  
	6.5 层级注入  
		 6.5.1 注入树介绍  
				- 组件树的每个层级都可独立注入，都是单例
				- 注入的冒泡查找，从当前组件冒泡到bootstrap
		6.5.2 结合通讯录例子demo  
				- 在不同层级注入同一个service，证明分别是独立  
		6.5.3 对比在各层级注入的应用场景  
				- 在组件，父组件，根组件，bootstrap这几个地方注入的对比  
## 第三章 实战

## 参考资料
> TODO
