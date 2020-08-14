### 动态绑定Class

- 如果只有一个class

  `<div className={index===this.state.currentIndex?"active":null}>此标签是否选中</div>`

- 如果有多个class

  `<div className={["container tab", index===this.state.currentIndex?"active":null].join(' ')}>此标签是否选中</div>`

  **推荐使用ES6**

  ```html
  <div className={`container tab ${index===this.state.currentIndex?"active":null}`}>此标签是否选中</div>
  ```

  