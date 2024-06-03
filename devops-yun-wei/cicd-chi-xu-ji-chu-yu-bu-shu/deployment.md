# Deployment

## **Blue/Green Deployment 蓝绿部署**

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

蓝绿发布比较简单，只是对全量发布的一种优化而已，发布前不用全部停机，而是另外部署新版本全部实例，然后再把流量全部再切换到新版本。

## Canary Deployment 金丝雀发布 <a href="#h_501209052_2" id="h_501209052_2"></a>

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

先升级服务一个实例，如果该实例没有问题，再全部升级剩余实例，如果有问题，再进行回滚。

## Rolling Deployment 滚动发布 <a href="#h-rolling-deployment-vs-canary-deployment" id="h-rolling-deployment-vs-canary-deployment"></a>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

滚动发布则是在金丝雀发布的基础上进行的改进和优化，第一次也是使用金丝雀发布，后续则使用多批次的形式发布剩余实例，每次批次之间会进行观察，如果有问题，再进行回滚。

灰度强调是部分节点给指定用户体验没问题后再扩大发布，而滚动强调的是自动节点的更换，相对有一定风险两都结合即减少人工工作量风险也降低。滚动式发布一般和金丝雀发布配合，先发一台金丝雀去验证流量，再按批次增量发布。

