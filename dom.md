# DOM 事件相关

## 什么是事件委托
----
* 给元素的某一个事件行为绑定方法，目的是行为触发会可以做点自己想做的事情
* 事件流又称为事件传播，描述的是从页面中接收事件的顺序。当一个事件发生后，会在子元素和父元素之间传播（propagation）。这种传播分成三个阶段：
  1. 事件捕获阶段（capturing phase）：事件从window对象自上而下向目标节点传播的阶段
  2. 处于目标阶段（target phase）：真正目标节点正在处理事件的阶段
  3. 事件冒泡阶段(bubbling phase)：事件从目标节点自下而上向window对象传播的阶段


## 怎么阻止默认动作
----
#### 浏览器的默认事件指的是浏览器自己的行为
* 比如在点击<a href = "#">的时候，浏览器跳转到指定页面
* 当滚动鼠标或按空格键和方向键时页面会向下滚动
* 阻止`x.preverntDefault()` 或 `window.event.returnValue = false`
```
let stopDefault = (e) =>{
    if(e && e.preventDefault){
        e.preventDefault();  //阻止默认浏览器动作
    }else{
        window.event.returnValue = false //IE中阻止函数器默认动作的方式
    }
    return false
}
```



## 怎么阻止事件冒泡
----
* 事件冒泡阶段与捕获阶段相反，冒泡阶段是从最具体的目标对象开始，一层一层地向上传递，直到window对象
* `addEventListener`方法默认就是从冒泡阶段执行事件处理程序
* 可以使用 `event.stopPropagation()` 方法阻止事件冒泡
  
```
    document.body.onclick = (ev) =>{
        console.log("body", ev)
    }
    outer.onclick = (ev) =>{
        console.log("outer", ev)
    }
    inner.onclick = (ev) =>{
        console.log("inner", ev)
    }
    center.onclick = (ev) =>{
        console.log("center", ev) 
        ev.stopPropagation()  //阻止冒泡，阻止之后再运行一下
    }
```

1. 当点击中间的center时，依次打印出center =>inner =>outer =>body
2. 若阻止冒泡，只打印出center
