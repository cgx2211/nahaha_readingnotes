---
layout: post
title: javascript
permalink: /technology/javascript
---

### JavaScript的强大
  JavaScript是世界上最流行的语言。Google地图、Gmail、Twitter、Facebook、GitHub。  
  JavaScript发展、性能提升。甚至浏览器中可以加载Linux内核(jslinux)。  

### 事件轮询与异步I/O
  服务器采用多线程处理并发。分配多个线程。并设置线程池。一个线程会处理一个或多个服务器请求。  
  而浏览器端则用异步的方式处理，以免等待太长时间。

### 高阶函数
  高阶函数是将函数作为参数，或者函数作为返回值的函数。  
  {% raw %}
  ```javascript
  var point = [1,9,7,4,6];  
  point.sort(function(a,b){  
    return a - b;  
    })
  angular,forEach(arr,function(el){  
      //TODO  
    });
  ```
  {% endraw %}
  angular的forEach方法是典型的高阶函数运用。这种运用也常见于underscore中。

### 偏函数
  偏函数是说创建调用另一个函数的函数。直接调用的那个函数参数与变量已经确定了。  
  举个栗子：三个异步请求，需要全部都返回成功，再调用后续方法。  
  缴费系统中我使用绑定了数字在scope上。当异步完成时+1，全部完成就调用后续方法并且置0。  
  偏函数栗子：  
  {% raw %}
  ```javascript
  var after = function(times,callback){
    var count = 0,result = {};
      //以下为实际业务代码
      return function(key,value){
        result[key] = value;
        count++;
        if(count === times){
          callback(results);
        }
      }
    }
  var done = after(times,render);
  ```
  {% endraw %}
  作为实际操作业务的done，需要一个参数，这个参数是返回值构成的对象，栗子中就是results。  
  那么这里在实际应用中，done首先调用了一个after函数，这个函数的参数就是固定的：  
  第一个参数times —— 指具体要回来几次，应用到我自己的项目中这里取3。  
  第二个参数callback —— 实际异步请求全部返回之后所需要执行的后续操作。
  这里after就起到一个计数的作用，实际里面在拼接所需对象，并且在计数满足times要求的时候，调用最后的callback方法。

### NodeJs中的EventProxy
  once()方法，执行一次就会删除监视器。  
  {% raw %}
  ```javascript
  var proxy = new events.EventEmitter();
  var status = 'ready';
  var select = function(callback){
    proxy.once('selected',callback);
    if(status === 'ready'){
      status = 'pending';
      db.select('SQL',function(results){
        proxy.emit('selected',result);
        status = ready;
        })
    }
  }
  ```
  {% endraw %}
  这里不断调用select方法的话，第一次查询后，后面的将不会有任何作用。一直持续到第一次请求返回。


  EventProxy模块作为事件emit/on模式的扩充。一个栗子：
  {% raw %}
  ```javascript
  var proxy = new EventProxy();
  proxy.all('template','data','resources',function(template,data,resources){
    //TODO
    });
    fs.readFile(template_path,'utf8',function(err,template){
      proxy.emit('template',template);
      });
    db.query(sql,function(err,data){
      proxy.emit('data',data);
      });
    l10n.get(function(err,resources){
      proxy.emit('resources',resources);
      });
  ```
  {% endraw %}
  这里当三个广播template、data、resources都成功之后，all()方法才会执行，且只执行一次。  
  相对应还有个tail()方法，当满足条件触发之后。如果其中任意事件再次广播，依然会执行。
