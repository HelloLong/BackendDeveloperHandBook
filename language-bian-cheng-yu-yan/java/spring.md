# Spring

## **三级缓存是哪三级？**

spring 中使用了 3 个 map 来作为三级缓存，每一级对应一个 map

| 第几级缓存 | 对应的 map                                            | 说明                                                    |
| ----- | -------------------------------------------------- | ----------------------------------------------------- |
| 第 1 级 | Map\<String, Object> singletonObjects              | 用来存放已经完全创建好的单例 beanbeanName->bean 实例                  |
| 第 2 级 | Map\<String, Object> earlySingletonObjects         | 用来存放早期的 beanbeanName->bean 实例                         |
| 第 3 级 | Map\<String, ObjectFactory\<?>> singletonFactories | 用来存放单例 bean 的 ObjectFactorybeanName->ObjectFactory 实例 |

## References

Spring系列第56篇：一文搞懂spring到底为什么要用三级缓存？[https://cloud.tencent.com/developer/article/1796740](https://cloud.tencent.com/developer/article/1796740)

\
