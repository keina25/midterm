# 闭包

### 什么是闭包？
----
* 一个函数和对其周围状态的引用捆绑在一起，或者说函数被引用包围,简单来说，就是声明一个变量，声明一个函数，在函数内部访问外部的变量，那么，这个函数+这个变量叫做闭包（closure）。

<pre><code>    
    let a = "1"
    let b = function(){
        console.log(a)
    }    
</code></pre>

### 闭包的用途
----
1. 从外部读取内部的变量
   
<pre><code>
     function f1(){
         let n = 666
         function f2(){
             console.log(n)
         }
         return f2()
    }
     let result = f1()
     result()   ///666
</code></pre>

2. 让这些变量的值始终保持在内存中，不会再function调用后被自动清除,封装对象的是私有属性和私有方法
   
<pre><code>
function f1(n){
    return function(){
        return n++
    }
}
var a1 = f1(1)
     a1()  //1
     a1()  //2
     a1()  //3
var a2 = f1(5)
     a2()  //5
     a2()  //6
     a3()  //7
</code></pre>

* a1 和 a2 是相互独立性。n 是闭包的变量。
* 每次调用一次计数，通过改变这个变量的值，会改变这个闭包的环境。每一次闭包内的变量的修改，不会影响另一个闭包中的变量。


### 闭包的优点
----

* 优点：可以避免全局变量的污染

### 闭包的缺点
----

1. 如果不是某些特定的任务需要使用闭包，在其他函数中创建函数是不明智的，变量都会被保存在内存中，会增大函数中内存的消耗，因此闭包在处理速度和内存消耗方面，会造成对网页的性能问题。解决方法，退出函数之前，将不使用的局部变量全部删除

2. 闭包会在父函数外部，改变父函数内部的变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（public method），把内部变量当作它私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。 

## 引用 
>https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
>https://www.cnblogs.com/cxying93/p/6103375.html