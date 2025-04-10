# 作业抢占

Slurm支持作业抢占，即停止低优先级的作业运行高优先级的作业
- 被抢占的作业可以被取消，或者重新排队，或者暂停等待（PreemptMode）
- 作业所在分区的分区调度优先级（PriorityTier）或其服务质量（QOS）可用于确定哪些作业可以抢占或被其他作业抢占



## 抢占配置

可以在 slurm.conf 配置相关参数

| 配置参数                                       | 说明                                                         |
| :--------------------------------------------- | :----------------------------------------------------------- |
| **SelectType**                                 | 支持抢占的资源分配插件：<br/> - `select/linear`：节点分配<br/> - `select/cons_tres`：socket/core/CPU资源分配 |
| **SelectTypeParameter**                        | 配置可消耗资源类型                                           |
| **GraceTime**                                  | 抢占时间（秒）                                               |
| **JobAcctGatherType / JobAcctGatherFrequency** | 内存限制强制，超限作业自动终止                               |
| **PreemptMode**                                | 抢占机制：<br/> - `OFF`：禁用（默认）<br/> - `CANCEL`：直接取消<br/> - `GANG`：启用轮转式调度<br/> - `REQUEUE`：重新排队<br/> - `SUSPEND`：挂起后恢复 |
| **PreemptType**                                | 识别哪些作业可以被抢占：<br/> - `preempt/none`：禁用 <br/> - `preempt/partition_prio`：按分区调度优先级 PriorityTier<br/> - `preempt/qos`：按QOS规则 |
| **PreemptExemptTime**                          | 指定作业在被抢占之前最小运行时间                             |
| **PriorityTier**                               | 调度优先级（数值越高越优先），高优先分区抢占低优先           |
| **OverSubscribe**                              | 资源超额订阅                                                 |
| **ExclusiveUser**                              | 独占分区行为                                                 |
| **MCSParameters**                              | 如果在作业上设置了MCS标签，则抢占仅对相同 MCS 标签的其他作业有效 |



## 轮转式调度

Slurm支持轮转式调度（设置 PreemptMode=GANG），允许多个作业共享同一分区的资源，**通过周期性挂起/恢复实现资源分时复用**