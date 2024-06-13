# kubernetes k8s

## k8s 基础概念

### k8s 是什么

Kubenetes是一个针对容器应用，进行自动部署，弹性伸缩和管理的开源系统。主要功能是生产环境中的容器编排。

### k8s架构的组成

K8S集群至少需要一个**主节点（Master）**和多个**计算节点（Node）**。

主节点主要用于暴露API，调度部署和节点的管理；

计算节点运行一个容器运行环境，一般是docker环境，同时运行一个K8s的代理（kubelet）用于和master通信。计算节点也会运行一些额外的组件，像记录日志，节点监控，服务发现等等。计算节点是k8s集群中真正工作的节点。

**Master节点（默认不参加实际工作）：**

* Kubectl：客户端命令行工具，作为整个K8s集群的操作入口；
* Api Server：在K8s架构中承担的是“桥梁”的角色，作为资源操作的唯一入口，它提供了认证、授权、访问控制、API注册和发现等机制。客户端与k8s群集及K8s内部组件的通信，都要通过Api Server这个组件；
* Controller-manager：负责维护群集的状态，比如故障检测、自动扩展、滚动更新等；
* Scheduler：负责资源的调度，按照预定的调度策略将pod调度到相应的node节点上；
* Etcd：担任数据中心的角色，保存了整个群集的状态；

**Node节点：**

* Kubelet：负责维护容器的生命周期，同时也负责Volume和网络的管理，一般运行在所有的节点，是Node节点的代理，当Scheduler确定某个node上运行pod之后，会将pod的具体信息（image，volume）等发送给该节点的kubelet，kubelet根据这些信息创建和运行容器，并向master返回运行状态。（自动修复功能：如果某个节点中的容器宕机，它会尝试重启该容器，若重启无效，则会将该pod杀死，然后重新创建一个容器）；
* Kube-proxy：Service在逻辑上代表了后端的多个pod。负责为Service提供cluster内部的服务发现和负载均衡（外界通过Service访问pod提供的服务时，Service接收到的请求后就是通过kube-proxy来转发到pod上的）；
* container-runtime：是负责管理运行容器的软件，比如docker
* Pod：是k8s集群里面最小的单位。每个pod里边可以运行一个或多个container（容器），如果一个pod中有两个container，那么container的USR（用户）、MNT（挂载点）、PID（进程号）是相互隔离的，UTS（主机名和域名）、IPC（消息队列）、NET（网络栈）是相互共享的。我比较喜欢把pod来当做豌豆夹，而豌豆就是pod中的container；

### Kubernetes相关基础概念

**master：**

k8s集群的管理节点，负责管理集群，提供集群的资源数据访问入口。拥有Etcd存储服务（可选），运行Api Server进程，Controller Manager服务进程及Scheduler服务进程；

**node（worker）：**

Node（worker）是Kubernetes集群架构中运行Pod的服务节点，是Kubernetes集群操作的单元，用来承载被分配Pod的运行，是Pod运行的宿主机。运行docker eninge服务，守护进程kunelet及负载均衡器kube-proxy；

**pod：**

运行于Node节点上，若干相关容器的组合。Pod内包含的容器运行在同一宿主机上，使用相同的网络命名空间、IP地址和端口，能够通过localhost进行通信。Pod是Kurbernetes进行创建、调度和管理的最小单位，它提供了比容器更高层次的抽象，使得部署和管理更加灵活。一个Pod可以包含一个容器或者多个相关容器；

**label：**

Kubernetes中的Label实质是一系列的Key/Value键值对，其中key与value可自定义。Label可以附加到各种资源对象上，如Node、Pod、Service、RC等。一个资源对象可以定义任意数量的Label，同一个Label也可以被添加到任意数量的资源对象上去。Kubernetes通过Label Selector（标签选择器）查询和筛选资源对象；

**Replication Controller：**

Replication Controller用来管理Pod的副本，保证集群中存在指定数量的Pod副本。

集群中副本的数量大于指定数量，则会停止指定数量之外的多余容器数量。反之，则会启动少于指定数量个数的容器，保证数量不变。

Replication Controller是实现弹性伸缩、动态扩容和滚动升级的核心；

**Deployment：**

Deployment在内部使用了RS来实现目的，Deployment相当于RC的一次升级，其最大的特色为可以随时获知当前Pod的部署进度；

**HPA（Horizontal Pod Autoscaler）：**

Pod的横向自动扩容，也是Kubernetes的一种资源，通过追踪分析RC控制的所有Pod目标的负载变化情况，来确定是否需要针对性的调整Pod副本数量；

**Service：**

Service定义了Pod的逻辑集合和访问该集合的策略，是真实服务的抽象。

Service提供了一个统一的服务访问入口以及服务代理和发现机制，关联多个相同Label的Pod，用户不需要了解后台Pod是如何运行；

**Volume：**

Volume是Pod中能够被多个容器访问的共享目录，Kubernetes中的Volume是定义在Pod上，可以被一个或多个Pod中的容器挂载到某个目录下；

**Namespace：**

Namespace用于实现多租户的资源隔离，可将集群内部的资源对象分配到不同的Namespace中，形成逻辑上的不同项目、小组或用户组，便于不同的Namespace在共享使用整个集群的资源的同时还能被分别管理；

\


## References

[kubernetes面试题汇总](https://mp.weixin.qq.com/s/X-f4Z3qgwShNGfHa\_CNxWg)&#x20;

2023高薪必备：K8S面试题 （史上最全 + 收藏版）[https://mp.weixin.qq.com/s/8TNCVZ5jSYmJxXimI5XbkQ](https://mp.weixin.qq.com/s/8TNCVZ5jSYmJxXimI5XbkQ)
