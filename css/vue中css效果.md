

### Vue中的css实现效果

- 路由切换过渡动画

  - html中使用

    - 如果是所有的路由使用：

      ```html
      <transition name="scaleUp" mode="out-in">
          <router-view></router-view>
      </transition>
      ```

    - 如果是单独的页面，在当前的组件中加入：

      ```html
      <transition name="scaleUp" mode="out-in">
        <div class="container">
        </div>
      </transition>
      ```

  - 过渡的css动画定义：

  ```css
  /*定义进出过程*/
  .scaleUp-enter-active, .scaleUp-leave-active {
    transition: 0.65s;
    position: absolute;
    top:0;
  }
  /*定义进入前与离开后状态*/
  .scaleUp-enter, .scaleUp-leave-to {
    /*渐渐消失*/
    opacity: 0;
    /*transform: translateX(-100%)  横向滑动*/
  }
  ```

- vue中切换页面，回到页面顶部

  ​	`main.js`中配置：

  ```js
  // 配置所有的页面
  router.afterEach((to, from, next) => {
    // 页面回到顶部
    window.scrollTo(0, 0);
  });
  ```