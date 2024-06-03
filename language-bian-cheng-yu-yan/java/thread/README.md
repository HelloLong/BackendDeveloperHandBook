# Thread

## 线程状态

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

* NEW（新建）：当通过`new Thread()`创建一个新的线程对象但还未调用其`start()`方法时，线程处于新建状态。此时线程对象已经存在，但是线程并没有真正开始执行。
* RUNNABLE（运行状态）：运行状态指的是线程正在执行代码时的活动状态。在Java中，线程的运行状态通常称为RUNNABLE。当调用了线程对象的`start()`方法后，线程会进入就绪状态。就绪状态意味着线程具备了执行条件，但并不保证立即开始执行。在Java虚拟机中，就绪状态的线程可能会等待调度器的选中，然后分配CPU时间片，进入运行状态。此时，线程可以执行，但并不一定会立即执行。此外，就绪状态也包括了那些因为时间片用完或者被挂起而暂时让出CPU，但在没有阻塞的情况下能够立即恢复执行的线程。如果就绪状态的线程被操作系统调度程序选中并获得CPU执行权，那么线程就进入了运行状态。值得注意的是，即使处于运行状态，线程也可能因为操作系统的调度或其他因素而暂时被挂起，等待下一次获得CPU执行权。
* BLOCKED（阻塞状态）：当线程试图获取某个对象的锁（例如进入synchronized代码块或方法），而该锁被其他线程持有时，该线程会进入阻塞状态（Blocked）。此时，线程会一直等待直到能够获取所需的锁才能继续执行。
* WAITING（等待状态）：当调用`wait()`、`join()`方法，或者在`synchronized`代码块中调用了`Thread.sleep(long millis)`等方法时，线程会进入等待状态（Waiting）。在这种状态下，线程不会消耗CPU资源，并且需要等待其他线程显式地唤醒才能继续执行，例如执行`notify()`、`notifyAll()`。
* TIMED\_WAITING（超时等待状态）：类似于等待状态，但这种状态下线程会在指定的时间后自动唤醒，例如，调用`Thread.sleep(long millis)`指定了超时时间、`Object.wait(long timeout)`、`LockSupport.parkNanos(long nanos)`或`Condition.awaitNanos(long nanos)`等方法会让线程进入限期等待状态。
* TERMINATED（终止状态）：线程执行完毕或者因异常退出`run()`方法后，线程就会变为终止状态。处于终止状态的线程无法再次被启动。

## References

美团一面：Java中线程有哪几种状态？[https://mp.weixin.qq.com/s/AdyXbbWBtyr-Eh6ZRsWMxw](https://mp.weixin.qq.com/s/AdyXbbWBtyr-Eh6ZRsWMxw)
