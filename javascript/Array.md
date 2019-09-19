# Array

Array静态方法
+ Array.from()  
从类数组对象或者可迭代对象中创建一个新的数组实例
+ Array.isArray()  
用来判断某个变量是否是一个数组对象
+ Array.of  
根据一组参数来创建新的数组实例，支持任意的参数数量和类型

## 数组实例  
所有的数组实例，都会从Array.prototype继承属性和方法。修改Array的原型会影响到所有的数组实例

### 属性  
+ Array.prototype.constructor  
所有的数组实例都继承了这个属性，它的值就是 Array，表明了所有的数组都是由 Array 构造出来的
+ Array.prototype.length  
上面说了，因为 Array.prototype 也是个数组，所以它也有 length 属性，这个值为 0，因为它是个空数组。
### 方法  
#### 修改器方法（改变调用它们的对象的自身的值）  
+ Array.prototype.copyWithin()
+ Array.prototype.fill()
+ Array.prototype.pop()
+ Array.prototype.push()
+ Array.prototype.reverse()
+ Array.prototype.shift()
+ Array.prototype.sort()
+ Array.prototype.splice()
+ Array.prototype.unshift()

#### 访问方法(绝对不会改变调用它们的对象的值，只会返回一个新的数组或者返回一个其它的期望值)
+ Array.prototype.concat()
+ Array.prototype.includes()
+ Array.prototype.join()
+ Array.prototype.slice()
+ Array.prototype.toSource()
+ Array.prototype.toString()
+ Array.prototype.toLocalString()
+ Array.prototype.indexOf()
+ Array.prototype.lastIndexOf()
#### 迭代方法()
+ Array.prototype.forEach()
+ Array.prototype.entries()
+ Array.prototype.every()
+ Array.prototype.some()
+ Array.prototype.filter()
+ Array.prototype.find()
+ Array.prototype.findIndex()
+ Array.prototype.keys()
+ Array.prototype.map()
+ Array.prototype.reduce()
+ Array.prototype.reduceRight()
+ Array.prototype.values()
+ Array.prototype[@@iterator]
