### 同步与异步的区别

return new promise((resolve,reject)=>{})











### JSONP

在跨域时因为种种原因无法使用cors，我们必须使用一个其他方式来进行跨域，于是我们请求一个JS文件，这个JS文件里面会有回调（callback），这个回调里面就有我们需要的数据，这个回调的名称不是固定的，我们通过请求JS的参数设置名称，引用时会把这个名称传给后台，然后后台回再次返回给我们并执行。

优点

* 兼容IE
* 跨域

缺点

* script标签不是AJAX不能读到精确的状态，比如状态码这些的都不支持，只知道成功或者失败了，onload，onerror这种
* **JSONP不支持POST**