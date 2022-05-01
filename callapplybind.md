## call
----

* call:是`函数的正常调用方式，并指定下文this`
```
     function.call(obj,[param1[,param2]...[,paramN]]]])
```
* 调用call的对象，必须是个函数function
* call的第一个参数，是一个对象。function的调用者，将会指向这个对象。如果不传，则默认为全局对象window
* 第二个参数开始，可以接受任意个参数。每个参数会映射到相应位置的function的参数上。但是如果将所有的参数作为数组传入，它们会作为一个整体映射到function对应的第一个参数上，之后参数都为空。
```
     function func(a,b,c){}
     
     func.call(obj,1,2,3)
         //func接收到的参数实际上1，2，3
    
     func.call(obj,[1,2,3])
         //func接收的参数实际上[1,2,3]，undefined,undefined
```
* 采纳以参数列表的形式传入，而apply以参数数组的形式传入

## apply
----

* apply的作用和call一样，只是调用的时候，传参数的方式不同。`区别是apply接受的是数组的参数，call接受的是连续参数`

```
     function.apply(obj[,argArray])
```

* apply的调用者是函数function，并且只接收两个参数，第一个参数的规则与call一致。
* `第二个参数，必须是数组或类数组，它们会被转换成类数组，传入function中，并且会被映射到function对应的参数上。这是call与apply重要的区别。`

```
     function.apply(obj,[1,2,3])
        //function接收的参数实际上是1，2，3
    
    function.apply(obj,{
        0:1,
        1:2,
        2:3,
        length:3
    })
        //function接收的参数实际上是1，2，3

```


## bind
----

* bind()方法创建一个新的函数，在调用时设置this关键字为提供的值。并在调用新函数时，将给定参数列表作为原函数的参数序列的前若干项。

```
     function.bind(thisArg[,arg1[,...]])
```

* bind接受的参数与call一致，只是bind不会立即调用，它会生成一个新的函数，你想神恶魔时候调用就什么时候调用,而apply和call则是立即调用
```
     function add(a,b){
        return a+b
     }
     function sub(a,b){
         return a-b
     }

     add.bind(sub,5,3) 
        //这时，并不会返回8
     add.bind(sub,5,3)()
        //调用后，返回8
```

* 如果bind的第一个参数是null或者undefined，this就指向全局对象window。


## apply,call,bind三者的区别
----

* 三者都可以改变函数的this对象指向
* 三者第一参数都是this要指向的对象，如果没有这个参数或者参数为undefined或者Null,则默认指向全局window
* 三者都可以传参，但是apply是数组，而call是参数列表，且apply和call是一次性传入参数,而bind可以分为多次传入
* bind是翻会绑定this之后的函数，便于稍后调用;apply,call则是立即执行