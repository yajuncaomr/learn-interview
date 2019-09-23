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
