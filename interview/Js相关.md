1. **JS实现深拷贝的方式**

   - 递归拷贝

     ```js
     //使用递归的方式实现数组、对象的深拷贝
     function deepClone1(obj) {
       //判断拷贝的要进行深拷贝的是数组还是对象，是数组的话进行数组拷贝，对象的话进行对象拷贝
       var objClone = Array.isArray(obj) ? [] : {};
       //进行深拷贝的不能为空，并且是对象或者是
       if (obj && typeof obj === "object") {
         for (key in obj) {
           if (obj.hasOwnProperty(key)) {
             if (obj[key] && typeof obj[key] === "object") {
               objClone[key] = deepClone1(obj[key]);
             } else {
               objClone[key] = obj[key];
             }
           }
         }
       }
       return objClone;
     }
     ```

   - Json方式

     ```js
     var _obj = JSON.stringify(obj),
     var objClone = JSON.parse(_obj);
     ```

   - Object.assign()

     如果对象是一级对象，则是深拷贝，如果是二级对象则为浅拷贝

   - 数组的拷贝

     slice()： 没有参数是拷贝数组，只有一个参数是从该位置起到结束拷贝数组元素，两个参数，拷贝从起始位置到结束位置的元素（不包含结束位置的元素：含头不含尾）

     如果数组的元素是一维，则为深拷贝，否则是浅拷贝
   
2. **后端直接返回10w数据到前端，前端如何渲染**

   使用懒加载和分页的方式

   - 每一屏只展示指定数量的数据，然后再用户下滑的时候，触发加载下一页的数据，**通过防抖函数优化**，区原始数组中加载下一页的数据，并渲染到页面

     因为一次性都加载到前端中，不需要每一页都请求数据，在内存中操作非常快，这样给用户的感觉就是有很多的数据，实际是通过分页的方式实现每次渲染少量数据

