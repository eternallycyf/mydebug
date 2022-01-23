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

## 7. vscode tsconfig path 别名不起作用
```js
// 可以看 vscode右下角提示, 在某个文件时 就会显示 tsconfig or jsconfig 是否生效
项目的根路径配置了一个 tsconfig.json 其中有配置 path别名 但只有ts文件生效
项目使用的是 jsx 语法 , 别名没有起作用
我首先配置了 一个jsconfig.json 还是没反应 到vscode github issues 上看了下
tsconfig.json jsconfig.json 如果同时存在 就只有 tsconfig.json 生效
如果需要 ts js 文件都生效需要 在tsconfig.json 中配置
{
  "compilerOptions":{
    "allowJs": true,   // 允许 js
    "outDir": "./xxx", // 我的ts报了一个错误 这里随便写 只要不是项目文件名就行
  }
}
vscode右下角已经显示 ok 了, 但是 事实还没有好, 不能跳转到 带有别名的路径
此时 我将 jsx 文件改为 tsx 文件 , 他好了 !!!
然后 再改回 jsx文件 就 success 了
```

## 8. 线上环境正则表达式无法识别 中文字符
```js
我用了一个正则截取中文 （
本机运行 ok 线上环境失败了 识别不了中文字符
解决办法 
（ 转 unicode
var reg1 = /\uff08/g
这样就可以了
```

## 9 vue 父传子 调试工具显示正常 但 console.log 输出  {__ob__: Observer}
```js
原因: 子组件渲染不会等待 axios的请求
<子组件
 v-if='xxx.length > 0'
/>
## 或者在子组件内部 监听
  watch: {
    chartData: {
      deep: true,
      immediate: true,
      handler(val) {
        this.chartData = val
      }
    }
  },
##      Object.assign({}, this.chartData)
```

## antd select placeholder 无效
```js
设置初始值为 undefined  就可以了
<Select value={ xxx ? xxx : undefined } />
```

## vue props异步 watch监听
```js
// this.drawLine 原来是 mounted中的方法
  props:['chartData'],
  watch: {
    chartData: {
      deep: true,
      handler(val) {
        if (val) {
          this.drawLine()
        }
      }
    }
  },
```

## vue在style中使用变量
- 使用原生的方法 react也差不多
```js
<template>
	<div class="test">
		<span :style="spanStyle" class="span1">hello world</span>
		<span style="--color:red" class="span1">hello world</span>
	</div>
</template>
<script>
export default {
	data() {return { spanStyle: { "--color": "green" }};}
}
</script>
<style scoped>
.span1 {
	color: var(--color);
}
</style>
```
- react 如果开始了校验需要转变下类型 否则会报错
```js
import styles from './app.module.css'
const App = () => {
  var style = { "--color": 10 } as React.CSSProperties;
  return (
    <div className={styles.header} style={style}>
      hello
    </div>
  );
};
export default App;
#
.header {
  color: var(--color)
}
```

## vscode 双击时删除键无效
```js
关闭Comment Translate插件
```