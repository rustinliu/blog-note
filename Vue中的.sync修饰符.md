## 为什么需要使用.sync

首先可以参考[官方文档对于.sync的解释](https://cn.vuejs.org/v2/guide/components-custom-events.html#sync-修饰符)，简单来说，就是因为子组件无法直接修改父组件传入的prop，如果直接修改，Vue会弹出一个警告，而且实际运行的效果也不是我们期望的，这时候就需要有一个办法来让我们能够实现子组件修改父组件传入的参数，这里可以使用之前跨对象通行的办法，用Vue自带的EventBus来解决这个问题。

## 举例说明

```js
<div id="app">
    <div>{{bar}}</div>
    <my-comp :foo.sync="bar"></my-comp>
    <!-- <my-comp :foo="bar" v-on:update:foo="bar=@event"></my-comp> -->
</div>
<script>
    Vue.component('my-comp', {
        template: '<div @click="increment">点我+1</div>',
        data: function() {
            return {copyFoo: this.foo}
        },
        props: ['foo'],
        methods: {
            increment: function() {
                this.$emit('update:foo', ++this.copyFoo); //发布自定义事件
            }
        }
    });
    new Vue({
        el: '#app',
        data: {bar: 0}
    });
</script>
```

以上就是一个使用`.sync`实现子组建修改父组件传入参数的例子，在这个例子里需要注意几点：

* 子组建采用`this.$emit（）`发布自定义事件，第一个参数为自定义事件名，格式必须为： `update：propname`，第二个参数为传入参数。
* ` <my-comp :foo="bar" v-on:update:foo="bar=@event"></my-comp>`中的`@event`即为子组件自定义事件第二个传入的参数，这里的@event不用加`this`
* `<my-comp :foo.sync="bar"></my-comp>`其实就是` <my-comp :foo="bar" v-on:update:foo="bar=@event"></my-comp>`的简写，也就是所谓的语法糖，表达的含义是完全相同的

以上就是对`.sync`的功能用法的简单讲解。