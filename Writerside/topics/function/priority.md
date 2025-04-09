# 作业优先级

可以在配置文件（slurm.conf）时指定优先级调度类型 `PriorityType`

- **PriorityType=priority/basic** ：作业按照先进先出（FIFO）的原则进行优先级调度
- **PriorityType=priority/multifactor** ：作业优先级由多种因子综合决定



## 多因子插件

多因子插件的影响因子如下：

- **Age**：作业在队列中的等待时间，等待时间越长，权重越高
- **Association**：关联因子，每个关联都可以分配一个优先级。数字越大，请求此关联的作业的优先级就越高
- **Fairshare**： 分配的计算资源与消耗的计算资源的差额

- **Job size**：作业大小因子，跟作业申请的节点数、CPU核数、内存大小有关
- **Nice**：用户可以控制的优先级参数
- **Partition**：与节点分区相关
- **QOS**： 与服务质量相关
- **Site**：`job_submit` 和 `site_factor` 插件的影响因子
- **TRES**: 对于作业来说，每个可追踪资源都有自己的因子

<note>使用Fairshare需要运行记帐数据库</note>

```bash
任务优先级权重 =
	自定义权重 (site_factor) +
	作业等待时间权重 (PriorityWeightAge * age_factor) +
	关联权重 (PriorityWeightAssoc * assoc_factor) +
  公平共享权重(PriorityWeightFairshare * fair-share_factor) +
	作业大小权重(PriorityWeightJobSize * job_size_factor) +
	分区权重(PriorityWeightPartition * priority_job_factor) +
	服务质量权重(PriorityWeightQOS * QOS_factor) +
	资源权重(SUM(TRES_weight_cpu * TRES_factor_cpu,
	    TRES_weight_<type> * TRES_factor_<type>,
	    ...))
	Nice降级 - nice_factor
```



## 作业大小权重

作业大小因子跟作业申请的节点数、CPU核数、内存大小有关。可以通过配置 slurm.conf 中的 PriorityFavorSmall 参数配置Slurm支持较大还是较小的作业

- **PriorityFavorSmall=NO**:  支持大作业优先，作业越大，其作业大小因子就越大

- **PriorityFavorSmall=YES**: 支持小作业优先，作业越大，其作业大小因子就越小



## 公平共享权重

Fairshare用于确保用户在**长期运行**中公平地使用计算资源

Fairshare因子判断基于账号的的分配计算资源与实际消耗资源的差额（资源余量），余量越多的账号调度权重越高

- 默认情况下仅用**核时**（allocate_cpus * seconds）消耗的资源，但可以通过配置 slurm.conf 中的 `TRESBillingWeights` 参数使得计算消耗额外考虑内存、GPU 等资源

- 过去的使用记录不是永久影响的，它会随着时间衰减，可以通过配置 slurm.conf 中的 `PriorityDecayHalfLife` 参数配置半衰期

- Slurm提供了两种算法计算具体权重值

  -- **Fair Tree（默认）**：按账户结构分层计算资源份额，更公平、适合多用户组织结构

  -- **Classic（老版）**：简单计算，不考虑用户所属账户结构

