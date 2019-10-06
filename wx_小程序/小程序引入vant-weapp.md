### 小程序中引入vant-weapp

> 小程序是基于ts来构建的初始化项目，如果是js构建的项目，可以直接省略后面的配置ts的步骤

1. 引入vant组件库

   官网：https://youzan.github.io/vant-weapp

   (1) 进入到项目的第二级文件夹，例如整个小程序的项目为PHMiniProgram，但是需要进入到里面的miniprogram这个文件夹中，然后执行

   `npm init` 初始化nom，会多出来一个package.json文件，提示的一些信息直接下一步即可

   (2) 安装vant

   `npm i vant-weapp -S --production`

   或

   `yarn add vant-weapp --production`

   (3) 配置小程序开发工具的npm构建

   在tools — build npm

   然后再右上角的详情中勾选  `use npm module`

   (4) 引入使用

   全局引入： 再app.json中配置需要引入的组件：

   ```json
     "usingComponents": {
       // 注意，如果是上述的安装方式，引入路径为：vant-wapp/xxx，xxx为需要引入的组件
       "van-button": "vant-weapp/button", 
       "van-tab": "vant-weapp/tab",
       "van-tabs": "vant-weapp/tabs"
     }
   ```

   

   （5）小程序 ts 和vant的配置解决

   ​    如果小程序使用ts构建的项目，那么再引入vant组件之后会报错，因为有一些ts的配置还是什么有点问题导致，并且ts编译的时候扫描的是miniprogram下面的所有的ts文件，在vant中有以 *.d.ts结尾的文件，所以会会出现一些问题。

    有两种解决方法；

   ​	(1) 直接exclude这些vant中的文件即可，让ts编译的时候不去编译这些文件

   ```json
   // tsconfig.json
   
   "exclude": [
       "node_modules",
       "miniprogram_dist",
       "**/*.spec.ts",
    +  "**/*.d.ts"
     ]
   
   ```

    

      (2) 网上找到的方法，没有尝试

   只需要把miniprogram_npm/vant-weapp里的组件文件夹都删除，

   之后再https://github.com/youzan/vant-weapp下载一份vant， 将dist文件夹（vant-weapp-dev\vant-weapp-dev\dist）中的文件复制到项目的miniprogram_npm/vant-weapp

   即下载一份vant，之后替换掉项目中的文件

   之后保存解决

