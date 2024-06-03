# APM(Application Performance Management) 应用性能管理

## 基本概念

APM 是Application Performance Managment的缩写，即：“应用性能管理”。现代的APM体系，基本都是参考Google的《[Dapper，大规模分布式系统的跟踪系统](https://www.zhihu.com/search?q=Dapper%EF%BC%8C%E5%A4%A7%E8%A7%84%E6%A8%A1%E5%88%86%E5%B8%83%E5%BC%8F%E7%B3%BB%E7%BB%9F%E7%9A%84%E8%B7%9F%E8%B8%AA%E7%B3%BB%E7%BB%9F\&search\_source=Entity\&hybrid\_search\_source=Entity\&hybrid\_search\_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2303779331%7D)》 的体系来实践的。

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Gartner的APM Conceptual Framework（概念框架）</p></figcaption></figure>

1、终端用户体验：End User Experience

2、运行时应用架构：Runtime application architecture

3、业务事务分析：Business Transactions

4、深度组件监控：Deep Dive Component Monitoring

5、分析报告：Analytics / Reporting

## 方法论

从用户的角度来说：可以保证为用户提供高质量的服务。从企业的角度来说：可以为企业降低IT的总成本。

#### Metrics、Tracing和Logging是APM中三个主要的概念

* Metrics 更节省存储资源，因为数据会被聚合后存储。
* Logging 需要的存储空间最大，成本最高。
* Tracing 也是存储大户，由于它的业务特点可以采样，所以总体存储成本则介于两者之间。

## 框架

### 主流监控

Skywalking

ELK stack

prometheus

open-falcon

Sensu

pinpoint

zipkin

Jaeger

Cat

#### 传统监控

zabbix

nagios

cacti

#### 前端监控

sentry

webfunny

zanePerfor



## References

[有什么知名的开源apm(Application Performance Management)工具吗？](https://www.zhihu.com/question/27994350/answer/2303779331)
