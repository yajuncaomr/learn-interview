# Promise  
Promise 对象用于表示一个异步操作的最终完成 (或失败), 及其结果值.  
Promise对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的的成功和失败分别绑定相应的处理方法。  
一个Promise有以下几种状态：
+ pending:初始状态，既不是成功也不是失败状态。
+ fulfilled:操作成功完成。
+ rejected:操作失败。

## 方法  
Promise.all(iterable)

这个方法返回一个新的Promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。

Promise.race(iterable)

当iterable参数里的任意一个子promise被成功或者失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象。

Promise.reject(reason)

返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法

Promise.resolve(value)

返回一个状态由给定value决定的Promise对象。

## Promise原型

属性  
Promise.prototype.constructor  
返回被创建的实例函数，默认为Promise函数

方法  
Promise.prototype.catch(onRejected) 

Promise.prototype.then(onFulfilled,onRejected)

Promise.prototype.finally(onFinally)

## 约定
+ 在本轮javascript event loop(事件循环)运行完成之前，回调函数是不会被调用的。
+ 通过then()添加的回调函数总会被调用，即便它是在异步操作完成之后才被添加的函数。
+ 通过多次调用then(),可以添加多个回调函数，它们会按照插入顺序一个接一个独立执行。

## 组合
Promise.resolve()和Promise.reject()是手动创建一个已经resolve或者reject的Promise的快捷方法。  
Promise.all()和Promise.race()是并行运行异步操作的两个组合式工具。
```javascript
    Promise.all([func1(),func2(),func3(),func4()]).then(([result1,result2,result3,result4]) => {});
```  
运用reduce实现时序组合
```javascript
    [func1,func2,func3,func4].reduce((p,f) => p.then(f),Promise.resolve())
    .then(result4 => {});
```  

可复用的形式
```javascript
    const applyAsync = (acc,val) => acc.then(val);
    const composeAsync = (...funcs) => (x) => funcs.reduce(applyAsync,Promise.resolve(x));//funcs中的函数可以是异步（Promise异步）或同步
```

ES2017中时许可通过async awiat实现  
```javascript
async function composeAsync(...funcs){
    let result;

    for(const f of funcs){
        result await f(result);
    }
    return result;
}
```

## 时序  
已经resolve的Promise,传递给then()的函数也总是会被异步调用:
```javascript
    Promise.resolve().then(() => console.log(2));
    console.log(1)//1 2
```
传递到then中的函数被置于一个微任务队列，而不是立即执行，这意味着它是在javascript事件队列的所有运行时结束了，事件队列被清空之后，才开始执行。  

```javascript
    const wait = ms => new Promise(resolve => setTimeout(resolve,ms));

    wait().then(() => console.log(4));
    Promise.resolve().then(() => console.log(2)).then(() => console.log(3));
    console.log(1);
```

