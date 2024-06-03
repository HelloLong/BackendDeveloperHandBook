# RedisDistributeLock redis分布式锁

## 注意点

* **「互斥性」**: 任意时刻，只有一个客户端能持有锁。
* **「锁超时释放」**：持有锁超时，可以释放，防止不必要的资源浪费，也可以防止死锁。
* **「可重入性」**:一个线程如果获取了锁之后,可以再次对其请求加锁。
* **「高性能和高可用」**：加锁和解锁需要开销尽可能低，同时也要保证高可用，避免分布式锁失效。
* **「安全性」**：锁只能被持有的客户端删除，不能被其他客户端删除

## References <a href="#activity-name" id="activity-name"></a>

Redis实现分布式锁的7种方案，及正确使用姿势！[https://www.cnblogs.com/wangyingshuo/p/14510524.html](https://www.cnblogs.com/wangyingshuo/p/14510524.html)
