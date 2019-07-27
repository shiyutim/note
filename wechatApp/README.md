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

### 背景音乐播放的特点
* 音乐播放不受页面关闭的影响，即使一个页面被`unload`掉，音乐依然会继续播放。所以在官方的API中音乐被称为背景音乐。
* 同时只能有一个后台音乐在播放，如果播放另外一首音乐，那么当前音乐将停止。
* 如果用户不主动关闭音乐，那么只有在退出小程序后音乐播放才会停止。关闭当前页面是不会影响小程序音乐播放的。
* 一首音乐拥有3个主要属性：`dataUrl(音乐的播放地址)`/`title(音乐标题)`/`coverImgUrl(音乐封面图Url)`
* 歌曲只能是网络流媒体，不能是本地音乐文件




#### `checkbox`等更改为默认选中
`checkbox`更改为默认选中状态等，需要在里面添加`checked`,如果需要取消的话，需要添加花括号的形式
```
<checkbox checked="{{ false }}"></checkbox>
```


#### 750px宽度比
设定默认为750px,那么，`1rpx = 1px`，然后进行换算比较方便，如：
```
750px  宽高为 100px
375px  宽高为 50px
```


#### 在请求验证码之后，设置按钮禁用
```
<button disabled="{{isDisabled}}" bindtap="xxx">
```
如上按钮，通过动态的设置`isDisabled`的值来更改按钮的状态。逻辑是**点击请求事件后，按钮进入倒计时，同时把`isDisabled`的值设置为`true`，等到秒数结束后，设置值为`false`。**

完整的代码为：
```
if(/^1[3456789]\d{9}/.test(userPhone)) {
    //如果为true，说明手机号正确，则获取验证码接口
    
    //请求接口
    wx.request({
        url: 'https://www.baidu.com',
        data: {
          phonenum: xsjm.jiami(userPhone)
        },
        header: {
          'content-type': 'application/x-www-form-urlencoded'
        },
        method: 'POST',
        success(res) {
          console.log(res.data)
          codeP = xsjm.jiemi(res.data)
        }
      })
      
}else if(userPhone == '') {
    //说明手机号为空，还没有输入，则使用`wx.showToast`来进行提示输入手机号
}else {
    //说明手机号错误，提示输入正确的手机号
}
```

#### 使用组件
创建：右键点击`component`，然后出现四个文件。

使用：在需要使用的文件夹里面，找到`json`文件，在`usingComponents{}`里面，填写需要使用的组件路径。如：
```
"usingComponents": {
    "myComponents": "xxx"  
    //MyComponents 为组件的文件名
    //xxx为页面路径
}
```
然后再文件中这样引入就可以了
```
<myComponents></myComponents>
```


#### 微信小程序点击导航高亮显示
点击导航，并高亮显示。思路就是点击导航触发事件，然后动态的添加类名

`wxml`为：
```
<view 
bindtap="activeNav"   //绑定点击事件
wx:for="{{navList}}"  //遍历这个数组里面的数据
data-index="{{index}}"  //取出navList里面的下角标
class="{{index === currentIndexNav ? 'active' : ''}}"    //currentIndexNav定义在data里面，默认为0，然后动态绑定一个类>
	{{item}}
</view>
```

`js`为：
```
data: {
	currentIndexNav: 0
},

activeNav(e) {
	this.setData({
		currentIndexNav: e.target.dataset.index
	})
}
```
`wxss`为：
```
.active {
	border-bottom: 5rpx solid #de688b;    //点击的时候在导航底部添加一个横线
}
```


#### 修改顶部导航栏颜色无效问题
接手的项目，想要修改一下导航栏颜色，发现修改后并没有生效。研究了半天，发现上一个人使用了自定义导航栏，这样定义的属性，默认为`default`
```
"navigationStyle": "custom"
```
使用这个属性后，想要修改导航栏的颜色，就需要在**每个页面单独设置**，然后找到单独页面的`wxss`文件后，修改里面的样式属性，就可以更改了。

> 网上看到有人抽离成一个组件，然后设置一个样式。但会很麻烦，还有一系列问题


#### 阻止点击事件
可以使用三元表达式
```
<view bindtap="{{isClicked ? 'clicked' : ''}}"></view>


data {
    isClicked: true
}

clicked() {
    //
}
```


#### 设置圆形头像
直接设置`border-radius: 50%;`是不起作用的，需要设置`overflow:hidden`
```
{
    border-radius: 50%;
    overflow: hidden;
}
```


#### 获取地理位置信息
使用小程序提供的`wx.getLocation`之后，使用说需要**在app.json**里面提供`permission`说明。
```
 "permission": {
    "scope.userLocation": {
      "desc": "你的位置信息将用于小程序的效果展示"
    }
  }
```


#### 获取数据
一般获取接口的数据后，需要赋值，然后在页面里渲染出来。遇到一个问题，就是赋值之后，`data`里面的数据很乱。几个`data`分不清，然后我突然发现一个问题。就是：
```
success(res) {
    list: res
}

//假如说页面是如下格式渲染
<view wx:for="{{list}}">
    {{item.data.data.name}}
</view>
```
如果在js中变成如下配置
```
success(res) {
    list: res.data
}
```
那么，在页面上也是需要改变的
```
<view wx:for="{{list}}">
    {{item.data.  name}}
</view>
```


#### 异步操作的登陆接口`wx.login`
登陆接口是异步的，所以说，如果下面有别的操作需要在登陆接口之后调用，需要在`wx.login`内部进行操作，如果在外面调用，有可能发能：还没有登陆，就已经发生后面的函数调用，可以在控制台里面输入`console.log`来进行查看。

如果没在登陆之后调用，就会造成一种现象，就是有时候能请求到具体信息，有时候请求不到。



#### 动态切换toggle效果
就是使用三元表达式，然后点击切换false/true
```
data: {
    onShow: true
}

showOrHide() {
    let that = this
    if(this.data.onShow === true) {
       that.setData({
         onShow: false
       })
    }else {
       that.setData({
         onShow: true
       })
    }
}
```
主要是获取data里面的onShow，需要`this.data.onShow`才能获取到。但是以上方法比较繁琐，有更简洁的方法：
```
showOrHide() {
    let that = this
    var toggle = !this.data.onShow
    that.setData({
      onShow: toggle
    })
}
```
这个方法就是点击一下`取反`，比较简洁。


#### 根据金额的位数动态渲染*的位数
为了完美，不想固定的放置一堆“****”，想要根据金额的位数来渲染*的位数
```
showOrHide() {
    let that = this
    var toggle = !this.data.onShow
    var moneyLength = that.data.userCardCharge.length 
    var noShowLength = []
    for(var i=0;i<moneyLength;i++) {
      noShowLength+="*"
    }
    console.log(noShowLength);
    that.setData({
      onShow: toggle,
      noShow: noShowLength
    })
  }
```


#### 有时候修改完数据后，没有刷新页面，需要重新`onLoad()`
修改信息数据后,就要去执行下onLoad函数重新渲染。
```
that.setData({
    xxx: xxx
})
that.onLoad()
```

#### 在前一页修改数据后，返回后一页也需要刷新页面
```
  onShow: function() {
    let that = this
    that.onLoad();
  },
```

#### 任何想要绑定Boolean值的情况下，需要使用数据双向绑定
举个例子，一个值，`autoplay`，这个是轮播图里面的，代表是否自动播放，我们想让他为true，那么只要这么写就可以:
```
autoplay="true"
```
但是如果想要换成false呢，
```
autoplay="false"
```
发现根本没用，因为只要不是空字符串，就会识别为true。所以如果想要为“真false”的话，需要这样写:
```
autoplay="{{false}}"
```


#### 获取openid
* 首先通过官方提供的`wx.login`API，然后获取一个`code`
* 然后发起`wx.request`请求，把`code`(也就是res.code)发送给开发者服务器(后端)
* 后端会发送给微信服务器，然后返回openid等信息
* 然后通过`success(res) {openid:res.openid}`来获取openid

