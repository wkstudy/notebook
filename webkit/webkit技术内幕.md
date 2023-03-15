# 阅读《webkit技术内幕》的笔记
> 一些标注都记在图书里，这里是一些额外的想法

## 第二章 html网页与结构
这里谈到 DOMContentLoaded是在dom树构建完成之后调用的，onload是在各个资源（如图片等）加载完调用的，那么对于异步的js资源( async defer)是在何时调用的
```
// 用http-server 起下demo
module
1.js:1 defer
test.html:40 DOMContentLoaded
2.js:1 async
test.html:43 onload

<!-- 把html里引用的图片注释掉 -->
async
3.js:1 module
1.js:1 defer
test.html:40 DOMContentLoaded
test.html:43 onload
```
1. 可以看到defer总是在DOMContentLoaded之前调用，async前后不一致，但都是在onload之前执行，我的理解是async异步下载，下载完立刻执行，但可能下载完时dom树已经完成了构建，也可能没有，所以出现了上述情况
2. 另外，这里也说明了，async的执行顺序可能可在html里写的顺序不一致，先下载完先执行，defer执行顺序总和写的顺序一致
3. type=module的也是异步加载，类似defer的效果