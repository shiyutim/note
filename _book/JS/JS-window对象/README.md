 `window.onload = function() {}`代表当网页加载完成后要做些什么
#### location对象
1. `location.assign("https://www.baidu.com")`使用这个方法可以打开一个新的页面，并且会在浏览历史中增加一条记录。这个方法等同于`window.location.href="https://www.baidu.com"`
2. 上面的两种方法都可以通过点击后退按钮导航到上一个页面，有时候我们不希望这种操作发生，可以使用`replace()`方法。`location.replace("https://www.baidu.com")`这样使用后就不能点击回退按钮回到上一个页面了
3. `reload()`方法用于重新加载当前的文档。
```
//语法
location.reload(force)
```
该方法如果**没有规定参数，或者参数是false**，他会检测文档是否改变，如果文档已经改变，`reload()`会再次下载文档，如果没有改变，该方法会从缓存中加载文档。

如果该方法的参数为true,`reload(true)`，那么无论怎样都会在服务器上重新下载该文档。

#### history对象
1. 通过使用下面的方法可以实现前进后退的功能。
```
history.go(1)  //前进
history.go(-1) //后退
```
还可以附带参数，会跳转到历史纪录中包含该字符串的第一个位置。无论是前进或者后退。
```
history.go("baidu.com")
```
2. `history.length`保存着历史记录的数量。如果你想确定用户是否一开始就打开了你的页面，可以这么使用：
```
if(history.length === 0) {}
```