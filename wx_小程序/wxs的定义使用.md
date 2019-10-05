### wxs的使用定义及使用方式



> 在wxml中并不支持使用js方式来改变数据或者做其他的事情，所以需要使用wxs来做一些js才可以做的事情，例如：vue中的filter  react中的jsx语法

1. wxs的定义及使用方式一

   在同一个wxml中定义并使用

   ```html
   <wxs module="info">
     // js代码
     var message = "hello word"
     
     function sum(num1, num2) {
     	return num1 + num2
     }
   
     module.exports = {
     	message: message,
     	sum: sum
     }
   </wxs>
   
   <view>{{info.message}}</view>
   <view>{{info.sum(20,30)}}</view>
   ```

2. wsx的定义及使用方式二

   > 在开发过程中，会有大量的wxs来使用，所以不会将wxs的代码写在wxml中，会单独写在一个文件或者目录中

   在.wxs文件中，可以不用`<wxs></wxs>`标签定义，就可以直接写wxs的代码

   使用方式：

   1. 在单独的wxs文件中定义对应的js代码

      ```js
      // info.wxs	
      
      	var message = "hello word"
        
        function sum(num1, num2) {
        	return num1 + num2
        }
      
        module.exports = {
        	message: message,
        	sum: sum
        }
      ```

      

   2. 在需要使用的wxml中引入对应的wxs文件即定义

   3. wxs中的src引入路径必须使用<font color=red>相对路径</font>

      ```html
      // 定义并引入对应的wxs文件
      <wxs src="../../wxs/info.wxs" module="info">
        
       
      <view>{{info.message}}</view>  
      <view>{{info.sum(20,30)}}</view>
      ```

      

      