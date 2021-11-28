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

## 4.react return 加注释就报错
```js
# 1
const Hello = ()=> {
  return (
    // 这里加注释就报错
  )
}
# 2 return 后面什么都不写也会报错
```

## 5. rcpress build上传后 刷新就404
```js
由于rcpress 只提供了 history API 路由的跳转方式
所以一旦刷新就会寻找每个文件夹的index.html
但是并没有 就自动跳转到404页面 由于rcpress build没有自动加404界面
所以刷新就会报错

解决办法 在 dist目录 复制index.html所有内容 复制到创新的 404.html中

我的 cicd

#!/usr/bin/env sh

set -e
rm -rf docs/.rcpress/dist
npm run build
cd docs/.rcpress/dist
cp index.html 404.html
git init
git add -A
git commit -m 'deploy'
git push -f git@github.com:eternallycyf/pluviophobe-react-document.git master:gh-pages

cd -
```


## 6. 阿里云 mysql 本地 navicat 不能连接 提示1045
```js
首先需要服务器防火墙开放3306端口 阿里云安全组放行3306
不能连接的原因是root用户初始化的host是 localhost 不能远程连接
需要手动更改 root用户的 host , 由 localhost 变为 %
我使用的是宝塔面板 所以下载了一个phpadmin 然后在 名称为 mysql的数据库的user表
将root用户的 host , 由 localhost 变为 %
随后重启 Mysql
就可以连接了
navicat 主机是公网ip root 密码是自己设置的
```
