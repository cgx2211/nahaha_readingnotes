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
  ```
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
  由上看出，路由作为组件，都属于整体应用的一部分。
### 嵌套路由  
  你是怎么嵌套div的？那就怎么嵌套路由就可以了。
