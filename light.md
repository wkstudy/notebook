# light
> 随时的一些想法，包含各种各类，暂时想不到合适的地方去记录，等到内容有一定规模的时候再做整理



### nodejs 二进制流
这里的二进制流还不是指按照0101来的，每一位是16进制
```
let buf = Buffer.from([1, 2, 3]);
let buf2 = Buffer.from('hello')
console.log(buf)
console.log(buf2)
buf.writeInt8(16, 1)
console.log(buf)
<Buffer 01 02 03>
<Buffer 68 65 6c 6c 6f>
<Buffer 01 10 03>
```
为啥int8是2位二进制呢？

这里是我的理解：int8是8bit，可表示的2的8次方个数，nodejs二进制流单独一个（16进制）可表示2的4次方个数，那么要表示2的8次方的话就需要2位了

http2的优势也有一个是二进制传输，那么相比文本传输，优势在哪呢？

[refer](https://juejin.cn/post/6945266413917437983#heading-0)
[文本文件和二进制文件的区别？请举例说明。 - 史历的回答 - 知乎](https://www.zhihu.com/question/19971994/answer/570107874)
[文本文件与二进制文件区别](https://www.cnblogs.com/zhangjiankun/archive/2011/11/27/2265184.html)

### 单工、半双工、全双工
单工：电视，一方发送，一方接收
半双工：单行道 http1.x 
全双工：双行道  http2 多路复用
http2 http1的区别
