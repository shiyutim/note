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