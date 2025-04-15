# 作业抢占

Slurm支持作业抢占，即停止低优先级的作业运行高优先级的作业
- 被抢占的作业可以被取消，或者重新排队，或者暂停等待
- 作业所在分区的分区调度优先级（PriorityTier）或其服务质量（QOS）可用于确定哪些作业可以抢占或被其他作业抢占





## 抢占配置

slurm配置可以在 slurm.conf 中指定，如果分区 / QOS 中有相同参数，优先使用分区/ QOS 中的

| 配置类型                   | 配置参数                | 说明                                                                                                                                                                                                                                                   |
|------------------------|:--------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| slurm配置                | SelectType          | 支持抢占的资源分配插件：<br/> -- select/linear：按节点分配<br/> -- select/cons_tres：按插槽/核心/CPU等资源分配                                                                                                                                                                    |
| slurm配置                | SelectTypeParameter | 配置可抢占资源类型（select/linear 仅支持 CR_Memory）<br/>-- CR_CPU：CPU 是可抢占资源<br/>-- CR_CPU_Memory：CPU 和内存是可抢占资源<br/>-- CR_Core：核心是可抢占资源<br/>-- CR_Core_Memory：核心和内存是可抢占资源<br/>-- CR_Socket：插槽是可抢占资源<br/>-- CR_Socket_Memory：内存和插槽是可抢占资源<br/>-- CR_Memory：内存是可抢占资源 |
| slurm配置 / 分区配置 / QOS配置 | GraceTime           | 抢占延迟时间（秒），仅在 PreemptType 设置为 partition_prio 时生效。默认值为零，表示此分区上不允许有抢占延迟                                                                                                                                                                                 |
| slurm配置 / 分区配置 / QOS配置 | PreemptMode         | 抢占机制：<br/> -- OFF：禁用（默认）<br/> -- CANCEL：直接取消<br/> -- GANG：启用轮转式调度<br/> -- REQUEUE：重新排队<br/> -- SUSPEND：挂起后恢复                                                                                                                                         |
| slurm配置                | PreemptType         | 识别哪些作业可以被抢占：<br/>-- preempt/none：禁用 <br/>-- preempt/partition_prio：按分区调度优先级 PriorityTier<br/>-- preempt/qos：按QOS规则                                                                                                                                   |
| slurm配置 / QOS配置        | PreemptExemptTime   | 指定作业在被抢占之前最小运行时间（分钟），当 PreemptMode 设置为 REQUEUE 或 CANCEL 才生效                                                                                                                                                                                          |
| 分区配置                   | PriorityTier        | 分区调度优先级（数值越高越优先），默认为1                                                                                                                                                                                                                                |
| 分区配置                   | OverSubscribe       | 资源<a href="share-resources.md">超额订阅</a>                                                                                                                                                                                                              |
| 分区配置                   | ExclusiveUser       | 配置独占的分区会阻止抢占                                                                                                                                                                                                                                         |
| slurm配置                | MCSParameters       | 如果在作业上设置了MCS标签，则抢占仅对相同 MCS 标签的其他作业有效                                                                                                                                                                                                                 |



## 基于分区的抢占

- 在 slurm.conf 中配置参数

```bash
# 设置抢占类型
PreemptType=preempt/partition_prio
```

- 可以修改分区参数 PreemptMode 确认抢占模式，也可以在 slurm.conf 中设置 PreemptMode
- 通过修改分区参数 PriorityTier 确定抢占优先级
- 修改分区配置
  <tabs group="update_partition">
    <tab id="update_partition_cmd" title="命令行" group-key="cmd">
       <code-block lang="bash">
          #修改分区调度优先级
          scontrol update PartitionName=debug PriorityTier=100 PreemptMode=CANCEL
       </code-block>
    </tab>
   <tab id="update_partition_conf" title="配置" group-key="conf">
       <code-block lang="bash">
          PartitionName=debug PriorityTier=100 PreemptMode=CANCEL
      </code-block>
  </tab>
  </tabs>



## 基于服务质量（QOS）的抢占

- 在 slurm.conf 中配置参数

```bash
# 设置抢占类型
PreemptType=preempt/qos
```

- 可以修改 QOS 参数 PreemptMode 确认抢占模式，也可以在 slurm.conf 中设置 PreemptMode
- 通过修 QOS 参数 Priority 确定抢占优先级
- 新增 QOS 配置

```bash
# 修改分区调度优先级
sacctmgr add qos high Priority=10000 PreemptMode=CANCEL
```




## 轮转式调度

Slurm支持轮转式调度（设置 PreemptMode=GANG），允许多个作业共享同一分区的资源，**通过周期性挂起/恢复实现资源分时复用**