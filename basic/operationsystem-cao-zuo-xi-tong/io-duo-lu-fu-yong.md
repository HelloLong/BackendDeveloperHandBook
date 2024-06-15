# IO 多路复用

## IO处理思路

每个网络链接都linux内核都是文件描述符(fd)，DMA会将接受到的数据拷贝到文件中。

```java
// Some code
while(1) {
    for (Fdx in (FdA ~ FdE)) {
        if (Fdx 有数据) {
            读 fdx;
            处理;
        }
    }
}
```

以上这种方式最大的问题是在判断文件中是否有数据需要频繁切换内核态和用户态。

## Select

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>select</p></figcaption></figure>

select通过内核判断文件描述符(fd)是否有数据，然后用bitmap标识出来。程序通过bitmap判断哪些fd上有数据。

缺点：

* bitmap大小受限，最大1024
* bitmap每次需要重新置位
* bitmap需要从用户态拷贝到内核态，涉及用户态和内核态切换
* 程序判断文件描述符是否有数据的过程需要遍历所有文件描述符，产生O(n)的复杂度

## Poll

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>poll</p></figcaption></figure>

poll 优化了bitmap的数据结构，使用pollfd替代。

优化点

* pollfd使用数组的方式不再有大小1024受限
* 只需重置pollfd中的revents，不需要重置整个bitmap



## Epoll

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>epoll</p></figcaption></figure>

