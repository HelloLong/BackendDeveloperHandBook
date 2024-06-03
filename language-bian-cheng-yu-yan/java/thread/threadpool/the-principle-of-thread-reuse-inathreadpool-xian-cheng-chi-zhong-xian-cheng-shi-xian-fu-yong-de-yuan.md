# The principle of thread reuse in a threadpool 线程池中线程实现复用的原理

## 原理

线程在线程池内部其实被封装成了一个 Worker 对象，Worker 继承了 AQS，也就是具有一定锁的特性。

创建线程来执行任务的方法，上面提到了，是通过 addWorker 方法。在创建 Worker 对象的时候，会把线程和任务一起封装到 Worker 内部，然后调用 runWorker 方法来让线程执行任务。

线程在执行完任务之后，会继续从 getTask 方法中获取任务，获取不到就会退出。



## 注意点

ArrayBlockingQueue take()和poll()的一点区别。使用take()函数，如果队列中没有数据，则线程wait释放CPU，而poll()则不会等待，直接返回null；同样，空间耗尽时offer()函数不会等待，直接返回false，而put()则会wait，因此如果你使用while(true)来获得队列元素，千万别用poll()，CPU会100%的。

另外，如果你希望ThreadPoolExecutor中常驻n个线程，请调用“public void allowCoreThreadTimeOut(boolean value)”将该属性设置为false，否则会不停循环轮询队列，会占用大量CPU。

```
// Some code
getTask() { 
    for (;;) { 
        try { 
            int state = runState; 
            if (state > SHUTDOWN) return null; 
                Runnable r; 
            if (state == SHUTDOWN) // Help drain 
                queue r = workQueue.poll(); 
            else if (poolSize > corePoolSize || allowCoreThreadTimeOut) 
                r = workQueue.poll(keepAliveTime, TimeUnit.NANOSECONDS); 
            else r = workQueue.take();
```



## References

24张图带你彻底弄懂 Java 线程池[https://javabetter.cn/thread/pool.html](https://javabetter.cn/thread/pool.html#%E4%BA%94%E3%80%81%E7%BA%BF%E7%A8%8B%E6%98%AF%E5%A6%82%E4%BD%95%E8%8E%B7%E5%8F%96%E4%BB%BB%E5%8A%A1%E4%BB%A5%E5%8F%8A%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E8%B6%85%E6%97%B6%E7%9A%84)
