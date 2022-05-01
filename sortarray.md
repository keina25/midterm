给出正整数数组 array = [2,1,5,3,8,4,9,5]
请写出一个函数 sort，使得 sort(array) 得到从小到大排好序的数组 [1,2,3,4,5,5,8,9]
新的数组可以是在 array 自身上改的，也可以是完全新开辟的内存。

不得使用 JS 内置的 sort API
```
    let countSort = arr =>{
        let hashTable ={}; max = 0; result = []
        for(let i = 0; i < arr.length; i++){
          if(!(arr[i] in hashTable)){
            hashTable[arr[i]] = 1
        }else{
            hashTable[arr[i]] += 1  //记录i出现的次数
        }
        if(arr[i] > max){max = arr[i]}
    }
    for(let j = 0; j<= max; j++){
        if(j in hashTable){
            for(let i = 0; i< hashTable[j]; j++){
               result.push(j)
            }
         } 
      }
    return result
    }
    console.log(countSort([2,1,5,3,8,4,9,5]))  //[1,2,3,4,5,8,9]
```

* 首先生成一个哈希表
* 每当发现一个新的数字i，旧将它记录一次
* 记录完之后，知道数组每个数出现与否或几次以及这个数组的最大值，然后开始从小到大循环遍历哈希表
* 如果过程中发现哈希表中有这个数字，就打印出来
* 这样就得到一串排序好的数组