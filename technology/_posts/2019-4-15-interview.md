---
layout: post
title: interview questions
permalink: /technology/interviewquestions
---
### Html
  - Doctype的作用？
    + 告知浏览器用什么文档类型规范来解析当前文档
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
  - ==和===有什么不同
    + == equality 等同，=== identity 恒等。 ==， 两边值类型不同的时候，要先进行类型转换，再比较。 ===，不做类型转换，类型不同的一定不等
  - 写一个三元表达式
  - 聊一聊闭包
    + 闭包就是定义在函数内部的函数，可以访问自己内部的变量、父级函数内部的变量、全局变量
  - 聊一聊具体哪个场景下能用到闭包
  - 解释下JavaScript中this是如何指向的
    + this永远指向函数运行时所在的对象。匿名函数或不处于任何对象中的函数指向window
    + 如果是call，apply,with，指定的this是谁，就是谁
    + 普通的函数调用，函数被谁调用，this就是谁
  - call和apply的区别是什么
    + call方法：call(thisObj，Object)。调用一个对象的一个方法。call将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象。没有提供thisObj参数，那么默认为Global对象
    + apply方法：apply(thisObj，[argArray])。应用某一对象的一个方法，用另一个对象替换当前对象。若argArray不是有效的数组/有效的arguments对象则会导致TypeError。若未提供argArray与thisObj，thisObj默认为Global，且无法传递参数
### CSS相关
  - display:none和visibility:hidden的区别
    + 没有；有，看不见。
  - position的absolute与fixed共同点与不同点。
    + 共同点：脱离文档流
    + 不同点：absolute的”根元素“是可以设置的，而fixed的”根元素“固定为浏览器窗口
  - CSS的盒子模型？
    + W3C的盒模型宽度并不包含padding与border
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

### 网络传输
  - 一次完整的HTTP传输
    + 域名解析 => 发起TCP三次握手 => 建立TCP链接后发起http请求 => 服务端响应http请求，客户端获得html => 浏览器解析html，请求依赖的资源
  - http 和 https 有何区别?
    + http是指HTTP协议运行在TCP之上。所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份。
    + https是HTTP运行在SSL/TLS之上，SSL/TLS运行在TCP之上。所有传输的内容都经过对称加密，对称加密的密钥则透过服务器方的证书采用非对称加密
  - HTTP常见状态码
    + 2开头 （请求成功）表示成功处理了请求的状态代码。
    + 3开头 （请求被重定向）
    + 4开头 （请求错误）
    + 5开头（服务器错误）
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
    ```
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
    + 使用$q服务

### React
  - React是什么？与其他的JS框架有何区别？
    + React是一款开源框架，由Facebook开发，适用于web或移动端构建复杂的前端交互
    + React体量小、致力于开发UI组件，这一点就非常特别
    + AngularJS(1.X)构建应用需注入诸多元件(指令、控制器、服务)，庞大的架构在许多场景下显得过于笨拙
  - React组件整个生命周期中发生了很么
    + 大致可以分为三类：初始化、更新状态/属性、注销
  - 聊聊JSX
    + 脸书发布React的时候，同时引入了混合JS与HTML的JSX。浏览器无法直接解析，需结合babel、webpack工具
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
