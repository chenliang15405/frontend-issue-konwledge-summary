### Vue的v-for遍历中的自定义指令无效

#### 问题发现

在v-for循环中，通过自定义指令获取循环中每一项的值，然后进行处理，第一次进行v-for遍历，可以正常获取值，并渲染页面，但是list被重新赋值，第二次v-for遍历的时候，在页面中可以直接获取值，但是在指令中无法获取最新的值，只能获取比第一次遍历的List多的几个元素的值

#### 原因分析

**代码：**

```html
<div v-for="item,index in list" :key="index">
        <td >{{item.id}}</td>
        <td v-time="item.inputdate"></td>  
</div>
```

首先看v-for原理：

官方文档：

> 当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。这个类似 Vue 1.x 的 `track-by="$index"`。	

理解为：通过v-for渲染的dom元素，在元素数据改变的时候，不会重新渲染dom，而是直接更新数据

**原因：**

**问题的原因就是`:key='index'`，v-for循环是根据key的值的变化来更新vnode的!**

在第一次遍历的时候，渲染出来的div的key时1，2，3， 第二次重新赋值list，然后渲染的时候，key为1，2，3，4，5(第二次的list比第一次多2个元素)，所以1，2，3这几个的dom节点认为是没有改变，所以指令获取vnode的数据是没有更新的，只会获取多的新节点的数据

#### 解决方案

1. 第一种方式：

   ```html
   // 给key一个每次不同的key
   <div v-for="item,index in list" :key="item.id">
           <td >{{item.id}}</td>
           <td v-time="item.inputdate"></td>  
   </div>
   ```

   给v-for的key一个每次都不重复的值，保证每次的vnode节点是不同的

2. 第二种方式：

   ```js
   // 在指令中设置随机数赋值给当前的节点，保证当前vnode的每个节点的key不同
   bind: function (el, binding, vnode) {
    // bind中的vnode里面的key可以给设置一个随机数，这样每次都会更新虚拟节点。
    let num = parseInt(Math.random() * 1000)
    vnode.key = num
     
    // 获取binding中的value，就会每次都是最新的
    console.log(binding.value)
   }
   ```

3. 第三种方式：

   在directives中，指令的钩子函数说明：

   > `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
   >
   > `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

   在节点数据更新的时候，会调用update函数，在第一次渲染的时候，调用bind函数

   所以，解决方法—>定义update函数，做和bind相同的处理即可，如果为了提升性能，可以在update中，比较oldValue和value是否相同决定是否重新更新

   ```js
   directives: {
         time: {
           bind: function(el, binding) {
             el.innerHTML = binding.value + '时间'
           },
           update: function(el, binding) {
             console.log(binding)
             el.innerHTML = binding.value + '时间'
           }
         }
       }
   ```

   