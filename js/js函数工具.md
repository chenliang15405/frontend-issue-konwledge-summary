### Js工具函数

- 获取url中参数

  ```js
  // 获取当前url中的参数
  function getQueryString(name) {
       return decodeURIComponent((new RegExp('[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)').exec(location.href) || [, ''])[1].replace(/\+/g, '%20')) || null;
  }
  
  // 获取指定url的参数
  function getQueryString(name, url) {
       return decodeURIComponent((new RegExp('[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)').exec(url) || [, ''])[1].replace(/\+/g, '%20')) || null;
  }
  
  // 获取当前url的参数
  getUrlQuery = (url = location.href) => { 
    try { 
      return [...new URL(url).searchParams].reduce( (pre, [key, value]) => Object.assign(pre, { key, value }), {}, ); 
    } catch { 
      throw new Error(`url格式不正确。url: ${url}`); 
    } 
  }
  ```

- js对象复制函数

  ```js
  // 使用es6 解构
  let {a, b, c} = objOld
  let objNew = {a, b, c}
  
  // 使用Object.assign
  Object.assign(target, source)
  
  // 自定义函数赋值
  Object.keys(objNew).forEach(key => {
    // 如果old没有，使用new中的默认属性，防止undefined
    objNew[key] = objOld[key] || objNew[key] 
  })
  ```


- 将分钟转化为时分

  ```js
  function dateTransfer(mins) {
    return parseInt(mins/60) + ":" + (mins%60>9?mins%60:"0"+mins%60); 
  }
  ```

  