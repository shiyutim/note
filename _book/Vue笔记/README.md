# Vue项目笔记
## 使用`redirect`可以重定向到别的页面。
```
       {
            path: '/',
            redirect: '/xxx'
        }
```
## 动态添加类名
下面的代码表示，在路径为`search`的时候，把类`active`动态的添加到指定的地方。
```
:class = "{active: $route.path ==  '/search'}"
```
## 动态的切换路由路径
可以给要点击的元素添加`@click`方法。
```
@click="goTo('/path')"
methods: {
    goTo(path) {
      this.$router.replace(path);
  }
}
```
## 使用`swiper`来进行轮播图。在要使用轮播图的`Vue`文件里，如下导入文件。
```
import Swiper from 'swiper'
import 'swiper/dist/css/swiper.min.css'
```
## 点击按钮跳转
* 第一种方法
`<router-link to="/xxx"></router-link>`
* 第二种方法
```
<button @click="jump">跳转</button>

jump () {
    this.$router.push({path: '/xxx'});
}
jump () {
    this.$router.push({path: "name?a=123"})或者
    this.$router.push({path: "name", query:{a:123}})
}
```
* 第三种方法
```
$router.go(1)
```
## 返回前一页
```
@click="$router.back()"
```
## 使用`v-show="$route.meta.xxxxx"`可以控制这个组件是否在本页面显示。
配置如下：
* 在控制该组件的**占位符**里面添加`v-show="$route.meta.showFooter"`。
* 然后在引入路由路径`routes`里面添加如下代码：
```
meta: {
    xxxxx: true
}
```
* `true`为显示，默认为`false`。

## 点击刷新页面
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
    
## addClass方法
```
<a
    v-for="(item, num) in navList" :key="num" href="" @click.prevent="addClass(num)"
    :class="{lineActive:num === current}"
>{{item.name}}</a>

addClass (index) {
  this.current = index
}
```
## vue动画
* 首先需要给要使用动画的元素嵌套一个<transition>标签
* 然后配置name属性,可以使用`fade`
```
.fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
    opacity: 0;
}
```
## VUE中获取固定格式日期

* 首先在main.js中定义函数
```
function formatDate(date, fmt) {
  date = new Date(date);
  if (typeof(fmt) === "undefined") {
      fmt = "yyyy-MM-dd HH:mm:ss";
  }
  if (/(y+)/.test(fmt)) {
      fmt = fmt.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length))
  }
  let o = {
      'Y': date.getFullYear(),
      'M+': date.getMonth() + 1,
      'd+': date.getDate(),
      'H+': date.getHours(),
      'm+': date.getMinutes(),
      's+': date.getSeconds()
  }
  for (let k in o) {
      if (new RegExp(`(${k})`).test(fmt)) {
          let str = o[k] + ''
          fmt = fmt.replace(RegExp.$1, RegExp.$1.length === 1 ? str : ('00' + str).substr(str.length));
      }
  }
  return fmt
};



Vue.filter("FormatDate", function(date, fmt) {
  return formatDate(date, fmt);
});
```

这样是注册在全局里面的，所有的组件都可以使用，如：

* 在某组件里，这样定义：
```
 <span>{{ time | FormatDate('Y-MM-d HH: mm: ss') }}</span>
 // 2019-09-25 22: 41: 52
```
## 使用拦截守卫，进行登录拦截
requireAuth 属性作用是表明该路由是否需要登录验证
```
{
    path: '/forum',
      component: Forum,
      meta: {
        requireAuth: true    // 这里定义是否需要拦截
      },
      beforeEnter: (to, from, next) => {
        if (to.meta.requireAuth) {  // 判断跳转的路由是否需要登录
          const cookie = document.cookie
          if (cookie) {
            next()
          } else {
            window.alert('请登录')
            next(false)
          }
        } else {
          next()
        }
      }
 }
```

## 获取元素高度
```
//获取高度值
var height= this.$refs.text.offsetHeight; //100


//获取元素样式值,element 为元素ref="element"
var heightCss = window.getComputedStyle(this.$refs.element).height; // 100px


//获取元素内联样式值
var heightStyle =this.$refs.element.style.height; // 100px
```
##### 添加
在`methods`定义一个方法，可以通过点击事件触发
```
methods: {
        saveStorage () {
           localStorage.setItem('test', '123') //  第一个值为key，第二个值为value，value可以是变量
        }
    }
```
触发后，打开控制台的**Application**选项卡，点击**Storage**下的**Local Storage**可以看到右侧已经添加进入了相应的值。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190930212345332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDYyMzA0MA==,size_16,color_FFFFFF,t_70)

##### 获取
在写一个方法用来获取
```
methods: {
       getStorage () {
           const info = localStorage.getItem('test')
           console.log(info)
       }
   }
```
调用此方法后，可以看到控制台输出了存储后的值

##### 删除
```
methods: {
       removeStorage () {
           localStorage.removeItem('test')
       }
   }
```
调用此方法后，发现选项卡里面储存的key为`test`的值已经没了

---
**在储存变量的时候，记得要使用JSON.stringify()方法，在获取的时候要使用JSON.parse()方法**


---

1. `<style>`标签里面添加`scoped`属性，可以设置这个标签只对当前组件生效。如果不设置就会影响引入了这个组件的父组件。
2. `.prevent`用来阻止默认事件。
3. `$route.query.xxx`获取url参数
4. `$route.params.xxx` 路由参数
5. . 默认`webpack`是不能识别`css`的，所以需要配置`loader`，`scss/less/stylus`同样也需要下载对应的`loader`文件。
    * `npm install stylus stylus-loader`
    * 下载之后再`.vue`文件里，如果要写`stylus`样式，需要在`<style>`标签里面添加`lang="stylus"
6. 获取DOM元素的**位置信息**
```
<p ref="selectLi"></p>

this.$refs.selectLi.getBoundingClientRect().top
```
7. router/index.js路由配置文件
路由配置文件里面的`@`代表 `webpack.base.conf.js`里面resolve 里面配置的文件名。**这样使用@就代表了src**
```
 alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
    }
```

8. “dependencies”/ "devDependencise"
* dependencies 里面是项目上线后需要的依赖
* devDependencise 里面是生产环境后需要的依赖


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

