# CSS世界
## 第一章 概述
1. `CSS`全称是Cascading Style Sheet,中文为“层叠样式表”。

2. 1996年12月17日**CSS1**诞生，1998年5月12日**CSS2**发布。

## 第二章 了解术语和概念
1. 下面两个选择器中，后代选择器表示**选择所有后代**，而相邻后代选择器仅表示**选择儿子元素**。
* 后代选择器：用空格表示。
* 相邻后代选择器： > 。
2. 兄弟选择器：选择当前元素后面的**所有**合乎规则的兄弟元素，用`~`连接。
3. 相邻兄弟选择器：仅仅选择当前元素**相邻**的那个合乎规则的**兄弟元素**，用`+`连接。
4. 某个浏览器和其他浏览器的行为不一样，有些情况下不是bug，有可能是“未定义行为”。

## 第三章 流、元素与基本尺寸

1. 通过给父元素添加`::after`伪元素来进行清除浮动。
2. 每个元素都有两个盒子，分别为**外在盒子**和**内在盒子**，外在盒子负责元素是可以一行显示，还是只能换行显示；内在盒子则是负责宽度、内容等。

display|外在|内在 
|-|:-:|-:
block|块级盒子|块级容器盒子
inline-block|内联盒子|块级容器盒子
inline|内联盒子|内联盒子
3. `div、p`这些元素的宽度默认是100%于父容器的。
4. 设置`display:block`的元素，除非必要情况，尽量不需要设置`width=100%`了。这是利用块级元素的流特性。
5. 设置`display:inline-block`的元素具有包裹性，也就是说里面元素的内容会被父元素包裹起来，一行放不下会自动换行。
6. 在使用固定宽度的情况下，增加`border`和`padding`会增加元素的宽度，这样不便于计算`content`的宽度。
   * 可以使用设置父元素宽度，子元素设置`padding`和`border`，这样就可以让内容自动计算宽度。
   * 设置`box-sizing: border-box`可以使得增加`padding`和`border`不会改变内容的宽度。
7. `textarea`里，想要让内容100%溶于父元素，只有设置`width`。`textarea`是有`border`，所以想要体验好需要设置`padding`。这时候可以通过设置`box-sizing:border-box`来改变该内容。
8. 相对于设置`*{box-sizing:border-box}`来说，设置`input,textarea,img,video,object {box-sizing:border-box}`更合理。          
9. 如果想要设置一个全屏的`div`,需要设置`html,body{height: 100%}`,然后设置`div{height:100%;}`。
也就是说想要**百分比高度值**起作用，其父级必须有一个可以生效的高度值。
10. 如何让`height:100%`生效？
    * 父元素设置固定宽度，或者设置`html,body {height:100%};`
    * 使用绝对定位，如：
    ```
    div {position: absolute; width:100%; height:100%;}
    ```
11. `min-width`和`max-width`一般出现在自适应布局和流体布局中。在使用**固定值**的`height/width`中，这两个属性毫无作用。
    * 特定区间的自适应布局方案可以设置为：
    ```
    .container{min-width: 1200px; max-width: 1400px;}
    ```
    * 对于有些**图片**在移动端上，可以设置`img {max-width: 100%; height: auto!important;}`。高度自适应是必须的，因为`max-width`生效的时候，图片就会被压缩，`auto`会使图片保持一定的比例显示出来。但是这样会有体验的问题，就是在加载图片占据高度会从0变成计算高度，图文会有明显的瀑布式下落。
12. 当`max-width和min-width`跟`width`冲突时，前者会覆盖后者，而且`width`加上`!important`也没有用。
13. 当`min-width`和`max-width`冲突时，前者会覆盖后者。
14. 对于设置了`position:absolute`的元素，可以使用`clip:rect()`对其进行剪裁。
15. `display:table-cell`可以设置任意个等宽的元素。
16. 使用`input,lable`可以实现展开和收起动画效果。"展开收起"效果是网页中比较常见的一种交互形式，通常的做法是控制`display`在`none`和其他值之间切换。但是这种方式比较生硬。传统的方式可以使用`jQuery`的`slideUp()`和`slideDown()`方法。使用CSS3的动画可以这样设置：
    ```
    .element {
        max-height: 0;
        overflow: hidden;
        transition: max-height .25s;
    }
    .element .active {
        max-height: 666px;
    }
    ```
## 第四章 盒尺寸四大家族

1. `<img>`元素的默认声明是`object-fit: fill`,如果设置了`object-fit: contain`，则图片会以保持比例图片，尽可能利用HTML尺寸但又不会超出的方式显示。如果设置`<img>`元素的`with/height`，如果比图片本身大的话，可以使**图片自动垂直居中**。
2. 使用`content`属性
    * 可以更改元素内容。但改变的仅仅是**视觉呈现效果**。
    * 而且使用`content`生成的图片是**无法设置尺寸**的，导致图片看上去模糊。可以使用**SVG矢量**图片。
    * 生成的文本是无法选中、无法复制的。
    * **不要生成重要信息，可以生成一些无关紧要的内容。**如：装饰性图形或者序号之类的。
3. `user-select: none`可以设置文本不被选中。