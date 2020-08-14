# JSX基础语法知识点
- 如果是在render中定义的function，那么在标签中使用的话，直接{fucntionName()}即可
  如果是在render外定义的fucntion，即React实例中定义的funciton，那么在标签中使用，需要{this.functionName()}进行使用
  
- **react父组件异步加载传递数据，子组件如何接收**

  - 父组件异步传递过来的数据，子组件再`componentWillMount`和`componentDidMount`生命周期函数中无法获取到异步传递的值，并且生命周期函数只会执行一次，所以无法获取到

    - 解决方案：

    - 第一种：父组件传递数据过来之后，子组件不会全部重新渲染，只会重新渲染`render`函数，所以在`render`函数中`this.props.xxx`获取数据即可

    - 第二种：通过`componentWillReceiveProps`生命周期函数接收

      ```js
          componentWillReceiveProps(nextProps){
             console.log('nextProps', nextProps)
              setTimeout(() => {
                  this.setState({
                      stared: nextProps.isStar
                  })
              },0)
          }
      ```

      

