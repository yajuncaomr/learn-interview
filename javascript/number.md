# number类型

## "safe" Numbers 
```javascript
    Number.MAX_SAFE_INTEGER
    Number.MIN_SAFE_INTEGER

    Number.MAX_VALUE
    Number.MIN_VALUE

    Number.isSafeInteger()
```
## 确定一个数是整数

```javascript
    Number.isInteger()//es2015

    typeof v === 'number' && isFinite(v) && Math.floor(v) === v;
```

## 更改小数位数

```javascript
    v.toFixed(n);//n小数点后的位数，不传入n等同于toFixed(0)
    v.toPrecision(x)//x未从左边第一个不为0的数开始计算的位数，不传入x返回原始值
```

## 转换为指数形式（AKA科学计数法）

```javascript
    var num = 1111.3456;
    num.toExponential(4);//1.1113e+3
```

## 转换为其他进制

```javascript
    var num = 3241;
    var bin = num.toString(2)//110010101001
    num.toString(8)//6251

    Number.parseInt(bin,2)//3241
```

## 数字字面量方法

```javascript
    3241.toString(2)//syntax error
    (3241).toString(2)//110010101001
```

## NaN 是数值类型
```javascript
    typeof NaN === 'number'//true

    NaN == NaN//false
    NaN === NaN//false

    Object.is(NaN,NaN)//true

    isNaN(NaN)//true
    isNaN('aaa')//true

    Number.isNaN(NaN)//true
    Number.isNaN('aaa')//false
```

## ways to round a Number

```javascript
    const x = 5.921

    Math.floor(x)//5
    Math.ceil(x)//6

    Math.round(x)//6

    x.toFixed(2)//5.92
    x.toFixed(2)//5.9

    x>>0//5 x>0比Math.floor()快
    ~~x//5 
```

## 指数

```javascript
    2 ** 2 //4

    let x = 2;
    x **= 4;//16 ES7 same as x = x ** 4;

    Math.pow(2,4);
```

## 生成随机数

```javascript
    Math.random();

    Math.random() * 10 >> 0;//生成0-9的随机数
    Math.floor(Math.random()*10)//生成0-9的随机数

    const getRandom = (min,max) => Math.floor(Math.random() * (max - min - 1)) + min;

    const values = new Set();

    for()
```

## 