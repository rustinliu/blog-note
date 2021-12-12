## computed的作用及写法

* 写法：`{ [key: string]: Function | { get: Function, set: Function } }`

* 用途：被计算出来的属性就是计算属性
* 示例：
  * [用户名展示](https://codesandbox.io/s/compassionate-lake-xyjkw)
  * [列表展示](https://codesandbox.io/s/bold-matsumoto-efn0i)

* 特点：

  * **计算属性具有缓存**。计算属性是基于它们的**依赖**进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要**依赖值**都没有发生改变，多次访问计算属性会立即返回之前的计算结果，而不必再次执行函数。

  

## watch的作用及写法

* 写法：

  * 语法一

  watch {

  ~~o1:()=>{},~~(this指向不对，不建议使用)

  o2:function(value,oldvalue){},

  o3(){},

  o4[fn1,fn2],

  o5:'methodName',

  o6:{

  Handler:fn,deep:true,immediate:true

  }

  'object.a':function(){}

  }

  * 语法二
    * vm.$watch('xxx',fn,{deep:...,immediate:...})
    * 'XXX'可以改成返回字符串的函数

* 用途：一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 `$watch()`，遍历 watch 对象的每一个 property。
* 示例：
  * [撤销](https://codesandbox.io/s/lucid-shamir-cpcw3)（此例说明watch是异步的）
  * [模拟computed](https://codesandbox.io/s/objective-star-vu2h3)
* 特点：
  * 不要使用箭头函数，this的指向不是期望的
  * 在选项参数中指定 `immediate: true` 将立即以表达式的当前值触发回调
  * 为了发现对象内部值的变化，可以在选项参数中指定 `deep: true`。注意监听数组的变更不需要这么做。

