### Vue-Router钩子函数

1. **全局**

   ```js
   // 前置守卫：
   beforeEach((to, from, next)=>{
   to：即将进入的路由对象
   form：当前导航正要离开的路由
   next()：进行管道中的下一个钩子
   })
   
   // 解析守卫：
   beforeResolve((to, from, next)=>{})
   
   // 后置守卫：
   afterEach((to,form)=>{}
             
   // 路由：
   beforeEnter((to, from, next)=>{})
   ```

2. **组件**

   ```js
   // 进入路由之前
   beforeRouteEnter (to, from, next) {
   // 在渲染该组件的对应路由被 confirm 前调用
   // 不！能！获取组件实例 this
   // 因为当守卫执行前，组件实例还没被创建
   }
   
   // 路由更新之前
   beforeRouteUpdate (to, from, next) {
   // 在当前路由改变，但是该组件被复用时调用
   // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
   // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
   // 可以访问组件实例 this
   }
   
   // 路由离开之前
   beforeRouteLeave (to, from, next) {
   // 导航离开该组件的对应路由时调用
   // 可以访问组件实例 this
   }
   ```

   



   