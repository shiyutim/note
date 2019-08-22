1. 通过require() 来引入。
2.  cd.>xxx.txt 【建立空文件】
3. 事件
* 同步：同步就是你要做的事你列了一个清单，按照清单上的顺序 一个一个执行
* 异步：就是可以同时干好几件事
* 阻塞：就是按照清单上的顺序一件一件的往下走，当一件事没有做完，下面的事都干不了
* 非阻塞：就是这件事没有干完，后面的事不会等你这件事干完了再干，而是直接开始干下一件事，等你这件事干完了，后面的事也干完了，这样就大大提高了效率
4. Node.js本身是单进程单线程应用程序。但是因为V8引擎提供的异步执行回调接口，通过这些接口可以处理大量的并发，所以性能非常高。
5. 浏览器打印返回的字符串
```
let http = require('http');

http.createServer((req, res) =>  {
    res.writeHead(200, {'Content-Type': 'text/plain'});

    res.end('This is my first server');
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081');
```
6. fs是filesystem的简写，想要进行文件操作，就必须引入这个模块。
* `fs.readFile()`是异步函数用于读取文件。
* `fs.writeFile()`用于写入文件。
    * 第一个参数：文件路径
    * 第二个参数：文件内容
    * 第三个参数：回调函数（error）
```
fs.readFile('xxx.js', function(error, data) {
    
}}
```
7. events 模块只提供了一个对象： events.EventEmitter。EventEmitter 的核心就是事件触发与事件监听器功能的封装。
8. `toString()`方法可以用于把其他进制的文件转换为正常显示。
9. node执行的js文件，有各自的模块作用域。可以通过exports暴露出去。
10. 发送的HTTP回应使用`res.setHeader('Content-Type', 'text/plain; charset=utf-8');`能够转为utf-8的格式。防止乱码。
11. `Content-Type`用来指定对应的内容，不同的资源对应的Cpntent-Type是不一样的。图片一般不需要指定编码。一般只为字符数据指定编码：`charset=utf-8`。

|文件扩展名|Content-Type|
|:--|:--|
|.html|text/html|
|.txt|text/plain|
|.css|text/css|
|.js|application/x-javascript|

具体编码查询地址：`http://tool.oschina.net/commons`
12. `fs.readdir('xxx.txt', function(err, files))`能够读取目录。
13. `url.parse()`用来解析url路径。
```
// 第二个参数为true时，自动解析发送的参数
url.parse('/xxx', true)
```