# scontrol

`scontrol` 用于查看或修改 Slurm **配置**和**状态**

```bash
scontrol [选项] [子命令]
```

<note>scontrol 命令的修改会在重启后失效，可以使用 <code>scontrol write config</code> 将修改持久化</note>



- 选项


| 参数           | 描述                                                              |
| -------------- |-----------------------------------------------------------------|
| -a, --all      | 当使用 show 命令时，显示所有分区、它们的作业和作业步骤，包括隐藏分区和对用户组不可用的分区信息              |
| -M, --clusters | 指定要发出命令的集群。只能指定一个集群名称。注意，slurmdbd 必须处于运行状态。此选项隐式设置 --local 选项   |
| -d, --details  | 显示可用的附加详细信息                                                     |
| --federation   | 如果是联盟成员，则报告来自联盟的作业                                              |
| -F, --future   | 报告处于未来状态的节点                                                     |
| -h, --help     | 打印帮助信息，描述 scontrol 的使用方法                                        |
| --hide         | 不显示关于隐藏分区、它们的作业和作业步骤的信息。默认行为是不显示这些信息                            |
| --json         | 以 JSON 格式转储信息，使用默认的数据解析插件或显式数据解析器。所有信息都会转储。此选项隐式设置 --details 选项 |
| --local        | 仅显示本集群的本地信息，忽略其他集群。覆盖 --federation                              |
| -o, --oneliner | 每条记录打印一行信息                                                      |
| -Q, --quiet    | 不打印警告或信息消息，仅打印致命错误消息                                            |
| --sibling      | 显示联合集群上的所有兄弟作业。隐式设置 --federation                                |
| -u, --uid      | 尝试以用户uid的身份更新作业，而不是调用用户的Id                                      |
| -v, --verbose  | 打印详细事件日志。多个 '-v' 会进一步增加日志的详细程度。默认情况下，仅显示错误信息                    |
| -V, --version  | 打印版本信息并退出                                                       |
| --yaml         | 以 YAML 格式转储信息，使用默认的数据解析插件或显式数据解析器。所有信息都会转储                      |



- 子命令

| 命令               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| cancel_reboot      | 取消节点上的待处理重启，节点将被取消排空，原因将被清除       |
| create             | 创建新的节点、分区或预留                                     |
| completing         | 显示所有处于`COMPLETING`/`DOWN` 状态的作业及其关联节点       |
| delete             | 删除指定的节点                                               |
| errnumstr          | 给定一个错误号，返回描述性字符串                             |
| fsdampeningfactor  | 设置 slurmctld 中的 FairShareDampeningFactor                 |
| getaddrs           | 从 slurmctld 获取节点的 IP 地址                              |
| help               | 显示 scontrol 选项和命令的描述                               |
| hold               | 阻止待处理作业启动                                           |
| notify             | 发送消息到指定作业的标准错误                                 |
| pidinfo            | 打印与指定进程 ID 对应的 Slurm 作业 ID 和计划终止时间        |
| listpids           | 打印作业步骤中的进程 ID 列表                                 |
| ping               | ping slurmctld 主从守护进程并报告它们是否响应                |
| power              | 控制提供的节点列表的电源状态<br/> -- down：将节点置入省电模式<br/> -- down asap：标记节点进行电源关闭，正在运行的作业将先完成<br/> -- down force：取消节点上的所有作业，关闭电源并重置状态<br/> -- up：将节点从省电模式移出 |
| reboot             | 重启系统中的节点                                             |
| reconfigure        | 指示所有 slurmctld 和 slurmd 守护进程重新读取配置文件        |
| release            | 释放先前被持有的作业以开始执行                               |
| requeue            | 将运行、暂停或完成的 Slurm 批处理作业重新排队                |
| requeuehold        | 将作业重新排队并置于持有状态                                 |
| resume             | 恢复先前暂停的作业                                           |
| schedloglevel      | 启用或禁用调度器日志                                         |
| setdebug           | 更改 slurmctld 守护进程的调试级别                            |
| setdebugflags      | 添加或移除 slurmctld 守护进程的调试标志                      |
| show               | 显示指定实体的状态<br/> -- aliases：返回与给定主机名关联的所有节点名称值<br/> -- assoc_mgr ：显示 slurmctld 的用户、关联和 QOS 的当前缓存内容<br/> -- bbstat：显示当前突发缓冲插件的状态工具输出<br/> -- burstbuffer   ：显示突发缓冲插件的当前状态<br/> -- config：显示来自配置文件的参数名称<br/> -- daemons：报告此节点上应运行的守护进程<br/> -- dwstat：显示当前突发缓冲插件的状态工具输出<br/> -- federation：显示控制器所属的联合名称及其成员<br/> -- frontend  ：显示已配置的前端节点<br/> -- hostlist  ：输出主机列表表达式<br/> -- hostlistsorted：输出排序后的主机列表表达式<br/> -- hostnames ：输出单个主机名列表<br/> -- job   ：显示所有作业的统计信息<br/> -- licenses  ：显示所有配置许可证的统计信息<br/> -- node  ：显示所有节点的统计信息<br/> -- partition ：显示所有分区的统计信息<br/> -- reservation   ：显示所有预留的统计信息<br/> -- slurmd：显示当前节点上运行的 slurmd 的统计信息<br/> -- step  ：显示所有作业步骤的统计信息<br/> -- topology  ：显示定义的拓扑布局信息 |
| shutdown           | 指示 Slurm 守护进程保存当前状态并终止                        |
| suspend            | 暂停正在运行的作业                                           |
| takeover           | 指示 Slurm 的备份控制器接管系统控制                          |
| top                | 将指定作业 ID 移动到相同用户、分区、帐户和 QOS 的作业队列顶部 |
| token              | 返回用于支持 JWT 身份验证的授权令牌                          |
| uhold              | 阻止待处理作业启动，供系统管理员使用                         |
| update             | 更新作业、步骤、节点、分区或预留的配置                       |
| version            | 显示正在执行的 scontrol 的版本号                             |
| wait_job           | 等待作业及其所有节点准备好使用或作业进入终止状态             |
| write batch_script | 将给定作业 ID 的批处理脚本写入文件或标准输出                 |
| write config       | 将当前配置写入文件                                           |



## 分区参数

| 参数               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| AllocNodes         | 用户可以执行作业的节点列表                                   |
| AllowAccounts      | 允许使用该分区的账户列表                                     |
| AllowGroups        | 允许使用该分区的用户组列表                                   |
| AllowQOS           | 允许使用该分区的QOS列表                                      |
| Alternate          | 当分区状态为DRAIN或INACTIVE时使用的备用分区                  |
| CpuBind            | 任务与资源绑定模式：<br/> -- none：不进行 CPU 绑定<br/> -- socket：绑定到 CPU 插槽<br/> -- core：绑定到物理核心<br/> -- thread：绑定到逻辑线程<br/> -- ldom：绑定倒 NUMA 域<br/> -- off：禁用之前设置的绑定 |
| Default            | 是否作为未指定分区作业的默认分区                             |
| DefaultTime        | 未指定时间限制的作业的默认运行时间                           |
| DefMemPerCPU       | 每个CPU的默认内存分配（MB）                                  |
| DefMemPerNode      | 每个节点的默认内存分配（MB）                                 |
| DenyAccounts       | 禁止使用该分区的账户列表                                     |
| DenyQOS            | 禁止使用该分区的QOS列表                                      |
| DisableRootJobs    | 是否禁止root用户提交作业                                     |
| ExclusiveUser      | 节点是否独占分配给单个用户                                   |
| GraceTime          | 被抢占作业的宽限时间（秒）                                   |
| Hidden             | 是否隐藏分区及其作业                                         |
| JobDefaults        | 作业默认值（逗号分隔的key=value列表）                        |
| MaxCPUsPerNode     | 每个节点可分配的最大CPU数                                    |
| LLN                | 是否在空闲CPU最少的节点上调度作业                            |
| MaxMemPerCPU       | 每个CPU的最大内存分配（MB）                                  |
| MaxMemPerNode      | 每个节点的最大内存分配（MB）                                 |
| MaxNodes           | 单个作业可分配的最大节点数                                   |
| MaxTime            | 作业最大运行时间                                             |
| MinNodes           | 单个作业分配的最小节点数                                     |
| MaxCPUsPerSocket   | 每个socket可分配的最大CPU数                                  |
| Nodes              | 关联到分区的节点列表                                         |
| OverSubscribe      | 是否允许多个作业共享计算资源                                 |
| OverTimeLimit      | 作业可超时运行的分钟数（软限制→硬限制）                      |
| **PartitionName**  | 分区名称（必填）                                             |
| PowerDownOnIdle    | 空闲节点是否立即进入省电模式                                 |
| PreemptMode        | 作业抢占机制                                                 |
| PriorityJobFactor  | 优先级计算因子（priority/multifactor插件使用）               |
| PriorityTier       | 分区优先级层级（值越高优先级越高）                           |
| QOS                | 分区QOS设置                                                  |
| ReqResv            | 是否仅允许在预留资源中运行                                   |
| RootOnly           | 是否仅允许root用户提交作业                                   |
| ~~Shared~~         | 同OverSubscribe（已重命名）                                  |
| State              | 分区状态                                                     |
| TRESBillingWeights | 定义每种TRES类型的计费权重，用于计算作业的使用情况           |