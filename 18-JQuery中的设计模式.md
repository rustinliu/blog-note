##  jQuery获取网页元素

jQuery的基本设计思想和主要用法，就是**"选择某个网页元素，然后对其进行某种操作"**。这是它区别于其他Javascript库的根本特点。

使用jQuery的第一步，往往就是将一个选择表达式，放进构造函数jQuery()（简写为$），然后得到被选中的元素。

选择表达式可以是CSS选择器：

```js
$(document) //选择整个文档对象

　　$('#myId') //选择ID为myId的网页元素

　　$('div.myClass') // 选择class为myClass的div元素

　　$('input[name=first]') // 选择name属性等于first的input元素
```

也可以是jQuery[特有的表达式](https://www.jquery123.com/category/selectors/)：

```js
　$('a:first') //选择网页中第一个a元素

　　$('tr:odd') //选择表格的奇数行

　　$('#myForm :input') // 选择表单中的input元素

　　$('div:visible') //选择可见的div元素

　　$('div:gt(2)') // 选择所有的div元素，除了前三个

　　$('div:animated') // 选择当前处于动画状态的div元素
```

我们也可以使用各种[过滤器](https://www.jquery123.com/category/traversing/filtering/)对结果集进行进一步的筛选，缩小选择结果。

```js
　　$('div').has('p'); // 选择包含p元素的div元素

　　$('div').not('.myClass'); //选择class不等于myClass的div元素

　　$('div').filter('.myClass'); //选择class等于myClass的div元素

　　$('div').first(); //选择第1个div元素

　　$('div').eq(5); //选择第6个div元素
```

有时候，我们需要从结果集出发，移动到附近的相关元素，jQuery也提供了在DOM树上的[移动方法](https://www.jquery123.com/category/traversing/tree-traversal/)：

```js
　　$('div').next('p'); //选择div元素后面的第一个p元素

　　$('div').parent(); //选择div元素的父元素

　　$('div').closest('form'); //选择离div最近的那个form父元素

　　$('div').children(); //选择div的所有子元素

　　$('div').siblings(); //选择div的同级元素
```

## jQuery链式操作

jQuery的链式操作，就是指最终选中网页元素以后，可以对它进行一系列操作，并且所有操作可以连接在一起，以链条的形式写出来，比如:

```js
　$('div').find('h3').eq(2).html('Hello');
```

分解开来，就是下面这样：

```js
　　$('div') //找到div元素

　　　.find('h3') //选择其中的h3元素

　　　.eq(2) //选择第3个h3元素

　　　.html('Hello'); //将它的内容改为Hello
```



这是jQuery最令人称道、最方便的特点。它的原理在于每一步的jQuery操作，返回的都是一个jQuery对象，所以不同操作可以连在一起。

jQuery还提供了[.end()](https://www.jquery123.com/end/) 方法，使得结果集可以后退一步：

```js
　　$('div')

　　　.find('h3')

　　　.eq(2)

　　　.html('Hello')

　　　.end() //退回到选中所有的h3元素的那一步

　　　.eq(0) //选中第一个h3元素

　　　.html('World'); //将它的内容改为World
```

## 元素的操作：创建、复制和删除

jQuery创建新元素的方法非常简单，只要把新元素直接传入jQuery的构造函数就行了：

```js
　　$('<p>Hello</p>');

　　$('<li class="new">new list item</li>');

　　$('ul').append('<li>list item</li>');
```

* 复制元素使用[.clone()](https://www.jquery123.com/clone/)。

* 删除元素使用[.remove()](https://www.jquery123.com/remove/)和[.detach()](https://www.jquery123.com/detach/)。两者的区别在于，前者不保留被删除元素的事件，后者保留，有利于重新插入文档时使用。

* 清空元素内容（但是不删除该元素）使用[.empty()](https://www.jquery123.com/empty/)。

## 元素的操作：移动

jQuery提供两组方法，来操作元素在网页中的位置移动。一组方法是直接移动该元素，另一组方法是移动其他元素，使得目标元素达到我们想要的位置。

假定我们选中了一个div元素，需要把它移动到p元素后面。

第一种方法是使用[.insertAfter()](https://www.jquery123.com/insertAfter/)，把div元素移动p元素后面：

```js
$('div').insertAfter($('p'));
```

第二种方法是使用[.after()](https://www.jquery123.com/after/)，把p元素加到div元素前面：

```js
$('p').after($('div'));
```

表面上看，这两种方法的效果是一样的，唯一的不同似乎只是操作视角的不同。但是实际上，它们有一个重大差别，那就是返回的元素不一样。第一种方法返回div元素，第二种方法返回p元素。你可以根据需要，选择到底使用哪一种方法。

使用这种模式的操作方法，一共有四对：

* 　[.insertAfter()](https://www.jquery123.com/insertAfter/)和[.after()](https://www.jquery123.com/after/)：在现存元素的外部，从后面插入元素

* 　[.insertBefore()](https://www.jquery123.com/insertBefore/)和[.before()](https://www.jquery123.com/before)：在现存元素的外部，从前面插入元素

* 　[.appendTo()](https://www.jquery123.com/appendTo/)和[.append()](https://www.jquery123.com/append)：在现存元素的内部，从后面插入元素

* 　[.prependTo()](https://www.jquery123.com/prependTo/)和[.prepend()](https://www.jquery123.com/prepend)：在现存元素的内部，从前面插入元素

## 元素的操作：取值和赋值(包括对属性进行修改)

操作网页元素，最常见的需求是取得它们的值，或者对它们进行赋值。

jQuery会使用同一个函数，来完成取值（getter）和赋值（setter），即"取值器"与"赋值器"合一。到底是取值还是赋值，由函数的参数决定。

```js
$('h1').html(); //html()没有参数，表示取出h1的值

$('h1').html('Hello'); //html()有参数Hello，表示对h1进行赋值
```

常见的取值和赋值函数如下：

* [.html()](https://www.jquery123.com/html/) 取出或设置html内容

* [.text()](https://www.jquery123.com/text/) 取出或设置text内容

* [.attr()](https://www.jquery123.com/attr/) 取出或设置某个属性的值

* [.width()](https://www.jquery123.com/width/) 取出或设置某个元素的宽度

* [.height()](https://www.jquery123.com/height/) 取出或设置某个元素的高度

* [.val()](https://www.jquery123.com/val/) 取出某个表单元素的值

我们使用[.attr()](https://www.jquery123.com/attr/) 来实现对元素属性的修改，比如：

```js
$('#mylink').attr('href','http://www.baidu.com'); //修改a标签的herf属性
```

另外需要注意的是，如果结果集包含多个元素，那么赋值的时候，将对其中所有的元素赋值；取值的时候，则是只取出第一个元素的值（[.text()](https://www.jquery123.com/text/)例外，它取出所有元素的text内容）。

## 元素的操作：CSS属性操作

jQuery 进行 CSS 操作的方法有如下几个：

- [.addClass()](https://www.jquery123.com/addClass/#addClass-className) - 向被选元素添加一个或多个类
- [.removeClass()](https://www.jquery123.com/removeClass/#removeClass-className) - 从被选元素删除一个或多个类
- [.toggleClass()](https://www.jquery123.com/toggleClass/#toggleClass-className) - 对被选元素进行添加/删除类的切换操作
- [.css()](https://www.jquery123.com/css/#css-propertyName)设置或返回样式属性

这里的[.css()](https://www.jquery123.com/css/#css-propertyName)需要单独记忆一下，它也是一个"取值器"与"赋值器"合一的函数，使用方法如下：

```JS
$("p").css("background-color"); //获取CSS属性
$("p").css("background-color","yellow"); //设置CSS属性
$("p").css({"background-color":"yellow","font-size":"200%"}); //设置多个CSS属性，每个属性采用键值对形式，用逗号隔开
```

## 参考资料

* [jQuery设计思想 - 阮一峰的网络日志 (ruanyifeng.com)](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)

* [jQuery API 中文文档 | jQuery 中文网 (jquery123.com)](https://www.jquery123.com/)

