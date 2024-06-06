---
layout: post
title: interview questions
permalink: /technology/interviewquestions
---
### Html
  - Doctype的作用？
    + 声明文档类型。指定HTML，让浏览器进入不同的文档模式（渲染模式或者呈现模式），确保页面可以正常渲染，并提高跨浏览器兼容性  
  - 请简单介绍严格模式与混杂模式
    + 严格模式表示以浏览器支持的最高标准运行
    + 混杂模式，以宽松标准兼容老浏览器
    + 没有Doctype，或格式不正确的文档以混杂模式处理
  - 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
    + 行内元素：a span img input select
    + 块级元素：div ul ol li dl dt dd h1 p
    + 空元素：<br> <hr> <link> <meta>
  - 如何实现浏览器内多个标签页之间的通信
    + WebSocket SharedWorker
    + 利用localstorge、cookies等本地存储方式；PS：Safari 在无痕模式下设置 localstorge 值时会抛出QuotaExceededError的异常
  - iframe标签的特点
    + 增加代码重用，统一页面头尾，引入iframe的地方方便修改
    + 页面非常多，对移动端不友好，兼容性差、浏览器前进后退无效、搜索引擎支持不好
  - 请描述下事件冒泡机制
    + 冒泡型事件：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发
    + 捕获型事件：事件从最不精确的对象(document 对象)开始触发，然后到最精确(也可以在窗口级别捕获事件，须由开发人员指定)

### javascript
  - 五种基本类型
    + Undefined、Null、Boolean、Number和String
    + Object、Array和Function则属于引用类型
  - 简单描述一下undefined与not defined有什么区别？
    + Undefined是声明了并没有负值，而not defined指该变量没有被声明
  - unll与undefined的区别
    + null代表空，undefined代表未定义，以前只有null，并且null可直接转换为0。这导致会出很多不易定位的问题，所以新增了undefined类型
  - JS中如何判断数据类型？
    + typeof，判断未经过计算的操作数类型。适用于基本数据类型与引用数据类型，判断快速，但所有对象类型都返回'objcet'
    + instanceof，检测某个对象是否为某个构造函数的实例。仅适用于对象类型，基本类型无法判断。且需要同样的上下文。
    + Object.prototype.toString，这个方法可以返回对象内部的[[class]]属性，以更精准的判断对象类型，包括日期，正则等。使用起来稍显繁琐
  - for in与for of的区别
    + for in遍历当前对象中可枚举的属性，若原型链上有，也会遍历
    + for of可以遍历数组，因为数组有迭代器，但对象没有
  - ==和===有什么不同
    + == equality 等同，=== identity 恒等。 ==， 两边值类型不同的时候，要先进行类型转换，再比较。 ===，不做类型转换，类型不同的一定不等
  - 写一个三元表达式
  - 聊一聊闭包
    + 闭包就是定义在函数内部的函数，可以访问自己内部的变量、父级函数内部的变量、全局变量
  - 聊一聊具体哪个场景下能用到闭包
    + 闭包可以创建私有变量和函数，实现模块化的开发。避免变量全局污染
    + 使用闭包可以创建私有变量和函数的对象，实现数据的私有化与封装。例如单例模式中，唯一的私有变量便是闭包的直接运用
  - 当js中调用new的时候，发生了什么
    + 创建一个空对象，并继承构造函数的prototype属性。
    + 绑定this，将构造函数中的this绑定到当前新创建的对象
    + 执行构造函数：执行构造函数代码，初始化新的对象
    + 返回对象：如果构造函数并没有显式地返回一个对象，那么new表达式回自动返回新创建的对象
  - 解释下JavaScript中this是如何指向的
    + this永远指向函数运行时所在的对象。匿名函数或不处于任何对象中的函数指向window
    + 如果是call，apply,with，指定的this是谁，就是谁
    + 普通的函数调用，函数被谁调用，this就是谁
    + 严格模式下this指向undefined
  - 大概聊一下改变this指向的call,apply,bind
    + call方法：call(thisObj，Object)。调用一个对象的一个方法。call将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象。若没有提供thisObj参数，那么默认为Global对象
    + apply方法：apply(thisObj，[argArray])。应用某一对象的一个方法，用另一个对象替换当前对象。若argArray不是有效的数组/有效的arguments对象则会导致TypeError。若未提供argArray与thisObj，thisObj默认为Global，且无法传递参数
    + bind方法：不同于上述两者直接调用，bind方法会返回一个新的函数。
  - JS中，深拷贝的方法
  - JS中的继承与常见的继承方式
    + 原型链继承

    ```javascript
    function Parent(){
      this.name = 'Parent';
    }

    Parent.prototype.getName = function(){
      return this.name
    };

    function Child (){
      this.age = 25;
    }

    Child.prototype = new Parent();// 设置原型链指向Parent的实例
    var child = new Child();
    
    console.log(child.getName();)// 输出parent
    ```
    + 构造函数继承
    
    ```javascript
    function Parent(name){
      this.name = name;
    }
    function Child(name,age){
      Parent.call(this,name);// 在构造函数内调用Parent的构造函数
      this.age = age;
    }

    var child = new Child('Tom',25);
    console.log(child.name)// 输出Tom
    ```
    + 组合继承（原型链+构造函数）
    
    ```javascript
    function Parent(name){
      this.name = name;
    }

    Parent.prototype.getName = function(){// 原型上定义getName方法
      return this.name;
    }

    function Child(name,age){
      Parent.call(this.name);// 调用Parent的构造函数
      this.age = age;
    }

    Child.prototype = new Parent();// Child的原型链指向Parent的实例

    var child = new Child('Jack',25);
    console.log(child.getName())// 输出Jack
    ```
    + 原型式继承
    
    ```javascript
    function object(o){
      function F (){}// 一个构造函数
      F.prototype = o;// 原型指向传入的对象
      return new F();
    }

    var parent = {
      name:'Jack',
      getName:function(){// 对象中定义方法
        return this.name;
      }
    }

    var child = object(parent);// 这里的child是一个函数，这个函数的原型指向parent
    console.log(child.getName());// 输出Jack
    ```
    + 寄生式继承

    ```javascript
    function createAnother(origin){
      var clone = object(origin);// 这个object应该是上文中的方法吧
      // 这里相当于拷贝了一份
      // 并在新的拷贝上添加sayHi的方法
      clone.sayHi = function(){
        return 'Hi';
      }
      return clone;
    }

    var parent = {
      name:'Parent',
      getName:function(){
        return this.name;
      }
    }

    var child = new creatAnother(parent);
    console.log(child.sayHi());// 输出Hi
    ```
    + ES6 class继承（基于原型）
    
    ```javascript
    class Parent {
      constructor (name){
        this.name = name;
      }

      getName(){
        return this.name;
      }
    }

    class Child extends Parent{
      constructor(name,age){
        super(name);// 这里super就调用了Parent的构造函数
        this.age = age;
      }
    }

    const child = new Child('Jack',25);
    console.log(child.getName());
    ```
    + ES6扩展运算符继承（Object.assign）
    
    ```javascript
    const Parent = {
      name:'Tom',
      getName(){
        return this.name;
      }
    }

    const child = Objcet.create(parent);
    child.age = 25;

    console.log(child.getName());// 输出Tom
    ```
  - JS中常用的设计模式
    + 单例模式:确保一个类只有一个实例，并提供全局访问点
      
    ```javascript
      const Singleton = (function(){
        let instance;

        function createInstance() {
          const obj = new Object('I am the Iron man!');
          return obj;
        }

        return {
          getInstance: function(){
            if(!instance){
              instance = createInstance();
            }
            return instance;
          }
        }
      })();

      const instance1 = Singleton.getInstance();
      const instance2 = Singleton.getInstance();

      console.log(instance1 === instance2);// true
    ```
    + 工厂模式：用于创建对象的接口，根据不同参数返回不同的实例
    + 工厂模式旨在将对象的创建与使用逻辑分离

    ```javascript
    function Car(type){
      this.type = type;
      this.drive = function(){
        console.log(`Driving a ${this.type} car`)
      }
    }

    function CarFactory () {
      this.createCar = funciton(type){
        // 这里可以做一些创建对象之前的处理
        return new Car(type);
      }
    }

    const factory = new CarFactory();
    const car1 = factory.createCar('SUV');
    const car2 = factory.createCar('Sedan');
    car1.drive();// Driving a SUV car
    car2.drive();// Driving a Sedan car
    ```

    + 订阅者模式

    ```javascript
    class EventEmitter {
      constructor(){
        this.events = {};
      }
      on(event,listener){
        if(!this.events[event]){// 没有这个事件就初始化一下
          this.events[event] = [];
        }
        // 然后将linstener回调推入事件对象中
        this.events[event].push(listener);
      }
      emit(event,...args){
        if(this.events[event]){
          this.events[event].forEach((listener) => {
            listener.call(this,...args);
          })
        }
      }
    }

    const myEmitter = new EventEmitter();

    myEmitter.on('greet',(name)=>{
      console.log(name)
    })

    myEmitter.emit('greet','wuhu~');
    ```
  - yield是什么
    + JS中生成器函数（generator function）的一部分，调用生成器函数并不会立即执行代码，而是返回一个生成器对象，生成器对象可调用next()方法来执行代码，每次执行到yield便会暂停，并返回一个值，直到下次调用next()方法。
    + 举个栗子

    ```javascript
    function* numberGenerator(){
      console.log('我特么来辣');
      yield 1;
      console.log('我特么第二步');
      yield 2;
      console.log('我特么第三步');
      yield 3;
      console.log('寄！');
    }

    const myGen = numberGenerator();
    
    console.log(gen.next()); // { value: 1, done: false }
    console.log(gen.next()); // { value: 2, done: false }
    console.log(gen.next()); // { value: 3, done: false }
    console.log(gen.next()); // { value: undefined, done: true }
    ```


### ES6
  - ES6的新特性
    + 增加模板字符串：`${name}`
    + 增加箭头函数，数组对象解构赋值，扩展运算符(...)，async/await
  - 箭头函数与function有什么区别
    + 箭头函数相当于匿名函数，简化了定义
    + 箭头函数不能作为构造函数
    + 箭头函数没有原型
    + 箭头函数用扩展运算符获取剩余参数，而function用argument
    + 箭头函数this指向上层作用域，若没有则直接指向window

### CSS相关
  - display:none和visibility:hidden的区别
    + 没有；有，看不见。
  - position的absolute与fixed共同点与不同点。
    + 共同点：脱离文档流
    + 不同点：absolute的”根元素“是可以设置的，而fixed的”根元素“固定为浏览器窗口
  - CSS的盒子模型？
    + W3C的盒模型宽度并不包含padding与border
    + 说人话就是IE的盒模型，宽度会把padding跟border都包含进去，而W3C模型不会，一般谷歌上都用的W3C模型
    <div align="center"><img width="330" src="{{site.baseurl}}/assets/images/box-model.jpg" alt="needs_change" /></div>
  - CSS样式优先级？
    + !important > 内联 >  id > class > tag
  - 浮动元素引起的问题？
    + 脱离文档流，影响页面结构
    + 父元素的高度无法被撑开
  - 浮动元素的解决办法？
    + 浮动后添加空元素clear:both，过多使用会导致非常多的空元素
    + 父级设定overflow:hidden，会影响内部元素超出边框部分的展示
  - 如何实现浏览器内多个标签页之间的通信?
    + 调用localstorge、cookies等本地存储方式
  - px和em的区别
    + 均是长度单位、px固定，em则继承父级元素的字体大小
  - link和@import有什么区别
    + link是xhtml标签，除了加载css外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS
    + link引用CSS时候，页面载入时同时加载；@import需要在页面完全加载以后、并且引用的CSS文件加载完成后才加载
    + link支持使用javascript控制去改变样式，无兼容性问题；而@import不支持JS控制，低版本浏览器有兼容性问题

### TypeScript
  - TypeScript是什么？
    + TS是js的超集，js作为若语言类型，编译前会有很明显的错误，TS的静态检查在编译之前能发现这些错误。最终编译结果会擦除类型断言形成可运行的JS
  - const与readonly有什么区别
    + const用于变量，readnoly用于属性
    + const在运行时检查，readnoly在编译时检查
  - any void unknown never有什么区别
    + any代表一切，可以赋值给任何值，任何值也可以赋值给any
    + void，用于函数没有返回值
    + never 没有值，很少用
    + unknown，不知道什么值，任何值可以赋给unknown，但unknown不能赋值给其他值
  - 泛型是什么？
    + TS中，泛型是一种允许在定义类，接口和函数时，延迟指定某中某些类型的概念。
    + 定义函数、类、接口或类型别名时，不预先指定具体类型，而在实际使用中再指定。
  - 聊一聊interface与type
    + type，给类型取一个别名。注意，不能给同一个类型重复取别名
    + interface，声明对象类型的另一种方法
    + 大部分时候两者都可用，几乎所有interface的功能type都支持
    + 最主要的区别是别名无法通过重复命名增加新属性，而interface支持重复扩展
    + interface主要用于声明对象类型，不能给基本类型取别名（这是type的工作）
### 网络传输
  - HTTP是什么
    + HTTP全称HyperText Transfer Protocol，超文本传输协议。计算机在传输数据内容（文字，图片，视频等）时的规范
  - 一次完整的HTTP传输
    + 域名解析 => 发起TCP三次握手 => 建立TCP链接后发起http请求 => 服务端响应http请求，客户端获得html => 浏览器解析html，请求依赖的资源
  - http 和 https 有何区别?
    + http是指HTTP协议运行在TCP之上。所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份。
    + https是HTTP运行在SSL/TLS之上，SSL/TLS运行在TCP之上。所有传输的内容都经过对称加密，对称加密的密钥则透过服务器方的证书采用非对称加密
  - HTTP常见状态码
    + 1开头 请求的中间态，需要继续操作
    + 2开头 （请求成功）表示成功处理了请求的状态代码。
    + 3开头 （请求被重定向）
    + 4开头 （请求错误）
    + 5开头 （服务器错误）

### cookie
  - IE6以前支持最多20个cookie，7以后版本支持最多50个；
  - FF支持50个；
  - Safari与谷歌浏览器并未做限制；
  - 大小不能超过4k
  - 数据会自动传到服务器端，服务器也可往客户端写cookie

### Storage
  - sessionStorage与localStorage
    + sessionStorage当前浏览器窗口关闭后删除
    + localStorage本地永久存储，除非手动删除
  - 大小可以达数MB
  - 都保存在本地，不会上传至服务器端

### Angular1
  - 控制器之间如何共享数据
    + 通过angularJS建立服务、注入服务，控制器就可以直接读取了
  - ng-if与ng-show有嘛区别
  - 聊一聊angular的脏值检查
    + 每一个digest cycle中，都会对比新旧数据，每次angular都会自动开始检查，同时我们也可以通过$apply()的方式手动调用
  - 通常angular中我们应在哪里操作DOM对象？
    + 在指令里面
  - 单向绑定与双向绑定有啥区别？
    + 单向绑定只有第一次model与scope绑定时赋值，而双向绑定则会跟随model变化而变化
  - angular中定义服务，如何返回promise？简单写一下
    + 使用$q服务
    ```javascript
    angular.factory('testService', function($q) {
      return {
        getName: function() {
          var deferred = $q.defer();

          //API call here that returns data
          testAPI.getName().then(function(name) {
            deferred.resolve(name);
          });

          return deferred.promise;
        }
      };
    });
    ```
    

### React
  - React是什么？与其他的JS框架有何区别？
    + React是一款开源框架，由Facebook开发，适用于web或移动端构建复杂的前端交互
    + React体量小、致力于开发UI组件，这一点就非常特别
    + AngularJS(1.X)构建应用需注入诸多元件(指令、控制器、服务)，庞大的架构在许多场景下显得过于笨拙
  - React组件整个生命周期中发生了很么
    + 大致可以分为三类：初始化、更新状态/属性、注销
  - 聊聊JSX
    + 脸书发布React的时候，同时引入了混合JS与HTML的JSX。浏览器无法直接解析，需结合babel、webpack工具

### Redux
  - Redux是什么
    + 介于React的单项数据流，在复杂应用用共享状态会很麻烦，Redux就是为了解决这个问题而存在的
    + Redux中有单一的数据源，数据都保存在store中，用dispatch方法发送action使用纯函数来执行修改
    + rducer是个纯函数，参数为当前的state,action，并返回最新的state
  - Redux是同步的还是异步的
    + Redux默认是同步的，当disPatch一个action后，会即刻调用reducer，数据也会实时更新，这样便让store中的数据变得流畅并且可预测。通过中间键可以实现异步操作。
  - Redux的中间键
    + 中间键（Middleware）是指在action被发送到reducer之前处理的地方
    + redux-thunk 允许action创建者返回一个函数，而不是一个action对象。这个函数可以接收disPatch和getState作为参数。
    + redux-saga 另一种基于ES6生成器的异步处理中间键。
    + redux-logger 日志记录，查看每个action及其产生的状态变化

### Vuex
  - Vuex 是什么
    + 转为Vue.js应用程序设计的状态管理模式。通过集中式存储管理应用所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
    + State 单一状态树，一个对象包含全部的应用层级状态。可共享
    + Getter 类似于Vue组件中的计算属性，用于从store中派生出一些状态。
    + Mutations 唯一能够改变Vuex store中状态的方法，必须是同步函数。每个Mutation都有一个字符串的事件类型和一个回调函数，这个回调函数则是实际状态更改的地方
    + Actions 类似于Mutations，但Action提交的是Mutation，而不是直接变更状态，支持异步操作
    + Modules 当应用非常复杂的时候，vuex可以将store分割为不同的模块（module），每个模块都拥有自己的一套state,mutation,action,getter，模块间支持嵌套

### Redux与Vuex有什么异同
  - 相似之处
    + 单一状态树：两者都通过单一的状态树管理所有的状态。一个对象存储整个应用的状态
    + 不可变性：状态不能直接改变，必须通过特定的方式修改（action,mutation,reducer）
    + 集中式管理：两者都提供了一个集中式的状态管理，可在不同组件中共享状态
    + 时间旅行调试：由于状态变更是同步的，可预测且有序，方便调试，追踪，定位
  - 不同之处
    + Vuex是转为vue设计的，深度集成了Vue的响应式系统。利用Vue的reactivity系统自动更新视图；Redux则与框架无关，可以与React，Angular，Vue一起使用
    + Vuex通过mutations同步修改状态，使用actions来处理异步操作并提交mutations；Redux使用reducers来描述状态的变化，通过纯函数来执行状态变更。所有状态修改都通过dispatch一个action来触发reducer
    + Vuex内置了模块化支持，方便的将状态，mutation，action和getter分割到不同的模块中。模块可嵌套；Redux本身没有内置模块化支持，但可以通过将reducer拆分成多个小的reducer，之后使用combineReducers来组合
    + Redux有强大的中间键机制，在action被发送到reducer之前拦截处理。比如redux-saga与redux-thunk；Vuex通过action来处理异步操作，没有Redux那样丰富的中间件生态，但可通过插件机制扩展Vuex的功能

### 闲聊
  - Jquery为何可以不断的.调用？
  - 页面上需要横向排布的时候，你一般用什么办法？遇到过什么坑?
  - 你认为编码中最难的是什么？
    + 从交谈中得知应试者在编码中的弱项
  - 你一般是怎么自测的？对此你有什么看法？简单说说要如何提升编码质量
    + 合格的程序员应该重视测试，做好测试可以节约非常多的时间
  - 前端技术更新迭代很快，整个过程中你是如何保持学习的
  - 你擅长使用什么操作环境？
  - 聊一聊你们团队中如何做到版本控制与代码检视？
    + 版本控制软件、版本控制、分支控制、合并与检视
  - 当前项目会有angular1的维护工作，并且长期有，对此你有什么看法

  - 请告诉我一个你最自豪的项目，以及你在项目中如何工作的？
    + 关注回答中，是什么内容最让应试者有成就感
    + 应试者是否只着重描述了自己的功劳，还是描述了团队的合作
  - 请告诉我一个令你失望的项目，你都为此做了什么改变？
  - 简单谈谈你编码一个页面或一个应用的工作流程
  - 聊聊你的软实力？
  - 说说工作中编码以外，你都解决过什么问题
    + 修咖啡机或自行车，查看应试者对与问题的态度
  - 你认为你在前/现领导眼中，是个什么样的人
  - 你是如何看待结对开发的？以前玩过没？
  - 如何定位性能问题
  - 聊聊跨域
  - 聊聊不同的http请求的作用
  - 你现在有5个不同的css文件，如何全部引入项目
  - 你如何组织你的JS代码？
    + 考察代码习惯，比如JS与HTML分离。(现在框架基本都限定好了)
  - 编码时，如何权衡稳定、性能、安全等各方面？
    + 根据业务要求来
