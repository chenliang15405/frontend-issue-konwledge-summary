1. **React中的setState()接收对象和函数有什么区别？**

   React 为了优化性能，有可能会将多个 setState() 调用合并为一次更新。
   因为this.props和this.state 可能是异步更新的，你不能依赖他们的值计算下一个state(状态)。以下面的代码为例:

   ```js
   this.setState({
   	counter: this.state.counter + this.props.increment,
   });
   ```

   我们并不能通过上述代码得到想要的值，为了弥补这个问题，使用另一种 setState() 的形式，接受一个函数。这个函数将接收前一个状态作为第一个参数，应用更新时的 props 作为第二个参数，代码如下：

   ```js
   this.setState((prevState, props) => ({
   	counter: prevState.counter + props.increment
   }));
   ```

   可以看 https://www.jianshu.com/p/82b24113d549 有state的详细介绍

2. **React的render中可以使用If else的判断吗**

   不可以，可以使用三元运算符或者运算符(||、&&)

3. **React路由切换时同一组件无法重新渲染有什么方法**

   给路由组件添加key标示
   
4. **React生命周期函数**