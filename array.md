
* 如何实现数组去重？
* 假设有数组 array = [1,5,2,3,4,2,3,1,3,4]
* 你要写一个函数 unique，使得
* unique(array) 的值为 [1,5,2,3,4]
* 也就是把重复的值都去掉，只保留不重复的值。
  
1. 不使用set,借鉴计数排序的原理
   ```
      let array = [1,5,2,3,4,2,3,1,3,4]
      const hash = []
      for( let i = 0; i < array.length; i++){
          hash[ array[i] = true]
      }
      const result = []
      for( let k in hash){
          result.push(k)
      }
      return result
   ```
 `缺点：此方法只支持数字或者字符串数组，如果数组里面有对象，比如array = [{number:1},2],就会出错`

2. 使用set
   
   ```
   unique = (array) =>{
       return [...new Set(array)] //或者return Array.from(new Set(array))
   }
   ```
 `缺点：API太新，旧浏览器不支持`

 1. 使用Map
    ```
    unique = (array) =>{
        let map = new Map();
        let result = [];
        for( let i = 0; i < array.length; i++){
            if(map.has(array[i])) {//判断map中是否已有该key
               continue
            }else{//如果map中没有该key，就加入result中
               map.set(array[i], true);
               result.push(array[i])
            }
        }
        return result
    }
    ```
`缺带：api太新，旧浏览器不支持`