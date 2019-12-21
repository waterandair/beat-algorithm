##### select,poll和epoll

其实所有的I/O都是轮询的方法,只不过实现的层面不同罢了.

这个问题可能有点深入了,但相信能回答出这个问题是对I/O多路复用有很好的了解了.其中tornado使用的就是epoll的.

selec,poll和epoll区别总结

基本上select有3个缺点:

连接数受限
查找配对速度慢
数据由内核拷贝到用户态
poll改善了第一个缺点

epoll改了三个缺点.

关于epoll的: http://www.cnblogs.com/my_life/articles/3968782.html

[selec,poll和epoll区别总结](http://www.cnblogs.com/Anker/p/3265058.html)

##### 