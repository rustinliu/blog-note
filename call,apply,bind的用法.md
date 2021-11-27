首先要知道[call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)、[apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)、[bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) 的主要作用都是改变this的指向，下面介绍它们的具体区别和使用方法

### call

call 的写法:`Function.call(obj,[param1[,param2[,…[,paramN]]]])`

需要注意以下几点：

- 调用 call 的对象，必须是个函数 Function。

- call 的第一个参数，是一个对象。 Function 的调用者，将会指向这个对象。如果不传，则默认为全局对象 window。

- 第二个参数开始，可以接收任意个参数。每个参数会映射到相应位置的 Function 的参数上。但是如果将所有的参数作为数组传入，它们会作为一个整体映射到 Function 对应的第一个参数上，之后参数都为空。

  ~~~js
  function func (a,b,c) {}
  
  func.call(obj, 1,2,3)
  // func 接收到的参数实际上是 1,2,3
  
  func.call(obj, [1,2,3])
  // func 接收到的参数实际上是 [1,2,3],undefined,undefined
  ~~~

### apply

apply的写法`Function.apply(obj[,argArray])`

需要注意的是：

- 它的调用者必须是函数 Function，并且只接收两个参数，第一个参数的规则与 call 一致。
- 第二个参数，必须是数组或者类数组，它们会被转换成类数组，传入 Function 中，并且会被映射到 Function 对应的参数上。这也是 call 和 apply 之间唯一的区别

~~~js
func.apply(obj, [1,2,3])
// func 接收到的参数实际上是 1,2,3

func.apply(obj, {
    0: 1,
    1: 2,
    2: 3,
    length: 3
})
// func 接收到的参数实际上是 1,2,3
~~~

### bind

bind的写法：`Function.bind(thisArg[, arg1[, arg2[, ...]]])`

bind 方法 与 apply 和 call 比较类似，也能改变函数体内的 this 指向。不同的是，**bind 方法的返回值是函数，并且需要稍后调用，才会执行**。而 apply 和 call 则是立即调用。

来看下面这个例子：

```js
function add (a, b) {
    return a + b;
}

function sub (a, b) {
    return a - b;
}

add.bind(sub, 5, 3); // 这时，并不会返回 8
add.bind(sub, 5, 3)(); // 调用后，返回 8
```

### 总结

从上面可以看到，appl、call、bind三者的区别在于：

- 三者都可以改变函数的this对象指向
- 三者第一个参数都是 this 要指向的对象，如果如果没有这个参数或参数为undefined或null，则默认指向全局window
- 三者都可以传参，但是apply是数组，call是参数列表，且apply和call是一次性传入参数，而bind可以分为多次传入
- bind 是返回绑定this之后的函数，apply 、call 则是立即执行