# 1. transform3d 闪烁
```js
- 问题描述: Chrome 开启硬件加速时 做一个类似硬币一样的东西 
当鼠标经过的时候 让这个圆形物体 翻转到背面 此时出现了闪烁(类似鬼畜一样。。。)
- 解决方法:
webkit- backface-visibility:hidden
webkit-perspective: 1000
```

