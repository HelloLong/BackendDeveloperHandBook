# HighConcurrency 高并发

而我们在应对高并发大流量时也会采用类似“抵御洪水”的方案，归纳起来共有三种方法。

Scale-out（横向扩展）：分而治之是一种常见的高并发系统设计方法，采用分布式部署的方式把流量分流开，让每个服务器都承担一部分并发和流量。

缓存：使用缓存来提高系统的性能，就好比用“拓宽河道”的方式抵抗高并发大流量的冲击。

异步：在某些场景下，未处理完成之前我们可以让请求先返回，在数据准备好之后再通知请求方，这样可以在单位时间内处理更多的请求。

## References

[高并发架构设计方法：面对高并发，怎么对症下药？](https://time.geekbang.org/column/article/487665?utm\_campaign=geektime\_search\&utm\_content=geektime\_search\&utm\_medium=geektime\_search\&utm\_source=geektime\_search\&utm\_term=geektime\_search)

[高并发系统：它的通用设计方法是什么？](https://time.geekbang.org/column/article/137323?utm\_campaign=geektime\_search\&utm\_content=geektime\_search\&utm\_medium=geektime\_search\&utm\_source=geektime\_search\&utm\_term=geektime\_search)

[大厂面试：如何设计一个高并发架构？](https://mp.weixin.qq.com/s/XJdsxvc9QE16O1w-JHuUQA)

\
