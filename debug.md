## 1. transform3d 闪烁
```js
- 问题描述: Chrome 开启硬件加速时 做一个类似硬币一样的东西 
当鼠标经过的时候 让这个圆形物体 翻转到背面 此时出现了闪烁(类似鬼畜一样。。。)
- 解决方法:
webkit- backface-visibility:hidden
webkit-perspective: 1000
```
## 2.antd mobile-v2 轮播图滑动报错
```js
1.使用react 17.0以下版本
2.node_modules
carousel.js  400行  注释掉：e.preventDefault()
```

## 3.vuepress 无法使用 上次git上传时间
```js
/Users/eternallycyf/Documents/GitHub/case/pluviophobe-vue-document/node_modules/@vuepress/plugin-last-updated/index.js
const lastUpdated = dateFormat(timestamp, 'yyyy-MM-dd hh:mm:ss')
自己重新定义一个时间过滤的函数
```

