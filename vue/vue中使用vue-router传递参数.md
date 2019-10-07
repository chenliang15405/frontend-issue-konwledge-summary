### Vue中使用vue-router跳转的参数传递

> 如果是编程式路由跳转，那么可以通过代码在跳转时传递参数，如果是通过router-line标签传递，可以直接通过to属性的path来传递参数

**1. 编程式跳转路由参数的传递**

* 通过`this.$router.push({name: 'name', params:{id:1}})`通过params传递参数，可以通过 `this.$route.params.id `这种获取
  不过需要的是这个路由的name来跳转，在router.js的配置中，不仅需要配置path，还要配置name

* 通过`this.$router.push({path: 'path', query: {id:1}})`通过`this.$route.query.id`获取参数

<font color=red>注意：</font> `path`是router.js中配置的路径的跳转链接 ， `path`是通过query传递参数,

​			 如果通过name来传递参数，那么在配置路由的时候（router.js中），也需			 要配置上参数name，并指定对应值

**2. 通过router-link标签的to属性传递参数**

通过在`router-link`的to属性中配置： `/path/:id`这种路径传递参数的方式，需要也在router.js中配置的 `/path/:id `这种跳转链接，然后再对应的路由页面中通过 `this.$route.params.id`获取

