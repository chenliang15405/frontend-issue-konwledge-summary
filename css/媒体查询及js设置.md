### 不同设备的屏幕进行css媒体查询/js设置

- 使用css控制不同的屏幕分辨率显示不同样式

  - css-媒体查询

    ```css
    /*注意：如果符合条件，则后面的会覆盖前面的, 所以将小的条件，放在最后
    	screen and (max-height: 700px)  表示：屏幕高度<=700
    	screen and (min-height: 800px)  表示：屏幕高度>=800
    */
    @media screen and (max-height: 700px) {
      .container {
        height: 195%;
      }
    }
    
    @media screen and (min-height: 800px) {
      .container {
        height: 158%;
      }
    }
    
    @media screen and (max-height: 600px) {
      .container {
        height: 200%;
      }
    }
    ```

  - js-document获取屏幕高度，并通过数据绑定来设置style或者class

    ```js
     this.heightPx = document.body.offsetHeight  //获取屏幕高度
     this.widthPx = document.body.offsetWidth   // 获取屏幕宽度
     console.log('屏幕高度', this.heightPx, this.widthPx)
    if(this.heightPx >=507){
      this.topHeight ="top:17.5rem"
    }
    if(this.heightPx<=508){
      this.zt= "font-size: 12px;"
      this.topHeight ="top:16rem"
    }
    
    ```

    ```js
    网页可见区域宽： document.body.clientWidth 或者 document.documentElement.clientWidth 
    在不同的浏览器的情况下获取高度
    
    document.getElementById("x-img-flag").style.height=h+"px";
    
    ```

    

