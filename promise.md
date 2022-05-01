# Promise

## promise的用途
----

* Promise 是一个对象，它代表一个异步操作的最终完成或者失败.
* 本质上Promise 是一个函数返回的对象，可以再它上面绑定回调函数，这样就不需要再一开始把回调函数作为参数传入这个函数。
* 好处： 
       1. 回调的名字和顺序规范
       2. 避免回调地狱，让代码可读性更强
       3. 方便捕获错误


## 如何创建一个 new Promise
----

```
     return new Promise ((resolve,reject) => {})
```

## 如何使用Promise.prototype.then
----

* then()方法接受两个函数，成功的时候执行第一个函数，失败的时候执行第二个函数

```
    const promise1 = new Promise((resolve, reject) =>{
        resolve('success')
    })

    promise.then((vale) => {
        console.log(value)
    })  //success
```

* then方法接受两个函数（注意是函数，不要直接调用函数，调用函数会立即执行）
* 成功的时候执行第一个函数，失败的时候执行第二个函数

## 如何使用Promise.all
----

```
     const promise1 = Promise.resolve(3)
     const promise2 = 42
     const promise3 = new Promise((resolve, reject)=>{
         setTimeout(resolve, 100, 'foo')
     })

     Promise.all([promise1, promise2, promise3]).then((values) =>{
         console.log(values)
     })
      
    //[3,42,"foo"]
```
* Promise.all 需要传入一个数组，数组中的元素都是Promise 对象，当这些对象都执行成功，执行then中的第一个函数（成功函数），失败时只能获得第一个失败Promise 的错误数据
* Promise.all 是大家一起到重点，一个失败全都失败

## 如何使用Promise.race
----

```
    const promise1 = new Promise((resolve, reject) =>{
        setTimeout(resolve, 500, "one")
    })

    const promise2 = new Promise((resolve, reject) =>{
        setTimeout(resolve, 100, "two")
    })

    Promise.race([promise1, promise2]).then((value) =>{
        console.log(value)  //哪个结果能更快获取？
    })

    //"two"
```

* Promise.race 和 Promise.all 相对应，哪个Promise 对象最快得到结果，就最先用水的结果（只要快就行，不管失败还是成功）
