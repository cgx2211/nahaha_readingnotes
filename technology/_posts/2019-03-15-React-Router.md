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
  React Router有很多组件，通过环境路由的定位来决定渲染些什么。    
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
  以上代码段是导航，当组件挂载时，下面的子元素会根据当前路由位置信息依次渲染。  
  假设路由切换了，从/faq切换到了/about，页面其他部分完成了变化。  
  但当前组件中并未检测到任何的属性、状态变化，因此组件内的子元素不会重新渲染。  
  组件的shouldComponentUpdate方法能检测到路由变化，并告知组件应该重新渲染了。
  如果手动触发shouldComponentUpdate方法，需要手动对比当前路由与跳转的context.router对象。  
  作为用户，不直接操作context而比较路由则是最完美的办法。  
  第三方代码
  你可能会发现，在路由变动之后，无论是否手动调用shouldComponentUpdate，组件都不会更新。  
  这很可能因为第三方在调用shouldComponentUpdate。比如react-redux's connect与mobx-react's observer。  
  使用第三方代码的时候，你可能无法很好的控制shouldComponentUpdate。相对的，构建代码的时候，你需要考虑如何能更容易检测到路由变动。  
  由connect与observer创建的组件使用的shouldComponentUpdate方法，都只做props浅层比较。组件更新需要至少一个props有变动。  
  因此为了确保组件更新，你可以在路由变动的时候，让组件的props发生变动。  
  原生组件PureComponent  
  原生组件并不会直接调用shouldComponentUpdate方法，与shouldComponentUpdate类似。浅层对比props与state。  
  没有任何变化，组件就不会更新。所以想让组件更新？你知道该怎么做了。  
  快速解决方案  
  如果你使用高级组件比如react-redux的connect或者Mobx的observer，可以直接用withRouter包裹起来，以避免非同步渲染。  
  关于这个解决方案可查看[Redux guide](https://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/guides/redux.md#blocked-updates)。要搞明白为什么这不是最有效的解决方案，可以看[这里](https://github.com/ReactTraining/react-router/pull/5552#issuecomment-331502281)。  
  推荐的解决方案  
  避免非同步的渲染，关键就是将路由对象作为属性传递给组件。路由一旦变化，组件就能检测到并更新。  
  取得路由  
  为了给组件传递当前路由对象，那首先要获取当前路由对象。常规方式便是使用<Route>组件。当<Route>匹配路由时，渲染子元素会将当前路由信息传递过去。  
  因此这就有两种方式可以将路由当作对象传入
  - 组件直接作为<Route>的子元素渲染  
  - <Route>也可将路由对象传递给任何一个子元素  
  这特么的叫两种方式？  
  当组件不通过<Route>渲染，或者组件渲染时没有路由对象作为参数的时候咋办？  
  依然是两种方式：  
  - 写一个没有路径的<Route>，无论路由处在什么位置，无路径的<Route>总是会渲染  
  - 用withRouter包裹高阶组件  
