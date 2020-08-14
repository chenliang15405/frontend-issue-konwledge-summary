### React优化项目加载

> Create-react-app 脚手架构建的项目优化

- **Path variable [contenthash] not implemented in this context: xxxx.[contenthash].css**

  修改之前：`    new ExtractTextPlugin('static/css/styles.[contenthash].css'),`

  **打包时报错**
  webPack 升级到 4.x导致
  extract-text-webpack-plugin 无法使用

  修改为：`new ExtractTextPlugin('static/css/styles.[md5:contenthash:hex:8].css')`

  因为webpack包含contenthash这个关键字

- **React.lazy与React-loaded使用**

  参考：https://blog.csdn.net/sophie_u/article/details/84645366

- **create-react-app中如何开启css模块化**



