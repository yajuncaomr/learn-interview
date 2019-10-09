# 继承与原型链  
每个实例对象（object）都有一个私有属性（`__proto__`）指向它构造函数的原型对象（prototype）。该原型对象也有一个自己的原型对象，层层向上直到一个一个对象的原型对象为null。根据定义null没有原型，并作为原型链中的最后一个环节。
## 基于原型链的继承  
### 继承属性  
javascript对象有一个指向原型对象的链。当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或者到达原型链的末尾。  
对象的[[Prototype]]符号用于指向对象的原型，从ES6开始，可以通过Object.getPrototypeOf()和Object.setPrototypeOf()访问器来访问。等同于非标准的但许多浏览器实现的__proto__.    
不要与构造函数的prototype属性相混淆。被构造函数创建的实例对象的[[Prototype]]属性指向构造函数的prototype属性。Object.prototype属性表示Object的原型对象。  
### 继承方法  
任何函数都可以添加到对象上作为对象的属性。函数的继承与其它的属性继承没有区别，包括属性遮蔽。
当继承的函数被调用时，this指向的是当前继承的对象，而不是继承的函数所在的原型对象。   

```javascript
    //执行new
    var o = new Foo();
    //相当于
    var o = new Object();
    o.__proto__ = Foo.prototype;
    Foo.call(o);
```