# 算法之排序  
冒泡排序、选择排序、插入排序、希尔排序、归并排序、快速排序、堆排序、计数排序、桶排序、基数排序。
## 冒泡排序  
1. 比较相邻的元素。如果第一个比第二个大，就交换他们的位置。
2. 对每一对相邻的元素做相同的工作，从开始的一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
3. 针对所有的元素重复上面的步骤，除了最后一个。
4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

代码  
```javascript
    function bubbleSort(arr){
        for(var i = 0;i < arr.length - 1;i++){
            for(var j = 0;j < arr.length - (i + 1);j++){
                var temp;
                if(arr[j] > arr[j + 1]){
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    //鸡尾酒排序(定向冒泡排序)
    function cocktailSort(arr){
        var i,left = 0,right = arr.length -1;
        var temp;
        while(left < right){
            for(i = left;i < right;i++){
                if(arr[i] > arr[i + 1]){
                    temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                }
            }
            right--;
            for(i = right;i > left;i--){
                if(arr[i] < arr[i - 1]){
                    temp = arr[i];
                    arr[i] = arr[i - 1];
                    arr[i - 1] = temp;
                }
            }
            left++;
        }
        return arr;
    }
```

## 选择排序(selectionSort)  
选择排序（selection sort）,首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序列的末尾。以此类推，直到所有元素均排序完毕。

```javascript
    function selectionSort(arr){
        for(var i = 0;i < arr.length -1;i++){
            var min = i;
            for(var j = i + 1;j < arr.length;j++){
                if(arr[min] > arr[j]){
                    min = j
                }
            }
            var temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
        return arr;
    }
```

## 插入排序（insertion sort）  
通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，通常采用in-place排序（即只需要O(1)的额外空间排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位为新元素提供插入空间。
```javascript
    function insertionSort(arr){
        for(var i = 1;i < arr.length;i++){
            var cur = arr[i];
            for(var j = i - 1;j >= 0;j-- ){
                if(cur < arr[j]){
                    arr[j + 1] = arr[j];
                }else{
                    break;
                }
            }
            arr[j + 1] = cur;
        }
        return arr;
    }

    function insertionSort(arr){
        for(var i = 1;i < arr.length;i++){
            var cur = arr[i];
            for(var j = i - 1;j >= 0 && cur < arr[j]>;j-- ){
                arr[j + 1] = arr[j];
            }
            arr[j + 1] = cur;
        }
        return arr;
    }
```
## 希尔排序（shell sort）  
希尔排序也称递减增量排序算法，是插入排序一种更高效的改进版本。  
希尔排序是基于插入排序的以下两点性质而提出改进方法的。
+ 插入排序在对几乎已经排好序的数据操作时，效率高，即可达到线性排序的效率。
+ 但插入排序是低效的，因为插入排序每次只能将数据移动一位。  
```javascript
    function shellSort(arr){
        var len = arr.length;
        var temp;
        for(var gap = Math.floor(len/2);gap > 0;gap = Math.floor(gap/2)){
            for(var i = gap;i < len;i ++){
                temp = arr[i];
                for(var j = i - gap; j >= 0 && temp < arr[j];j -= gap){
                    arr[j + gap] = arr[j]
                }
                arr[j + gap] = temp;
            }
        }
        return arr;
    }
```

## 归并排序（merge sort）  
归并排序是创建在归并操作上的一种有效的排序算法，效率为O(nlogn)。该算法是采用分治法（Divide and Conder）的一个非常典型的应用，且各层分治递归可以同时进行。  
采用分治法：
+ 分割：递归的把当前序列平均分割成两半。
+ 集成：在保持元素顺序的同时将上一步得到的子序列集成到一起。  
 
 递归法（Top-down）  
 1. 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
 2. 设定两个指针，最初位置分别为两个已经排序序列的起始位置
 3. 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
 4. 重复步骤3，直到某一指针到达序列尾
 5. 将另一序列剩下的所有元素直接复制到合并序列尾  

迭代法（Bottom-up）  
原理如下（假设序列共有n个元素）  
1. 将序列每相邻两个数字进行归并操作，形成ceil(n/2)个序列，排序后每个序列包含两/一个元素
2. 若此时序列数不是一个则将上述序列再次归并，形成ceil(n/4)个序列，每个序列包含四/三个元素
3. 重复步骤2，直到所有元素排列完毕  
```javascript
    //递归法
    function merge(left,right){
        var result = [];
        while(left.length > 0 && right.length > 0 ){
            if(left[0] > right[0]){
                result.push(right.shift())
            }else{
                result.push(left.shift())
            }
        }
        return  result.concat(left,right);
    }

    function mergeSort(arr){
        if(arr.length <= 1) return arr;
        var mid = Math.floor(arr.length/2);
        var left = arr.slice(0,mid);
        var right = arr.slice(mid);
        return merge(mergeSort(left),mergeSort(right));
    }

    //迭代法
```

## 快速排序（quick Sort）  
快速排序，又称划分交换排序。在平均状况下，排序n个项目要O(nlogn)次比较。在最坏情况下则需要O(n²)次比较，但这种情况并不常见。事实上快速排序通常明显比其他算法更快，因为它的内部循环可以在大部分的架构上很有效率的达成。

快速排序使用分治法（Divide and conquer)策略来把一个序列分为较小和较大的2个子序列，然后递归的排序两个子序列。

步骤为：  
1. 挑选基准值：从数列中挑出一个元素，称为基准
2. 分割:重新排序数列，所有比基准小的元素摆放在基准的前面，所有比基准大的元素摆在基准的后面（与基准值相等的数可以到任何一边）。在这个分割结束之后，对基准值的排序就已经完成。
3. 递归排列子序列：递归地将小于基准值元素的子序列和大于基准值元素的子序列排序。  
递归到最底部的判断条件是数列的大小是0或1，此时该数列显然已经有序。  
```javascript
    function quickSort(arr){
        var l = arr.length;
        if(l < 2) return arr;
        var basic = arr[0],left = [],right = [];
        for(var i = 1;i < arr.length;i++){
            var cur = arr[i];
            cur >= basic && right.push(cur);
            cur < basic && left.push(cur);
        }
        return quickSort(left).concat(basic,quickSort(right));
    }

    //不需要额外空间的原地排序版本
    function quickSort(arr,left,right){
        var len = arr.length,partitionIndex,
        left = typeof left != 'number' ? 0 : left;
        right = typeof right != 'number' ? 0 : right;

        if(left < right){
            partitionIndex = partition(arr,left,right);
            quickSort(arr,left,partitionIndex - 1);
            quickSort(arr,partitionIndex + 1,right);
        }
        return arr;
    }

    function partition(arr,left,right){
        var pivot = left,index = pivot + 1;
        for (var i = index; i <= right; i++) {
            if (arr[i] < arr[pivot]) {
                swap(arr, i, index);
                index++;
            }       
        }
        swap(arr, pivot, index - 1);
        return index-1;
    }

    function swap(arr, i, j) {
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
```

## 堆排序（heap sort）  
堆排序是指利用堆这种数据结构所设计的一种排序算法。堆是一个近似完全二叉树的结构，并同时满足堆积的性质：即子节点的键值或索引总是小于（或者大于）它的父节点。

堆节点的访问  
通常堆是通过一维数组来实现的。在数组起始位置为0的情形中：  
+ 父节点i的左子节点在位置(2i + 1);
+ 父节点i的右子节点在位置(2i + 2);
+ 子节点i的父节点在位置floor((i - 1)/2);

堆的操作  
在堆的数据结构中，堆中的最大值总是位于根节点（在优先队列中使用堆的话，堆中的最小值位于根节点）。堆中定义以下几种操作：   
+ 最大堆调整（Max Heapify）:将堆的末端子节点作调整，使得子节点永远小于父节点
+ 创建最大堆（Build Max Heap）:将堆中的所有数据重新排列
+ 堆排序（HeapSort）:移除位在第一个数据的根节点，并作最大堆调整的递归运算

```javascript
    function heapSort(arr){
        var len = arr.length;
        for(var i = Math.floor(len/2) - 1;i>=0;i--){
            max_heapify(i,len - 1);
        }

        for(var j = len -1;j > 0;j--){
            swap(0,j);
            max_heapify(0,j - 1);
        }
        function max_heapify(start,end){
            var left = 2 * start + 1;
            var right = 2 * start + 2;
            var largest = start;
            if(left <= end &&  arr[start] < arr[left]){
                largest = left;
            }
            if(right <= end && arr[start] < arr[right]){
                largest = right;
            }

            if(largest !== start){
                swap(start,largest);
                max_heapify(largest,end);
            }
        }

        function swap(i,j){
            var temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        return arr;
    }
```

## 计数排序（Counting Sort）  
是一种稳定的线性时间排序算法。  
1. 找出待排序的数组中最大和最小的元素。
2. 统计数组中每个值为i的元素出现的次数，存入数组C的第i项。
3. 对所有的计数累加（从C中的第一个元素开始，每一项和前一项，每一项和前一项相加）。
4. 反向填充目标数组：将每个元素i放在新数组的第C[i]项，每放一个元素就将C[i]减去1。

```javascript
    function countingSort(arr){
        var c = [];
        for(var i = 0; i < arr.length;i++){
            var m = arr[i];
            c[m] >= 1 ? c[m]++ : (c[m] = 1);
        }
        var d = [];
        for(var j = 0;j <c.length;j++){
            if(c[j]){
                while(c[j] > 0){
                    d.push(j);
                    c[j]--;
                }
            }
        }
        return d;
    }

    function countingSort(arr){
        var bucket = [];
        var sortIndex = 0;

        for(var i = 0;i < arr.length;i++){
            var m = arr[i];
            bucket[m] >= 1 ? bucket[m]++ : (bucket[m] = 1);
        }

        for(var j = 0;j <bucket.length;j++){
            console.log(j)
            while(bucket[j] > 0){
                arr[sortIndex++] = j;
                bucket[j]--;
            }
        }
        return arr;
    }
```

## 桶排序  
或箱排序，工作的原理是将数组分到有限数量的桶里。每个桶再个别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排序）。
1. 设置一个定量的数组作为空桶。
2. 寻访数列，并且把项目一个个的放到对应的桶中。
3. 对每个不是空的桶进行排序。
4. 从不是空的桶里把项目在放回原来的序列中。
 
 ```javascript
    function bucketSort(arr,num){
        var min = Math.min.apply(Math,arr);
        var max = Math.max.apply(Math,arr);
        var buckets = [];
        var bucketsNum = num || 5;
        var bucketsSize = Math.floor(max - min/bucketsNum) + 1;
        for(var i = 0;i < arr.length;i ++){
            var index = Math.floor(arr[i]/bucketsSize);
            !buckets[index] && (buckets[index] = []);
            buckets[index].push(arr[i]);
            var l = buckets[index].length;
            while(l > 0){
                buckets[index][l] < buckets[index][l - 1] && swap(buckets[index],l,l - 1);
                l--;
            }
        }
         
        arr = [];
        for(var j = 0;j < buckets.length;j++){
            arr = arr.concat(buckets[j]);
        }

        function swap(arr,i,j){
            var t = arr[i];
            arr[i] = arr[j];
            arr[j] = t;
        }
        return arr;
    }
 ```

 ## 基数排序（Radix sort）  
 是一种非比较型整数排序算法，其原理是将整数按位数切割成不同的数字，然后按每个位数分别比较。由于整数也可以表达字符串（比如名字和日期）和特定格式的浮点数，所以基数排序也不是只能使用于整数。  
 将所有待比较数值（正整数）统一为同样的数字长度，数字较短的数前面补零。然后从低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后，数列就变成一个有序数列。

 ```javascript
    function radixSort(arr){
        var max = Math.max.apply(Math,arr) + '';
        var digit = max.length;
        var start = 1;   
        var buckets = [];
         while(digit > 0){
             start *= 10;
             for(var i = 0;i < arr.length;i ++){
                 var index = Math.floor(arr[i]%start/(start/10));
                 !buckets[index] && (buckets[index] = []);
                 buckets[index].push(arr[i]);
             }
            arr = [];
             for(var j = 0; j < buckets.length;j++){
                 buckets[j] && (arr = arr.concat(buckets[j])); 
             }
             buckets = [];
             digit --
         }
         return arr;

    }
 ```



