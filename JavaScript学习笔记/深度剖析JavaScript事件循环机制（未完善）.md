众所周知，JavaScript 语言采用的是单线程模型。即所有任务只能在一个线程上完成，一次只能做一件事。
但是，任何一个程序在执行的时候，都可能会开启多个任务，JavaScript也一样，那么作为单线程的语言--JavaScript，是怎么处理这种多任务的情况的呢？
事实上，**JS是通过异步的方式来处理多任务的，而`事件循环(Event Loop)`是处理异步函数的具体方法。**

#异步
即同一时间可以做多个事情
#多任务
JavaScript在执行的时候，也可能会开启多个任务事件，如：
任务1：监听事件；比如监听按钮的点击事件、鼠标事件、键盘事件等
任务2：开启计时器；每隔一段时间做一件事情
...
#任务队列



---
参考文献
1. [深入理解JavaScript事件循环](https://www.cnblogs.com/yugege/p/9598265.html)
2. [2分钟了解 JavaScript Event Loop](https://www.bilibili.com/video/BV1kf4y1U7Ln?from=search&seid=11880379691261548174 "2分钟了解 JavaScript Event Loop | 面试必备")
