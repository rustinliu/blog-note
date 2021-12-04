## 什么是MVC

MVC模式是架构模式的一种，而且是一种非常重要的且经典的构架模式。

**MVC是三个单词的首字母缩写，它们是Model（模型）、View（视图）和Controller（控制）。**

这个模式认为，程序不论简单或复杂，从结构上看，都可以分成三层。

* 最上面的一层，是直接面向最终用户的"视图层"（View）。它是提供给用户的操作界面，是程序的外壳。

* 最底下的一层，是核心的"数据层"（Model），也就是程序需要操作的数据或信息。

* 中间的一层，就是"控制层"（Controller），它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

这三层是紧密联系在一起的，但又是互相独立的，每一层内部的变化不影响其他层。每一层都对外提供接口（Interface），供上面一层调用。这样一来，软件就可以实现模块化，修改外观或者变更数据都不用修改其他层，大大方便了维护和升级。

下面对各组成部分进行简单举例说明：

操作数据相关内容都放到m：

~~~js
const m = {
  data: { //数据
  },
  create() {},
  delete() {},
  update() {},
  get() {} //操作数据相关
}
~~~

 处理视图相关都放到v:

~~~js
const v = {
  el: null,  
  html: ``,//存放模版
  render(n) {
    //更新视图
  }
}
~~~

其他相关都放到c:

~~~js
const c = {
  init(container) {
    //初始化工作
  },
  events: {
    'click #add1': 'add',
    'click #minus1': 'minus',
    'click #mul2': 'mul',
    'click #divide2': 'div',
  }, //绑定事件表
  autoBindEvents() {
    //表驱动绑定事件
    }
  }
}
~~~

## EventBus 相关

Eventbus就是事件总线，JS实现事件总线的本质就是发布-订阅模式，达成任意组件间相互通信的作用。在一个地方触发（发布）事件，然后通过事件中心通知所有订阅者（订阅）。也就是说实现了对象间的通信

实现Eventbus的方法可以使用原生API也可以使用jQuery，但是eventbus实现的功能是一样的，都需要有类似如下API：

* $emit:创建触发事件，也可以用trigger表示
* $on:订阅事件，实现事件监听
* $off:解除事件绑定

## 表驱动编程

表驱动编程其实就是将代码里重复部分的合并到一个haspmap里面去，再通过forin或者forEach等其他方法来实现了，目的是使代码的复杂度保持稳定，同时也更加清晰，这里直接举例进行说明：

~~~js
let arr = [0,1,2,2,3,3,3,4,4,4,4,6];
let arr2 = arr.map( item=>{
  switch (item) {
    case 0 : return '周日';
    break;
    case 1 : return '周一';
    break;
    case 2 : return '周二';
    break;
    case 3 : return '周三';
    break;
    case 4 : return '周四';
    break;
    case 6 : return '周六';
    break;
    default : return '周五';
  }
})
console.log(arr2) // 
~~~

这段代码是将数组中的数字替换成星期几的，用switch实现，看起来很冗长，如果改成使用表驱动就变成了这样，

~~~JS
let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map((i)=>{
  const hash = {0:'周日',1:'周一',2:'周二',3:'周三',4:'周四',5:'周五',6:'周六'}
  return hash[i]
})
console.log(arr2)
~~~

光看起来就舒服多了，在DOM操作绑定事件中也可以使用这样的方法：

~~~js
    events: {
    'click #add1': 'add',
    'click #minus1': 'minus',
    'click #mul2': 'mul',
    'click #divide2': 'div',
  },
  autoBindEvents() {
    for (let key in c.events) {
      const value = c[c.events[key]]
      const spaceIndex = key.indexOf(' ')
      const part1 = key.slice(0, spaceIndex)
      const part2 = key.slice(spaceIndex + 1)
      v.el.on(part1, part2, value)
    }
  }
~~~

上述代码也是使用了表驱动减少了重复代码的书写。

## 模块化的理解

模块化的出现使用历史原因的，一开始JS是不支持模块化的，但是随着JS代码越来越臃肿和复杂，模块化的必要性就出来了，当然模块化的好处不只是单纯解决代码臃肿复杂的问题和实现团队分工，更重要的是实现了最小知识原则，也就是说引入一个模块不需要知道他做了什么，直接引入使用就可以了，非常的方便，同时使用模块也更方便我们进行解耦，因为模块与模块之前是独立的，相互之间不会影响，这也是模块化的一大好处。

关于JS模块化的AMD，CMD以及ES6的语法就不详细写了，资料是很多的

## 参考资料

* [谈谈MVC模式 - 阮一峰的网络日志 (ruanyifeng.com)](https://www.ruanyifeng.com/blog/2007/11/mvc.html)

