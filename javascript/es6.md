### ES6的新功能 

#### 箭头函数（=>）
 
 箭头函数使用=>作为函数的简写形式。  
 函数体支持表达式（expression）和声明（statement）,箭头函数和它周围的代码共享相同的this,箭头函数在一个function中时，它使用父function的arguments(也就是没有自己的arguments)。  
 箭头函数不能用new操作符调用，它的原型（__proto__）为undefind.

 #### classes

 #### 增强对象字面量

 1. 字面量指定__proto__，['__proto__']字面量指定不会设置原型，不会覆盖__proto__;
 2. 属性名简写；
 3. 使用Super;
 4. 动态计算属性[];

 #### 模板字符串（template Strings）

 #### 解构赋值

 #### 默认参数、剩余参数、扩展运算符

 #### let const

 #### for ... of 

 #### 生成器函数（generators）

 #### 模块（modules import export）

 #### Map、Set、WeakMap、WeakSet

 #### Proxies

 #### Symbles

 #### 一些内置对象可以创建子类

 #### Math、Number、String、Object APIS

 ```javascript
    Number.EPSILON
    Number.isInterger()
    Number.isNaN()

    Math.acosh()
    Math.hypot()
    Math.imul()

    String.prototype.includes
    String.prototype.repeat

    Array.from()
    Array.of()

    Array.prototype.fill
    Array.prototype.findIndex
    Array.prototype.entries
    Array.prototype.keys
    Array.prototype.values

    Object.assign()
    
```
#### 二进制和八进制文字（Binary and Octal Literals）

#### Promises

#### Reflect API

#### 尾递归（tail calls）


