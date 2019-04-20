---
layout: post
title: React Router
permalink: /technology/reactrouter
---
### 路由的哲理
  静态路由与动态路由的区别。  
  静态路由在整个框架初始化之前就定义好了，比如像angular，Express等。React Router前四版大部分也属于静态路由。  
  Angular中，将事先定义好的路由，注入到AppModule顶层。Ember中，routers.js文件很方便的帮你读取、注入路由设置。  
  上述的这一切都发生在框架渲染之前。
  为了更好的运用React Router，忘掉这些东西吧 :O。  
### 一切的起源
  讲道理，最初React Router V2版本的使用理念越发让我觉得沮丧。我们(Michael与Ryan)被限制在了API之中，不断的重构部分React，比如生命周期等。  
  这与React的前端理念背道而驰。  
  某天我们在车间隔壁的旅店的门廊散步，讨论到底该怎么做。“像车间里教授时用的模式来发展Router怎么样？”  
  只论证了几个小时，我们就确定了这将是路由未来的方向，弃用之前总是游离在React之外的API，相信你们会喜欢。  
### 动态路由  
  动态路由是指当应用启动时一并渲染，而不是一套游离于应用之外的设置。这意味着所有的一切都是Router的组件。  
  {% raw %}
  ```javascript
  ReactDOM.render((
    <BrowserRouter>
      <App/>
    </BrowserRouter>
    ),el
  )
  const App = () => (
    <div>
      <div>
        <Link to="/dashbord">Dashbord</Link>
      </div>
      <div>
        <Route path="/dashboard" component={Dashboard}>
      </div>
    </div>
  )
  ```
  {% endraw %}
  由上看出，路由作为组件，都属于整体应用的一部分。
### 嵌套路由  
  你是怎么嵌套div的？那就怎么嵌套路由就可以了。
### 静态路由
  之前版本的React Router都是通过静态路由配置，在渲染页面之前就匹配路由，自从v4版本引入动态路由之后，静态路由越发鸡肋。为了满足先前版本的使用，我们依然在继续开发
### Update Blocking
  React Router有很多组件，通过自身当前的位置决定在哪里渲染。  
  默认来说，当前位置是由React内容模态框传递给组件的。当路由位置变化后，组件会根据内容位置重新渲染  
  针对应用渲染优化，React提供了两个方法：shouldComponentUpdate生命周期方法与PureComponent。  
  当渲染条件不满足，组件将不会随着路由的改变而同步渲染。  
  举个栗子
  {% raw %}
  ```javascript
  class UpdateBlocker extends React.PureComponent {
    render() {
      return (
        <div>
          <NavLink to="/about">About</NavLink>
          <NavLink to="/faq">F.A.Q.</NavLink>
        </div>
      );
    }
  }
  ```
  {% endraw %}
  以上是个导航，当组件挂载时，下面的子元素会根据当前路由位置信息依次渲染。  
  假设路由切换了，从/faq切换到了/about，页面其他部分完成了变化。  
  但当前组件中并未检测到任何的属性、状态变化，因此组件内的子元素不会重新渲染。
