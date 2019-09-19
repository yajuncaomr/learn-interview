# 前端知识总结javascript

## 数据类型
+ 7种原始类型
    + Boolean
    + Null
    + Undefined
    + Number
    + BigInt
    + String
    + Symbol
+ Object

### Number类型
    Number类型包括浮点数、+Infinity、-Infinity、NaN。
    1. 所有的数字都是浮点型
    2.  所有的数字类型相同‘number’
    3. JS与任何其他语言一样，受限于它可以表示的数字大小以及它的准确程度。

### BigInt类型
    BigInt类型是 JavaScript 中的一个基础的数值类型，可以用任意精度表示整数。使用 BigInt，您可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。BigInt是通过在整数末尾附加 n 或调用构造函数来创建的

### 字符串类型

### 符号类型

### 对象
+ Date
+ Array
+ TypedArray
+ Maps
+ Sets
+ WeakMaps
+ WeakSets
+ Error
+ RegExp
+ Function
+ Math
### 基本类型判断
#### 判断是否数值
```javascript
    typeof v === 'number' && isFinite(v) //isFinite()排除NaN和Infinity、-Infinity
    typeof NaN === 'number'//true
    typeof Infinity === 'number'//true
```
#### 判断布尔值
```javascript
    typeof v === 'boolean'
```
#### 判断字符串
```javascript
    typeof v === 'string'
```
#### 判断undifined
```javascript
    typeof v === 'undifined'
```
#### 判断symbol
```javascript
    typeof v === 'symbol'
```
### 判断是否数组？
```javascript
obj && typeof obj === "object" && obj.construstor === Array;//方法一
Object.prototype.toString.apply(my_value) === '[object Array]';//方法二会排除arguments
Array.isArray(obj);//es6新方法
obj instanceof Array //不需要判断来自不同的frame
```


## bind、call、apply的区别？

都是改变函数中this的指向。
fn.call(thisArgs,arg1,arg2);//call接受一个参数列表，并运行
fn.apple(thisArgs,[arg1,arg2]);//apply接受一个参数数组，并运行
fn.bind(thisArgs,arg1,arg2);//bind接受一个参数列表，但不运行

## 