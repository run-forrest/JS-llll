### BOM
#### 12.2 location 对象
下面两行代码都会执行与显式调用 assign()一样的操作：
window.location = "http://www.wrox.com";
location.href = "http://www.wrox.com";
在这 3 种修改浏览器地址的方法中，设置 location.href 是最常见的
最后一个修改地址的方法是 reload()，它能重新加载当前显示的页面。调用 reload()而不传参
数，页面会以最有效的方式重新加载。也就是说，如果页面自上次请求以来没有修改过，浏览器可能会
从缓存中加载页面。如果想强制从服务器重新加载，可以像下面这样给 reload()传个 true：
location.reload(); // 重新加载，可能是从缓存加载
location.reload(true); // 重新加载，从服务器加载
脚本中位于 reload()调用之后的代码可能执行也可能不执行，这取决于网络延迟和系统资源等因
素。为此，最好把 reload()作为最后一行代码。
东西不是很多，感觉大部分都是一些查一下就行的东西。
