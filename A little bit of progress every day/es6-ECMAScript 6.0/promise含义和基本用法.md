### 1.Promise的含义

Promise是异步编程的一种解决方案，比传统的解决方案（回调函数和事件）更合理更强大。

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件 (通常是一个异步操作)的结果。从语法上说，`Promise是一个对象`，从它可以获取异步操作的消息。

Promise对象有以下2个特点： 
- `对象的状态不受外界影响`。Promise对象代表一个异步操作，`有三种状态：Pending(进行中)、Resolved(已完成)和Rejected(已失败)`。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。 
- `一旦状态改变，就不会再变，任何时候都可以得到这个结果`。Promise对象的状态改变，只有两种可能：从Pending变为Resolved；从Pending变为Rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果。就算改变已经发生了，你再对Promise对象田静回调函数，也会立即得到这个结果。这与事件(Event)完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

有了Promise对象，就`可以把异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数`。此外，Promise对象提供了统一的接口，使得控制异步操作更加容易。

### 2.基本用法

ES6规定，Promise对象是一个构造函数，用来生成Promise实例

```
var promise = new Promise(function(resolve,reject){
  // ... some code
  if(/* 异步操作成功 */){
    resolve(value);
  }else{
    reject(error);
  }
});
```

Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，又JavaScript引擎提供，不是自己部署。

`resolve函数的作用`，将Promise对象的状态从“未完成”变成“成功”(即从Pending变为Resolved)，在`异步操作成功时调用，并将异步操作的结果，作为参数传递出去`； 

`reject函数的作用是`，`在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。`

Promise实例生成以后，可以用`then方法分别制定Resolved状态和Rejected状态的回调函数`：


```
promise.then(function(value){
  // sucess
},function(error){
  // failure
});
```

then方法可以接受2个回调函数作为参数，第二个函数是可选的，不一定要提供。这两个函数都接受Promise对象传出的值作为参数。

###### 下面是一个Promise对象的简单例子：


```
function timeout(ms){
  return new Promise((resolve,reject)=>{
    setTimeout(resolve,ms,'done');
  });
}

timeout(100).then((value)=>{
  console.log(value);
});
```

上面代码中，timeout方法返回一个Promise实例，表示一段事件以后才会发生的结果。过了指定的时间(ms参数)以后，Promise实例的状态变为Resolved，就会触发then方法绑定的回调函数。

`Promise新建后就会立即执行`


```
let promise = new Promise(function(resolve,rejeact){
  console.log('Promise');
  resolve();
});

promise.then(function(){
  console.log('Resolved');
});

console.log('Hi');

// Promise
// Hi
// Resolved
```

上面代码中，Promise新建后立即执行，所以首先输出的是”Promise”，然后then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以”Resolved”最后输出。

###### 下面是异步加载图片的例子：


```
function loadImageAsync(url){
  return new Promise(function(resolve,reject){
    var image = new Image();
    image.onload = function(){
      resolve(image);
    };
    image.onerror = function(){
      reject(new Error('Could not load image at' + url));
    };

    image.src = url;
  });
```

###### 下面是一个用Promise对象实现Ajax操作的例子：


```
var getJSON = function(url){
  var promise = new Promise(function(resolve,reject){
    var client = new XMLHttpRequest();
    client.open('GET',url);
    client.onreadystatechange = handler;
    client.responseType = 'json';
    client.setRequestHeader('Accept','application/json');
    client.send();

    function handler(){
      if(this.readyState !` 4){
        return;
      }
      if(this.status `= 200){
        resolve(this.response);
      }else{
        reject(new Error(this.statusText));
      }
    }
  });

  return promise;
};

//
getJSON('/posts.jons').then(function(json){
  consoloe.log(json);
},function(error){
  console.log('出错了');
});
```
