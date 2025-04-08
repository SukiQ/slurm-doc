# 分区管理



Slurm中的分区(Partition)是计算节点的逻辑分组，用于：

- 组织不同类型的计算资源（如CPU节点、GPU节点）
- 设置不同的作业策略和限制
- 实现多租户资源隔离
- 提供优先级调度机制



## 查看分区



### 分区概览

使用 `scontrol show partitions` 查看所有分区，或 `scontrol show partition <分区名称>` 查看指定分区

```bash
> scontrol show partitions

PartitionName=debug
   AllowGroups=ALL AllowAccounts=ALL AllowQos=ALL
   AllocNodes=ALL Default=YES QoS=N/A
   DefaultTime=NONE DisableRootJobs=NO ExclusiveUser=NO ExclusiveTopo=NO GraceTime=0 Hidden=NO
   MaxNodes=UNLIMITED MaxTime=UNLIMITED MinNodes=0 LLN=NO MaxCPUsPerNode=UNLIMITED MaxCPUsPerSocket=UNLIMITED
   NodeSets=ALL
   Nodes=node[136-139]
   PriorityJobFactor=1 PriorityTier=1 RootOnly=NO ReqResv=NO OverSubscribe=NO
   OverTimeLimit=NONE PreemptMode=REQUEUE
   State=UP TotalCPUs=32 TotalNodes=4 SelectTypeParameters=NONE
   JobDefaults=(null)
   DefMemPerNode=UNLIMITED MaxMemPerNode=UNLIMITED
   TRES=cpu=32,mem=124000M,node=4,billing=32
```



### 分区状态

使用 `sinfo` 查看所有分区状态，或 `sinfo -p <分区名称>` 查看指定分区

```bash
> sinfo 

PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
debug*       up   infinite      4   idle node[136-139]
```



## 创建分区

使用 `scontrol create` 命令，或者编辑 `slurm.conf` 文件创建分区
<tabs group="create_partition">
    <tab id="cmd" title="命令行" group-key="cmd">
        How to install on Windows.
    </tab>
    <tab id="conf" title="配置" group-key="conf">
        How to install on macOS.
    </tab>
</tabs>

