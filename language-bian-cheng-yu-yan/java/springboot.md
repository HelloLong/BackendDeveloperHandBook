# SpringBoot

## SpringStarter

Spring starter 是 Springboot 的核心，可以理解为一个可拔插式的插件，利用starter，可以避免一些繁琐的配置，将 starter 里面的功能开箱即用。

利用starter实现自动化配置只需要两个条件——maven依赖、配置文件。引入maven实质上就是导入jar包，spring-boot启动的时候会找到jar包中的resources/META-INF/spring.factories文件，根据spring.factories文件中的配置，找到需要自动配置的类。

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



## References

Spring - starter机制[https://zhuanlan.zhihu.com/p/665466489](https://zhuanlan.zhihu.com/p/665466489)
