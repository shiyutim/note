1. `letter-spacing`设置字母间距 `word-spacing` 设置字间距
2. 
* visible: 不剪裁溢出的内容。浏览器将把溢出的内容呈现在其容器元素的显示区域以外的地方，全部内容在浏览器窗口里都是可见的。
* hidden： 剪裁溢出的内容。 内容只显示在其容器元素的显示区域里，这意味着只有一部分内容在浏览器窗口里是可见的。
* scroll： 类似于hidden，浏览器将对溢出的内容进行剪裁，但会显示滚动条以便让用户能够看到内容的其他部分。
* auto： 类似于scroll，但浏览器只在真的发生内容溢出时才显示滚动条。如果内容没有溢出，就不显示滚动条。
3. `font-style: italic`定义字体斜体
4. `<td rowspan="2">`表格中单元格占2行。colspan
5. `multiple`select里面多选属性
6. `required`提示必须输入
7. `:first-letter`设置首字母样式
8. `:first-line`第一行样式
9. 
* 绝对路径（url）指从网址开始（http:www.）
* 相对路径指相对于这个html文件所对应的路径
10. `white-space： pre`会保留文本中的空格
11. `font-size: 0px` 可以消除设置display: inlie-block 的块级元素间距
12. `calc()`可以计算元素的宽高
13. 有下载需求的图片采用img标签实现，无下载需求的图片采用css背景实现
* 产品logo、用户头像、用户产生的图片等有潜在下载需求的图片，以img形式实现，能方便用户下载。
* 无下载需求的图片，比如icon、背景、代码使用的图片等，尽可能采用css背景图实现。
14. [建议]同一 rule set下的属性在书写时，应按功能进行分组，并以 Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。
Formatting Model 相关属性包括:
    * position/top/right/bottom/left/float/display/overflow
    * Box Model 相关属性包括:border/margin/padding/width/height
    * Typographic 相关属性包括:font/line-height/text-align/owrd-wrap
    * Visual 相关属性包括: background/color/transition/list-style
15. `cursor: pointer`鼠标放上小手效果
16. `checked`表单默认选中
17. `autofocus`设置默认焦点
18. `maxlength`接受最大字符数
19. a标签
    * `a:link`未点击之前
    * `a:visited`点击之后
    * `a:hover`鼠标悬停
    * `a:active`点击时状态
20. 
* `text-decoration: underline`下划线 
* `overline`顶部线
* `line-through`文本中间
21. `text-indent`定义首行缩进
22. `text-transform：`
* `uppercase`大写
* `lowercase`小写
* `capitalize`单词首字母大写
23. flex属性
* `flex-direction`。决定项目的方向
    * `row`横向
    * `column`垂直方向
    * `row-reverse`横向相反
    * `column-reverse`垂直相反
* `flex-wrap`。决定项目一条轴线排不下，如何换行
    *  `nowrap`不换行，都挤在第一行
    *  `wrap`换行，第一行在上方，然后依次往下排列
    *  `wrap-reverse`换行，只不过第一行在最下方。
* `flex-flow`为上述两种的简写属性。
* `justify-content`定义项目在主轴上的对齐方式。
    * `flex-start`全部靠左
    * `flex-end`全部靠右
    * `center`居中
    * `space-between`两端靠边
    * `space-around`分布排列
* `align-items`定义项目在垂直方向的位置
    * `flex-start`全部在上方
    * `flex-end`全部在下方
    * `flex-center`居中
    * `stretch`如果项目未设置高度，则自动占满整个容器的高度
    * `baseline`项目的第一行文字的基线对齐
* `align-content`
    * `flex-start`：与交叉轴的起点对齐。
    * `flex-end`：与交叉轴的终点对齐。
    * `center`：与交叉轴的中点对齐。
    * `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
    * `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    * `stretch`（默认值）：轴线占满整个交叉轴。
* 设置项目上的属性 
    * `order`可以改变属性的排列顺序，数值越小，排列越靠前。
    * `flex-grow`定义项目的放大比例，如果所有的项目都为1，则平分剩余空间
    * `flex-shrink`定义项目的缩小比例
    * `flex-basis`定义在分配多余空间之前，项目占据主轴空间。
    * `flex`是flex-grow/flex-shrink/flex-basis的简写
    * `align-self `