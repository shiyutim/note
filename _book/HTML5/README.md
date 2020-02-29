# HTML5笔记
1. `<video src="" controls="controls" autoplay="autoplay">xxxx</video>`
* 当浏览器不支持时，xxx显示在视频的位置上
* `controls`定义视频的控件
* `autoplay`定义网页加载即播放视频
* `loop`定义循环播放
2. 设置图片可拖放: `draggable="true"`
* 要使用`canvas`元素，必须设置其`width`和`height`属性，指定可以绘图的区域大小。
3. `getContent('2d')`，内建HTML5对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。
4. `fillRect()`定义填充图形，`strokeRext()`定义描边图形。
5. `fillStyle、strokeStyle`定义颜色，`fillRect、strokeRext`定义形状、位置和尺寸。
6. `lineWidth`定义描边的宽度。
7. `xxx.moveTo(xx, xx); xxx.lineTo(xx, xx);`,
`stroke()`方法会实际的绘制出通过moveTo()和lineTo()方法定义的路径。默认颜色为黑色。
8.`clearRect()`方法用于清除画布上的区域。
9. `beginPath()`表示要开始绘制新路径；`xxx.stroke()`定义结束。
10. 绘制文本`fillText()、strokeText()`。
11. SVG是指可伸缩矢量图形，使用XML格式定义图形，图像放大或改变尺寸图形质量不会损失。
12. 
Canvas：
* 依赖分辨率
* 不支持事件处理器
* 弱的文本渲染能力
* 能以.jpg或.png格式保存图像
* 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

SVG：
* 不依赖分辨率
* 支持事件处理器
* 最适合带有大型渲染区域的应用程序（比如谷歌地）
* 复杂度高会减慢渲染速度（适合过度使用DOM的应用都不快）
* 不适合游戏应用
13. HTML5 Geolocation（地理定位）用于定位客户的位置。
14. HTML5 提供了两种在客户端储存数据的新方法：
* localStorage 没有时间限制的数据储存
* sessionStorage 针对一个session的数据储存
15. HTML5引入了应用程序缓存，如需开启缓存，可以在文档的`<html>`中包含： `manifest`属性。`manifest`文件的建议文件扩展名是`.appcache`。
16. 一旦应用被缓存，他会就保持缓存直到发生下列情况：
* 用户清空浏览器缓存
* manifest文件被修改
* 由程序来更新应用缓存
17. web worker 是运行在后台的Javascript，不会影响页面的性能。
18. HTML5 服务器发送事件`server-sent event`允许网页获得来自服务器的更新。
19. `input`输入类型：`eamil;url;number;range;date;search;color`。