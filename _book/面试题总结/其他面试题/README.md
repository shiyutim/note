# 其他类别面试题
#### 请描述一下 cookies sessionStorage和localstorage区别
相同点：都存储在客户端

不同点：
* 存储大小：
    * cookie数据大小不能超过4k。
    * sessionStorage和localStorage。虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。
* 有效时间：
    * localStorage存储持久数据，浏览器关闭后数据不丢失除非主动删除数据
    * sessionStorage数据在当前浏览器窗口关闭后自动删除。
    * cookie设置的cookie过期时间之前一直有效
* 数据与服务器之间的交互方式
    * cookie的数据会自动的传递到服务器，服务器端也可以写cookie到客户端
    * sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
---
#### HTTP状态码
* 2xx 请求正常处理完毕
* 3xx需要进行附加操作以完成请求
* 4xx（客户端）服务器无法处理请求
* 5xx（服务器）服务器处理请求错误
---
#### px和em的区别
* px表示像素，是绝对单位，不会因为其他元素的尺寸变化而变化。
* em表示相对于父元素的字体大小。em是相对单位，没有一个固定的度量值，而是由其他元素尺寸来决定的相对值。

