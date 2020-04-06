# Vue使用params方式传参数据丢失



### 1. Vue-router传递参数的方式

- query传递参数

  > query传递参数不会出现路参数丢失的情况，所以不需要做其他的配置，不过缺点就是参数会拼接在url后面: url?xx=yy 这种方式来传递参数，会暴露参数，并且url也有字符上限限制

  使用方式：

  `this.$router.push({path: 'path', query: {id:1}})`

  获取参数：

  `this.$route.query.id`获取key为id的路由参数

- params传递参数

  > params传递参数是将参数放在route对象中，没有放在url后面，但是会有一个问题，在跳转之后的页面中刷新的时候，会导致当前路由中保存的params的参数丢失

  使用方式：

  `this.$router.push({name: 'name', params:{id:1}})`

  获取参数:
  `this.$route.params.id` 获取route对象中的Params的参数信息

### 2. 解决使用params传递参数刷新页面参数丢失

> 使用params传递参数，参数没有像query那样，拼接在url后面，所以刷新的时候会出现数据丢失，则无法获取到数据

有两种方式可以解决：

- 使用sessionStorage、localStorage

  - sessionStorage、localStorage根据具体的场景来选择，保存到里面的数据不会在刷新下的时候丢失，不过在移动端，使用微信悬浮窗的时候，部分安卓机型的sessionStorage中的数据会丢失

- 使用params中的路由匹配

  - 使用方式: 在router.js，即匹配路由规则的位置，加上占位符即可

    ```js
    {
      path: '/index/:num/:name',
      name: 'index',
      component: Index
    }
    ```

    params中的参数名称需要和占位符的名称一致即可

  - 获取参数，还是和获取params中参数一致：`this.$route.params.name`

  - 这样的话，参数就会出现在url中，格式为：url/num/name，这种方式将参数放在url上，刷新的时候才不会丢失数据。

  