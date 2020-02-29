# 响应式web设计 HTML5和CSS3实战
## 第一章 响应式web设计基础
1. IOS默认会按**980像素宽度**来渲染网页，然后再把**页面缩小**呈现在视口当中。
2. 浏览器中用于呈现网页的区域叫视口(viewport)。视口通常并不等于屏幕大小。
3. 在网页的`<head>`中添加下面的代码
```
<meta name="viewport" content="width=device-width">
```
意思是：按照设备的宽度（device-width）来渲染网页内容
4. **自适应图片**
```
img {
    max-width: 100%;
}
```
为什么不用`width:100%`？因为如果屏幕比图片本身的宽度 宽，会使图片被拉伸，所以需要设置最大宽度！
5. 媒体查询可以使用不同的长度单位指定，入百分比、em、rem和px。
```
@media screen and (min-width 50em) {
    
}
```

* `@media`指定告诉浏览器这是一个媒体查询
* `screen`告诉浏览器这里的规则只适应于屏幕类型（这个可以不用声明）
* `and(···)` 其中的规则只使用于视口宽度在50em以上的情况。
6. 我们在媒体查询外面写的第一条规则，实际上是针对所有媒体的“基本” 样式。在此基础上，可以再针对不用能力的设备加以扩展。
7. “不针对特定的设备设置断点，而应该根据内容”。断点就是某个宽度的临界点，跨过这个临界点布局就会发生变化。

## 第二章 媒体查询
1. 设置断点的时候，使用em属性可以换算为：除以16为em的长度。如：800px像素，800/16 = 50em
2. 使用@import导入样式表。**使用css中的import会增加HTTP请求，进而影响加载速度。**
```
@import url(xxx.css) screen and (max-width: 360px);
```
3. “在针对所有设备的媒体查询中，可以使用简写语法，即省略关键字all（以及紧随其后的and）。换句话说，如果不指定关键字，则关键字就是all”
4. 使用媒体查询链接不同的CSS文件。浏览器会先解析符合规则的样式表，其他样式文件可以等到页面初始渲染结束后再处理。（所有文件都会下载下来，只是如果有的文件不必立即应用）
5. 在大多数情况下可以使用这个标签
```
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

## 第三章 弹性布局与响应式图片
1. 在开始时，网站的宽度大都以百分比形式定义。百分比布局使得网页宽度能够随着查看它们的屏幕窗口大小变化，因而得名**弹性布局**
2. 在大约2005-2010年，出现了固定宽度的设计。
3. 为了使得媒体查询断点间的平滑过渡，需要使用弹性布局。
4. 在2015年css推出了一个新的布局模块叫“弹性盒子”flexbox。可以用来实现弹性布局。
5. 在设置了flex的属性里，给最后一个元素设置`margin-left: auto`可以使这个元素定位在最右侧。
6. 通过scrset切换分辨率
```
<img src="xxx.png" srcset="xxx.png 1.5x, xxx.png 2x">
```
7. srcset和sizes联合切换
```
<img srcset="xxx.png 450w, xxx.png 900w" sizes="(min-width: 20em) 100vw, (min-width: 50em) 50vw" src="xxx.png">
// 450/900分别代表像素
```

## 第四章 HTML5与响应式Web设计
1. `lang`用于声明语言的类型，告知浏览器用什么来声明。常见的有
* lang="en"
* lang="zh"
* lang="zh-CN"
2. 对于本地文件video而言，设定固定的高宽不能使他自适应，可以这样设置`max-width: 100%; height: auto;`。对于嵌入视频（其他来源），这样并不能解决问题

## 第五章 CSS3新特性
1.  `word-wrap: break-word`可以设置折行，比如url
2. 设置截短文本，如`All you need to is ...`,需要如下设置
```
 {
    width: 100%; // and width: xxxpx; 
    overflow: hidden;                 
    text-overflow: ellipsis;      
    white-space: no-wrap   // 确保长出来的文本不会折行显示在外部元素中
 }
 ```
 3. 选择器伪类：
 * first-child
 * last-child
 * only-child
 * only-of-type
 4. 使用@font-face设置自定义字体
 5. hsl和hsla颜色
 
## 第六章 CSS3高级技术
1. text-shadow文本阴影，四个值，分别为
    * 阴影右侧的偏移量
    * 阴影下方的偏移量
    * 模糊距离
    * 颜色值
2. background-size 背景图片大小。第一个值为宽度，第二个值为高度。
    * auto 让图片保持其原生大小
    * cover 保持图片比例，拓展至覆盖整个元素
    * contain 保持图片比例，拓展图片让其最长边保持在元素内部

## 第七章 SVG与响应式设计
1. SVG是用于描述二维图形的语言。支持三种图像对象：矢量图形形状/图像和文本。
2. SVG允许在代码中使用矢量点来描述二维图像。因为矢量图是使用相对点来保存数据的，所以可以缩放到任意大小而不会损失清晰度。相对于同尺寸的jpg等文件来说体积更小。

## 第八章 CSS3过度丶变形和动画
1. transition 过度 transform 变形 animation 动画
2. transition-property 指定要过度css属性的名字，可以指定具体的名字，也可以指定all（all会过度所有可以过度的属性）
 
## 第九章 表单
1. 使用:placeholder-shown 可以给placeholder添加样式，不过需要添加前缀
2. autocomplete浏览器自动补全功能。使用off来禁用。
3. 表单的pattern属性支持验证 正则表达式


## 第十章 实现响应式web设计
1. 让设计决定断点
2. 在真实设备上观察和使用设计
3. 渐进增强。选择支持的浏览器中共同拥有的方法来编写前端代码，然后逐渐增强。