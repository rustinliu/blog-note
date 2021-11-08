## 数组究竟是什么

* js其实没有真正的数组，而使用对象模拟的数组
* 典型的数组
  * 元素的类型相同
  * 使用连续的内存存储
  * 通过数字下标获取元素
* JS的数组
  * 元素的类型可以不同
  * 内存不一定是连续的（对象是随机存储的）
  * 不能通过数字下标获取，而是通过字符串获取
    * 这意味着数组可以有任意KEY，比如 `let a = [1,2,3] a['xxx']=xxx`在JS中是完全合法的
* 如何创建一个数组
  * 新建
    * `let a = [1,2,3]`
    * `let a = new Array(1,2,3)`
    * `let a = new Array(3)`
  * 转化
    * `let a = '1,2,3'.spite(',')`
    * `let a = '123'.spite()`
    * `Array.from('123')`
  * 伪数组
    * `let divlist =document.queryselctorAll('div')`
    * 伪数组的原型链中并没有数组的原型，需要进行转化（使用Array.from()）才能使用数组的方法
  * 合并两个数组得到一个新数组
    * arr1.concat(arr4)
  * 截取数组的一部分成为新数组
    * Arr.slice(1)//从第二个元素开始
    * arr.slice(0)//全部截取，是拷贝的方法
    * **注意，JS只提供浅拷贝** 

## 数组元素的删除

* 可以使用对象一样的方法 `delete arr[0]` ,但是**数组的长度不会改变**，会产生一个稀疏数组，但是不推荐这样做
* 修改length可以直接删除长度后面的元素，也不推荐这样做
* 推荐的做法
  * 删除第一个元素：`arr.shift() //arr被修改，返回第一个元素`
  * 删除最后一个元素： `arr.pop()//arr被修改，返回最后一个元素`
  * 删除中间的元素：
    *  `arr.splice(index,1)//删除index的第一个元素`
    *  `arr.splice(index,1,'x')//删除index的第一个元素并在此位置添加'x'`
    *  `arr.splice(index,1,'x','y')//删除index的第一个元素并在此位置添加'x','y'`
    * 此方法会修改原数组

## 遍历数组

* 使用for循环
  * `for（let i = 0;i < arr.length;i++ ）{...}`
* 使用forEach
  * `arr.forEach(function(item,index,arr){...})`
  * 和for的对比
  * 首先：for循环里面是有 break，continue等方法的，forEach是没有的
  * 其次：for是一个关键字，里面的是一个块作用域，而forEach是一个函数，里面的是一个函数作用域
* 查看单个属性
  * 使用下表读取，a[1]，注意此时1会在JS内部被强制转化成字符串形式
    * 索引越界问题
      * 读取了length的属性就会越界，因为undefine不能使用testing()方法，所以此时会报错，一定要注意这一点
  * 查看单个元素是否存在
    * `arr.indexOf(item) //存在返回index，不存在返回-1`
  * 使用条件查找元素
    * `arr.find(item=>item%2 === 0)//找第一个偶数`
  * 使用条件查找元素的索引
    * `arr.findindex(item=>item%2===0))//找第一个2偶数的索引`

## 数组元素的增加

* 在尾部添加元素
  * arr.push(newitem) //修改arr，返回新长度
  * arr.push(item1,item2)//修改arr，返回新长度
* 在头部添加元素
  * arr.unshift(newitem) //修改arr，返回新长度
  * arr.unshift(item1,item2)//修改arr，返回新长度
* 在中间添加元素
  * arr.splice(index,0,'x' )// 在index除插入'x'
  * arr.splice(index,0,'x' ,'y')// 在index除插入'x','y'

## 反转顺序

* 反转数组
  * arr.reverse() //会修改原数组
    * 反转一个字符串 `string.split(' ').reverse().join(' ')`
  * 自定义顺序
    * Arr.sort((a,b)=>a-b)

## 数组的变换

* map() n变n
* filter() n变少
* reduce() n变1

