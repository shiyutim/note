# 创建wechat小程序
### 准备步骤
1. 首先创建`app.js/app.json/app.wxss`文件在**根目录**下。
2. 在项目根目录下创建`pages`**文件夹**，并且在里面创建`xxx.js/xxx.json/xxx.wxml/xxx.wxss`文件。
### 开始创建内容
1. 在`pages/xxx.wxml`文件里书写内容。想要显示这个页面需要让小程序的MIMA框架知道这个页面的**存在以及这个文件的路径**。**需要在`app.json`文件里配置这个路径**。*注：下面的文件名不需要写文件扩展名，因为MINA框架会自己寻找页面路径，然后进行整合*。
```
{
    "pages": [
        "pages/<文件夹名>/<文件名>"
    ]
}
```
2. 接下来需要在`welcome.js`文件里写入：
```
Page({
    
})
```
3. 之后再`welcome.json`文件里写入：
```
{
    
}
```
---
**经过以上配置之后，应该能显示基本的页面了。下面就是需要在基本的`.wxml`里，写入代码了**。

---
### `html`标签部分
```
<view>
    <image></image>
    <text></text>
<view>
```
1. 基本组件：
* `<view>`组件，类似于`div`标签。
* `<text>`组件用来显示一段文本，类似于`<span>`标签。
* `<image>`组件用来显示一张图片，类似于`<img>`标签。
2. 配置**全局**导航栏颜色，需要在`app.json`下配置：
```
"window": {
    navigationBarBackgroundColor: "xxx"
}
```
配置单页导航栏颜色需要在本页面的`json`下配置：
```
{
    "navigationBarBackgroundColor": "#xxxxxx"
}
```

或者
```
//定义导航条标题颜色
wx.setNavigationBarColor({
  frontColor: "#000000",
  //定义所有的页面颜色为深黄色
  backgroundColor: "#ffa801",
  //定义动画
  animation: {
    duration: 100,
    timingFunc: "easeIn"
  }
})
```
3. 配置轮播图，使用`swiper`组件，`swiper`组件只允许是`swiper-item`。 *注：在设置图片宽度和高度的时候，需要同时设置swiper 和 swiper image的高度和宽度*。
```
<view>
    <swiper>
        <swiper-item>
            <image src="xxxx"></image>
        </swiper-item>
    </swiper>
</view>
```
### 注意事项：
1. 每个文件夹里面都需要有`.js/.json/.wxml/.wxss`文件，但是并不能一键创建。可以在`app.json`文件里，添加`pages`路径。之后系统会自动创建。
2. 里面图片资源并不能复制粘贴，所以需要自己在项目文件里面粘贴，系统会自动刷新。
3. 图片显示的高度不是图片本身的高度，它被MINA框架设置成了**宽度为`320px`，高度为`240px`**。
4. 真实项目里，图片资源尽量不要储存在小程序目录里，因为小程序有大小限制，超过则**无法发布**。应该将图片**存放在服务器上**，让小程序通过**网络来加载图片**。
5. `rpx`是自适应长度单位。
    * 在需要保持**一定比例**的情况下需要使用。
    * 在保持固定长度的情况下使用`px`。
6. `app.wxss`定义**全局样式**。想要在每个文件里使用样式，可以在这个文件里定义属性样式。
7. 小程序启动后的**首页**由`app.json`文件里的`pages`数组的**第一个元素**决定。
8. 要使轮播图生效，还需要在`<swiper>`组件里添加如下属性：
```
<swiper indicator-dots="true" autoplay="true" interval="3000">
    <swiper-item></swiper-item>
</swiper>
```
9. `wx.redirectTo`会使页面被卸载，`wx.navigateTo`会使页面被隐藏，并且导航栏有返回按钮。
**也就是说，从父页面进入子页面，可以执行`Unload`和`Hide`事件，但是子页面返回父页面，被动执行`Unload`事件**。因为不执行unload事件会使得大量页面残留在小程序中。
10. 当使用`wx.navigateTo`跳转的时候，就形成了两个页面层级，小程序里强制规定，**只允许有5层页面**，**太多的子页面严重影响用户体验**，建议页面不超过**3层**。
11. **不能再`<template>`上注册事件**，因为`<tempalte>`仅仅是一个**占位符**，再**编译**后会被**模板内容**替换。所以，在`<template>`上**注册事件是无效的**。
    * 可以在`<tempalte>`标签外部使用`<view>`标签包裹起来。然后把事件添加到`<view>`标签里。
    ```
    <view catchtap="xxxxx">
        <template></template>
    </view>
    ```
12. 在以前的版本里，使用`wx.setNavigationBarTitle`设置导航条动态获取文章标题，需要在`onReady`里面设置，因为`onReady`在`onShow`发生之后触发，`onShow`设置完后，`onReady`会从新渲染页面，所以会发生这种情况。**而在新版本中，可以在`onLoad`或者`onShow`中调用这个方法。**
    ```
    onReady: function(){
        wx.setNavigationBarTitle({
            title: this.postData.title //这里可以是任何代码
        })
    }
    ```


---
### 页面生命周期
周期|代码|内容
|-|:-:|:-:|
加载|onLoad|监听页面加载，一个页面只会调用一次
显示|onShow|监听页面显示，每次打开页面都会调用
渲染|onReady|监听页面初次渲染完成，一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
隐藏|onHide|监听页面隐藏
卸载|onUnload| 监听页面卸载


### 小程序生命周期

周期|代码|内容
|:-:|:-:|:-:|
初始化|onLaunch|**监听小程序初始化**，当小程序初始化完成时，会触发onLaunch（全局只触发一次）。
显示|onShow|**监听小程序显示**，当小程序启动，或从后台进去前台显示，会触发onShow。
隐藏|onHide|**监听小程序隐藏**，当小程序从前台进入后台，会触发onHide。
错误|onError|**错误监听函数**，当小程序发生脚本错误，或者API调用失败时，会触发onError并带上错误信息。
---
### 事件
1. 跳转事件

事件| 代码|实例
|:-:|:-:|:-:|
跳转|catchtap|catchtap="onCatJump"
```
onCatJump: function() {
    wx.redirectTo({
       url: "../",
)}
```
2. 冒泡事件和非冒泡事件

代码|描述
|:-:|:-:|
touchstart|手指触摸动作开始
touchmove|手指触摸后移动
touchcancel|手指触摸动作被打断，如来电提醒，弹窗。
touchend|手指触摸动作结束
tap| 手指触摸后马上离开
longtap|手指触摸后，超过350ms再离开
冒泡事件是指某个组件上的事件被触发后，事件还会继续向父级元素传递。非冒泡事件则不会向父级元素传递。
```
bind不会阻止事件的传播，catch讲阻止事件继续向父节点传播
```

### 在url中添加Id
```
url: "post-detail/post-detail?id=" + postId
```
### 条件渲染: `wx:if/wx:else`
* 当变量为`true`时，执行`wx:if`，否则将执行`wx:else`。
    ```
    <image wx:if="{{post.status}}" src="../"></image>
    <image wx:else src="../"></image>
    ```

### 交互`wx.showToast`
* API ->界面->交互
    ```
    wx.showToast
    ```
### 控制元素显示和隐藏`wx:if/hidden`
```
                if
<image wx:if="{{post.status}}" src="../"></image>
                hidden
hidden="{{see}}"
hidden="{{!see}}"
```
* `wx:if`
    * `wx:if`的切换和渲染机制较为复杂。在条件快切换时销毁或重新渲染。
* `hidden`
    * 组件始终会渲染，只是简单的控制显示与隐藏。

`wx:if`有更高的切换消耗，而`hidden`有更高的初始渲染消耗。因此，**在需要频繁切换的情景下用`hidden`更好，在运行条件不大可能改变时用`wx:if`更好。**