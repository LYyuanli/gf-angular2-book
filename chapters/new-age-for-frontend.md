
2015年6月17日，ECMAScript 2015(又名ES6)正式发布，这是JavaScript语言的一次重大的革新，也意味着前端界即将迎来一个崭新的时代。

在早些年间，以jQuery为代表的DOM操作库曾经给前端界带来过一轮技术革新。jQuery以巧妙的封装，链式的调用和清晰的接口使用，大大提升了前端开发的生产力，也降低了前端的入门门槛。在一段时间里很多前端工程师招聘要求里都提及到需要熟悉(精通)jQuery，可见其使用的广泛性与重要性。

而近几年来，前端界可谓是百家争鸣，日益兴旺。在与各端和各技术栈的融合中，前端工程师们创造出了很多新奇而又具颠覆性的新东西出来。
 - 使用Node.js，前端工程师可以进行服务端开发；
 - 使用React Native、Ionic，前端工程师可以进行移动APP开发；
 - 使用nw.js、Electron，前端工程师可以进行桌面应用开发。
 
还有很多好玩、实用的框架与库，这些都让前端越发绽放光彩，也让前端工程师成为市场上炙手可热的抢手岗位。在众多新技术中以Angular为代表的MVVM框架又给前端界带来了新一轮的技术革新。

MVVM(Model-View-ViewModel)这个概念最早是在2005年由微软提出的，相对于1979年提出的MVC(Model-View-Controller)架构来说，还是比较新颖的。MVVM最主要的特点是双向绑定技术，View层与ViewModel层是相互关联、自动变化的，ViewModel层同时又与Model层是相互通信、自动变化的，从而可以实现了Model和View的真正解耦，代码量也减少了很多。凡是能提升生产力的模式自然是会被提倡与实现的，而实现MVVM这个框架理念的技术有很多种，关键是要实现ViewModel层与其他层的双向绑定，以Knockout.js，Vue.js等框架均采用的Object.defineProperty来设置getter/setter,采用这种做法要比Angular 1.x使用的Dirty check的性能高。但Object.defineProperty使用的是ES5的技术，只能兼容到IE8，要兼容更旧的浏览器只能采用其他手段如用VBScript模拟之类的。
