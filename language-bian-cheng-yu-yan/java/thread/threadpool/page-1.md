# Page 1

### 线程池中线程实现复用的原理 <a href="#si-xian-cheng-chi-zhong-xian-cheng-shi-xian-fu-yong-de-yuan-li" id="si-xian-cheng-chi-zhong-xian-cheng-shi-xian-fu-yong-de-yuan-li"></a>



线程池的核心功能就是实现线程的重复利用，那么线程池是如何实现线程的复用呢？

线程在线程池内部其实被封装成了一个 Worker 对象

<figure><img src="https://cdn.tobebetterjavaer.com/paicoding/64eca0f0c92bb74b6f428f7a87ccf1cd.png" alt=""><figcaption></figcaption></figure>

Worker 继承了 [AQSopen in new window](https://javabetter.cn/thread/aqs.html)，也就是具有一定锁的特性。

创建线程来执行任务的方法，上面提到了，是通过 addWorker 方法。在创建 Worker 对象的时候，会把线程和任务一起封装到 Worker 内部，然后调用 runWorker 方法来让线程执行任务，接下来我们就来看一下 runWorker 方法。
