# kubernetes k8s

## k8s 基础概念

### k8s 是什么

Kubenetes是一个针对容器应用，进行自动部署，弹性伸缩和管理的开源系统。主要功能是生产环境中的容器编排。

### k8s架构的组成是什么

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

## References

[kubernetes面试题汇总](https://mp.weixin.qq.com/s/X-f4Z3qgwShNGfHa\_CNxWg)&#x20;