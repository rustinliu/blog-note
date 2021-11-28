## Promise的用途

promise 是异步编程的一种解决方案，promise可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。

## 创建promise

~~~js
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
~~~

## Promise.prototype.then() 的用法

then()用来执行回调函数，它最多需要有两个参数：Promise 的成功和失败情况的回调函数，并且then方法里也可以返回promise对象，这样就可以链式调用了。

语法如下：

~~~js
p.then(onFulfilled[, onRejected]);
~~~

示例如下：

~~~js
var Pro = function (time) {
    //返回一个Promise对象
    return new Promise(function (resolve, reject) {
        console.log("123");
        //模拟接口调用
        setTimeout(function () {
            //这里告诉Promise 成功了，然后去执行then方法的第一个函数
            resolve("成功返回");
        }, time);
    });
};
(function () {
    console.log("start");
    Pro(3000)
        .then(function (data) {
            console.log(data);
            return Pro(5000);
        })
        .then(function (data) {
            console.log(data);
            console.log("end");
        });
})();
//依次输出：
//start
//123
//成功返回
//123
//end
~~~

## Promise.all() 的用法

Promise.all() 方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。个 Promise 的resolve回调执行是在所有输入的promise的resolve回调都结束，或者输入的iterable里没有promise了的时候。它的reject回调执行是，只要任何一个输入的promise的reject回调执行或者输入不合法的promise就会立即抛出错误，并且reject的是第一个抛出的错误信息。

语法如下：

~~~js
Promise.all(iterable);
~~~

iterable指可迭代对象，如Array等

示例如下：

~~~js
let p1 = new Promise(function (resolve, reject) {
    resolve(1);
});
let p2 = new Promise(function (resolve, reject) {
    resolve(2);
});
let p3 = new Promise(function (resolve, reject) {
    resolve(3);
});
Promise.all([p1, p2, p3])
    .then(function (results) {
        console.log("success:" + results);
    })
    .catch(function (r) {
        console.log("error");
        console.log(r);
    });
//输出：success:1,2,3
~~~

## Promise.race() 的用法

Promise.race() 方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。一旦迭代器中的某个promise解决或拒绝，返回的 promise就会解决或拒绝，也就是说取决于最先改变状态的promise实例。

语法与all类似：

```js
Promise.race(iterable);
```

iterable指可迭代对象，如Array等

示例如下：

```js
var p1 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 500, "one");
});
var p2 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 100, "two");
});

Promise.race([p1, p2]).then(function(value) {
  console.log(value); // "two"
  // 两个都完成，但 p2 更快
});

var p3 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 100, "three");
});
var p4 = new Promise(function(resolve, reject) {
    setTimeout(reject, 500, "four");
});

Promise.race([p3, p4]).then(function(value) {
  console.log(value); // "three"
  // p3 更快，所以它完成了
}, function(reason) {
  // 未被调用
});
```

