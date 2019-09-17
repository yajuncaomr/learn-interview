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
+ 

### 判断是否数组？
```javascript
obj && typeof obj === "object" && obj.construstor === Array;//方法一
Object.prototype.toString.apply(my_value) === '[object Array]';//方法二
Array.isArray(obj);//es6新方法
obj instanceof Array //不需要判断来自不同的frame
```

