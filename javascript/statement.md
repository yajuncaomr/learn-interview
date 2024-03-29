# statement(声明)

## let  
let 语句声明一个块级作用域的本地变量，并且可选的将其初始化为一个值。
### 描述  
**let**允许你声明一个作用域被限制在块级中的变量、语句或者表达式。与var关键字不同的是，var声明的变量只能是全局或者整个函数块的。
#### 作用域规则  
let声明的变量只在其声明的块或子块中可用，与var相似。二者之间最主要的区别在于var声明的变量的作用域是整个封闭函数。  
```javascript
    function varTest(){
        var x = 1;
        {
            var x = 2;//同样的变量
            console.log(x);//2
        }
        console.log(x);//2
    }

    function letTest(){
        let x = 1;
        {
            let x = 2;//不同的变量
            console.log(x)//2
        }
        console.log(x);//1
    }
```
在程序和方法的最顶端，let不像var一样,let不会在全局对象里新建一个属性。位于函数或代码顶部的var声明会给全局对象新增属性。
#### 模仿私有成员  
通过闭包和var创建的私有变量必须要有函数作用域(IIFE),使用let,只需要块级作用域。
#### 重复声明  
在同一个函数或块作用域中重复声明同一个变量会引起SyntaxError
#### 暂存死区  
let 被创建在包含该声明的（块）作用域顶部，一般被称为提升。与通过var声明的有初始值undefined的变量不同，通过let声明的的变量直到它们的定义被执行时才初始化。在变量初始化前访问变量会导致ReferenceError。该变量处在一个自块顶部到初始化处理的"暂存死区中"。
#### 暂存死区与typeof  
typeof 操作符作用于在暂存死区中的变量或抛出ReferenceError;

## const  
常量是块级作用域，很像使用let语句定义的变量。常量的值不能通过重新赋值来改变，并且不能重新声明。
### 描述  
此声明创建一个常量，其作用域可以是全局或本地声明的块。与var变量不同，全局常量不会变为全局对象的属性。必须在声明的同一语句中指定它的值。

const声明创建一个值的只读引用。只是变量的标识符不能重新分配。“暂存死区”适用于const;

# 函数和类
## function
## function*  
function*会定义一个生成器函数（generator function),它返回一个Generator对象。
### 描述  
生成器函数在执行时能暂停，后面又能从暂停处继续执行。调用 一个生成器函数并不会马上执行它里面的语句，而是返回一个这个生成器的迭代器（iterator)对象。当这个迭代器的next()方法被首次（后续）调用时，其内的语句会执行到第一个（后续）yield的位置为止，yield后紧跟迭代器要返回的值。或者如果用的是yield*,则表示将执行权移交给另一个生成器函数（当前生成器暂停执行）。

next()方法返回一个对象，这个对象包含两个属性：value和done,value属性表示本次yield表达式的返回值，done属性为布尔类型，表示生成器后续是否还有yeild语句，即生成器函数是否已经执行完毕并返回。

调用next()方法时，如果传入了参数，这个参数会传给上一条执行的yield语句左边的变量。

当在生成器函数中显式return时，会导致生成器立即变成完成状态，即调用next()方法返回的对象的done为true。如果return后面跟了一个值，那么这个值会作为当前调用next()方法返回的value值。

### 使用迭代器遍历二维数组并转换为一维数组
```javascript
    function* iterArr(arr){
        if(Array.isArray(arr)){
            for(let i;i < arr.length;i++){
                yield* iterArr(arr[i]);
            }
        }else{
            yield arr;
        }
    }
    var arr = ['a',['b','c'],['d','e']];
    //使用for-of遍历
    for(var x of iterArr(arr)){
        console.log(x);
    }

    //或者直接将迭代器展开
    var arr2 = ['a',['b',['c',['d','e']]]];
    var gen = iterArr(arr2);
    arr2 = [...gen];
```

## async function  
async function 用来定义一个返回AsyncFunction对象的异步函数。异步函数是指通过事件循环异步执行的函数，它会通过一个隐式的Promise返回其结果。

