小程序中View和Block上使用wx:for的区别：

```html
<view wx:for={{list}}>
  	{{index}}: {{item.name}}
 <view>
```

view相当于一个组件，会渲染到页面，即会渲染为这个样子：

```html
<view>1: test1</viewv>
<view>2: test2</viewv>
...
```



```html
<block wx:for={{list}}>
    {{index}}: {{item.name}}
 <block>
```

block相当于vue中的template和react中的fragment一样，是模版div，不会渲染在页面中，即会渲染为：

```html
1:test1 2:test2 ...
```

