# React组件之间传递数据的知识点

- 组件之间传递数据的类型定义和默认属性

  在react的组件之间，可以设置默认的props和定义props-type

  - 定义默认的props（defaultProps）

    ```js
    static defaultProps = {
      title: 'github',
      icon: 'github icon' 
    }		
    ```

  - 如果是函数式组件（无状态组件），可以通过这种方式：

    ```js
    xxx.defaultProps = {
       title: 'github'
    };
    ```

  
定义了defaultProps，那么如果没有传递该props的话，就会使用defaultProps进行渲染
  
- 定义props的类型(PropTypes)
  
  ```js
    import PropTypes from 'prop-types'
     ...
      static propTypes = {
         title: PropTypes.string.isRequired,
         icon: PropTypes.stiring.isRequired
      }
     ...
    ```
  
  如果类型不正确或者没有该属性，则会报错