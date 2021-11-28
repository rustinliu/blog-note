## 基于原型链的继承

示例如下：

~~~js
// 父级构造函数
function Shape() {
  this.x = 0;
  this.y = 0;
}

// 父级构造函数的原型对象
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};

// 子级构造函数
function Rectangle() {
  Shape.call(this); // 继承第一步：这里用call和apply都可以，目的是使子类实例具有父类实例的属性。
}

Rectangle.prototype = Object.create(Shape.prototype);//继承第二步：利用create把父级构造函数的原型对象添加到子对象的原型链上
Rectangle.prototype.constructor = Rectangle;//继承第三步：把子级构造函数的原型对象的constructor重新指回到子级构造函数上
~~~

一共就这三步，这里就会有疑问了，第二步为什么要用create而不是直接用`Rectangle.prototype =Shape.prototype`呢？这是因为如果直接等于的话那么之后对于`Rectangle.prototyp`的修改（比如第三步的constructor以及添加新方法等）也会导致`Shape.prototype`的修改，这就可能出问题了。

## 基于class的继承

示例如下：

~~~js
// 父级class
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    add() {
        this.x += this.x;
        this.y += this.y;
        console.log(this.x, this.y);
    }
}

// 子级class
class Son extends Father {   //第一步：使用extends关键词
    constructor(x, y, z) {
        super(x, y); //第二步：使用super来表示父类构造函数，用来新建父类的this
        this.z = z;
    }
    sonadd() {
        super.add();
        this.z += this.z;
        console.log(this.x, this.y, this.z);
    }
}
~~~

注意点：

* 子类必须在`constructor`方法中调用`super`方法，否则新建实例时会报错。这是因为子类自己的`this`对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。
* 在子类的构造函数中，只有调用`super`之后，才可以使用`this`关键字，否则会报错。