# Vue项目笔记
1. 默认`webpack`是不能识别`css`的，所以需要配置`loader`，`scss/less/stylus`同样也需要下载对应的`loader`文件。
    * `npm install stylus stylus-loader --save-dev`
    * 下载之后再`.vue`文件里，如果要写`stylus`样式，需要在`<style>`标签里面添加`lang="stylue" rel="stylesheet/stylus`。
2. 使用`redirect`可以设置**默认**的**路径**。
```
       {
            path: '/',
            redirect: '/xxx'
        }
```
3. **动态的添加类名**，下面的代码表示，在路径为`search`的时候，把类`active`动态的添加到指定的地方。
```
    :class = "{active: $route.path ==  '/search'}"
```
4. 动态的切换**路由路径**，可以给要点击的元素添加`@click`方法。
```
    @click="goTo('/path')"
    methods: {
        goTo(path) {
          this.$router.replace(path);
      }
    }
```
5. 使用`swiper`来进行轮播图。在要使用轮播图的`Vue`文件里，如下导入文件。
```
import Swiper from 'swiper'
import 'swiper/dist/css/swiper.min.css'
```
6. 导入组件
```
在<template>里添加如下组件:
<OwnOne></OwnOne>

在script标签里面如下：
import OwnOne from '../../xxxx'
export default {
    components: {
        OwnOne,
    }
}
```
7. 导入`vue-router`
    * `<router-link to="/xxx"></router-link>`
8. 返回前一页，可以使用
```
@click="$router.back()"
```
9. 使用`v-show="$route.meta.xxxxx"`可以控制这个组件是否在本页面显示。配置如下：
    * 在控制该组件的**占位符**里面添加`v-show="$route.meta.showFooter"`。
    * 然后在引入路由路径`routes`里面添加如下代码：
    ```
    meta: {
        xxxxx: true
    }
    ```
    * `true`为显示，默认为`false`。
10. 点击刷新页面
* 方法一
```
this.$router.go(0)
```
* 方法二
```
window.location.reload()
```
* 方法三
```
history.go(0)
```
# 学习笔记
#### 使用定时器`setInterval()`
首先在`methods`中定义好函数后，在`mounted`里面调用。
**调用方法的时候，不要加括号**;**定时器在页面关闭时一定要销毁掉，不然会一直存在**
```
methods: {
    add () {
        xxxx
    }
},
mounted () {
    this.add();
    var timer = setInterval(this.add, 1000);
}
beforeDestroy() {
    clearTnterval(this.timer)
}
```

#### 使用方法后不能更新视图
可以使用`Vue.set()`方法。
```
Vue.set(this.xxx, 0, {
    name: 'xxx',
    xxxx: xxxx
})
```
#### 跨域问题
通过在index.js文件里面通过设置model.export = {}设置代理。




# Vue-cli(脚手架)
## 使用`vue-cli`构建项目
1. **首先安装全局安装`webpack`,**
```
cnpm install webpack@3.10.0 -g
```
然后使用`webpack -v`查看安装是否成功

**全局安装vue-cli**
```
cnpm install --global vue-cli
```
安装完成后，使用`vue -V`查看版本号
2. 用vue-cli构建项目,输入如下指令
```
vue init webpack <项目名称>
```
按`enter`/`y `来确认信息
3. 如果需要使用`cnpm install`安装依赖包
4. 使用`npm run dev`运行项目
5. 在项目开发完成后，可以输入`npm run build`来进行打包工作

