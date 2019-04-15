---
layout: post
title: interview questions
permalink: /technology/interviewquestions
---
### javascript
  - 五种基本类型
    + Undefined、Null、Boolean、Number和String
    + Object、Array和Function则属于引用类型

### CSS相关
  - display:none和visibility:hidden的区别？
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

### 网络传输
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
