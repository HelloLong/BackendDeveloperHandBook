# BigData 大数据

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

在大数据架构中，Hive和HBase是协作关系，数据流一般如下： 通过ETL工具将数据源抽取到HDFS存储；通过Hive清洗、处理和计算原始数据；HIve清洗处理后的结果，如果是面向海量数据随机查询场景的可存入Hbase数据应用从HBase查询数据。

## References

[「只需7分钟！我将抢走你的赞」大数据入门](https://mp.weixin.qq.com/s?\_\_biz=MzI4Njg5MDA5NA==\&mid=2247486604\&idx=1\&sn=fba7a7f34c8faf182b88b137ff85b3ed\&chksm=ebd74d8ddca0c49b87fc50027d94b272b7df7ac11e966a6a85b7c1f9bafec846f25a3c6461ef\&token=2140209384\&lang=zh\_CN#rd)

[Hadoop、Hive、HDFS、Hbase之间关系](https://zhuanlan.zhihu.com/p/483077758)

\


\
