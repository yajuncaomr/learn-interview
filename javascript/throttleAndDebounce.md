### throttle and debounce(节流与防抖)

节流（throttle）：限制函数的执行频率，在一定时间内只执行一次。

防抖（debounce）：调用函数后，在指定时间内没有再次调用才会执行。

两者的不同[看这里](https://stackoverflow.com/questions/25991367/difference-between-throttling-and-debouncing-a-function "throttle与debounce有什么不同")

#### throttle简单实现  
```javascript
    //节流函数
    function throttle(fn,throttleHold){
        throttleHold || (throttleHold = 250)
        var lastcall,timeoutId;
        return function(){
            var self = this,args = arguments;
            var now = Date.now();
            if(lastcall && now < lastcall + throttleHold){
                clearTimeout(timeoutId);
                timeoutId = setTimeout(function(){
                    fn.apply(self,args);
                    lastcall = now;
                },throttle);
            }else{
                fn.apply(self,args);
                lastcall = now;
            }
            
        }
    }

```
#### debounce简单实现
```javascript
//stackoverflow上的实现
function debounce(func, wait, immediate) {
    var timeout;
    return function () {
        var context = this, args = arguments;
        var later = function () {
            timeout = null;
            if (!immediate) func.apply(context, args);
        };
        var callNow = immediate && !timeout;
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
        if (callNow) func.apply(context, args);
    };
};
```
