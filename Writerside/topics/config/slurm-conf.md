# slurm.conf


| 参数                          | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| AccountingStorageBackupHost   | 记账信息存储数据库的备份主机的名称，仅在使用 SlurmDBD 的系统中使用，其他情况下将被忽略 |
| AccountingStorageEnforce      | 作业提交限制策略：<br/>-- all: 添加除 nojobs 和 nosteps 限制外的其他所有限制<br/>-- associations: 要求所有作业必须指定正确的关联<br/>-- limits: 隐藏启用关联和QOS限制（不会阻止作业提交）<br/>-- nojobs: Slurm不会记录任务作业或步骤<br/>-- nosteps: Slurm不会记录任务步骤<br/>-- qos: 要求所有作业必须指定正确的 QOS (服务质量)<br/>-- safe: 作业不会因限制而被终止<br/>-- wckeys: 阻止用户使用无权访问的 wckey 运行作业 |
| AccountingStorageExternalHost | 外部 slurmdbd 的列表，使用逗号分隔，如果未提供端口，将使用 AccountingStoragePort。这允许注册到外部 slurmdbd 的集群 |
| AccountingStorageHost         | 记账信息存储数据库的主机名称，仅在使用 SlurmDBD 的系统中使用，其他情况下将被忽略 |
| AccountingStorageParameters   | 记账信息存储数据库选项，使用逗号分隔                         |
| AccountingStoragePass         | 记账信息存储数据库的密码                                     |
| AccountingStoragePort         | 记账信息存储数据库的监听端口。默认值为 SLURMDBD_PORT，通常设置为 6819 |
| AccountingStorageTRES         | 要在集群上跟踪的资源的列表，包括 GRES、CPU、内存等，默认包括计费、CPU、能源、内存等 |
| AccountingStorageType         | 记账信息存储类型。目前可接受的值为 "accounting_storage/slurmdbd" |
| AccountingStorageUser         | 记账信息存储数据库的用户                                     |
| AccountingStoreFlags          | 用于修改发送到记账信息存储数据库的字段，选项包括： --  job_comment -- job_env -- job_extra -- job_script -- no_stdio |
| AcctGatherNodeFreq            | AcctGather 插件的节点记账信息采样间隔，默认值为零（禁用）。  |
| AcctGatherEnergyType          | 用于能源消耗记账信息的插件标识，可配置选项包括 acct_gather_energy/gpu、acct_gather_energy/ipmi 等。 |
| AcctGatherInterconnectType    | 用于互连网络流量记账信息的插件标识。可配置选项包括 acct_gather_interconnect/ofed 和 acct_gather_interconnect/sysfs |
| AcctGatherFilesystemType      | 用于文件系统流量记账信息的插件标识。可配置选项包括 acct_gather_filesystem/lustre |
| AcctGatherProfileType         | 用于详细作业分析的插件标识。可配置选项包括 acct_gather_profile/hdf5 和 acct_gather_profile/influxdb |
| AllowSpecResourcesUsage       | 如果设置为 "YES"，允许作业覆盖节点配置的 CoreSpecCount 值    |
| AuthAltTypes                  | slurmctld 用于通信的认证插件，可接受的值包括 auth/jwt        |
| AuthAltParameters             | 定义认证插件选项                                             |
| AuthInfo                      | 用于 Slurm 守护进程（slurmctld 和 slurmd）与 Slurm 客户端之间通信认证的附加信息 |
| AuthType                      | Slurm 组件之间通信的认证方法。所有 Slurm 守护进程和命令在更改 AuthType 的值之前必须终止，并在之后重新启动。更改此值会中断未完成的作业步骤。可接受的值包括 auth/munge 和 auth/slurm |
| BackupAddr                    | 已弃用的选项，请参见 SlurmctldHost                           |
| BackupController              | 已弃用的选项，请参见 SlurmctldHost                           |
| BatchStartTimeout             | 批处理作业被允许启动的最大时间（以秒为单位），超出此时间将被视为缺失并释放分配。默认值为 10 秒 |
| BcastExclude                  | 在自动检测和广播可执行共享对象依赖项时要排除的绝对目录路径，默认值为 `/lib`,`/usr/lib`,`/lib64`,`/usr/lib64` |
| BcastParameters               | 控制 sbcast 和 srun --bcast 行为 -- DestDir：广播到分配的计算节点的文件的目标目录。默认值为当前工作目录 -- Compression：指定要使用的默认文件压缩库。支持的值为`lz4`和`none` -- send_libs：如果设置，则尝试自动检测并将可执行文件的共享对象依赖项广播到分配的计算节点。文件与可执行文件一起放在一个目录中 |
| BurstBufferType               | 管理突发缓冲区的插件 -- burst_buffer/datawarp：使用 Cray DataWarp API 提供突发缓冲功能 -- burst_buffer/lua：此插件提供由 Lua 脚本定义的 API 挂钩 -- burst_buffer/none：无 |
| CliFilterPlugins              | 逗命令行接口选项过滤/修改插件，指定的插件将按照列出的顺序执行 -- cli_filter/lua：允许您使用 lua 编写自己的 cli_filter 实现 -- cli_filter/syslog：启用作业提交活动的日志记录 -- cli_filter/user_defaults：查找文件 $HOME/.slurm/defaults 并读取每一行作为 key=value 对，其中 key 是 salloc/sbatch/srun 可用的任何作业提交选项，value 是用户定义的默认值 |
| ClusterName                   | 此 Slurm 管理集群的名称，建议使用小写名称                    |
| CommunicationParameters       | 用于标识通信选项 -- block_null_hash：要求所有 Slurm 认证令牌包含较新（20.11.9 和 21.08.8）有效负载 -- DisableIPv4：禁用所有 Slurm 守护进程的 IPv4 仅操作（除 slurmdbd 外） -- EnableIPv6：启用所有 Slurm 守护进程使用 IPv6 地址（除 slurmdbd 外） -- getnameinfo_cache_timeout：控制 slurmctld 保留 IP 到主机名解析的时间（秒）。默认值为 60，设置为 0 则禁用缓存 -- keepaliveinterval：指定空闲连接的保活探测间隔（秒），此设置影响 srun 与 slurmstepd 及 slurmdbd 之间的连接，默认使用系统设置 -- keepaliveprobes：指定在连接断开之前发送的未确认保活探测数量。此设置影响 srun 与 slurmstepd 及 slurmdbd 之间的连接，默认使用系统设置 -- keepalivetime：指定连接标记为需要保活探测的时间（秒）。此设置影响 srun 与 slurmstepd 及 slurmdbd 之间的连接。较长的值可提高网络故障时的通信可靠性，默认禁用保活 -- NoCtldInAddrAny：直接绑定到运行 slurmctld 的节点解析的地址，而不是绑定到节点的任意地址 -- NoInAddrAny：直接绑定到节点解析的地址，适用于所有守护进程/客户端（除 slurmctld 外） |
| CompleteWait                  | 当任何作业处于 COMPLETING 状态时等待的时间（以秒为单位），然后再调度其他作业。这是为了尽量保持在最近使用的节点上的作业，目标是防止资源碎片。如果设置为零，则待处理作业将尽快启动。由于 COMPLETING 作业的资源在每个节点的 Epilog 完成后会立即释放供其他作业使用，因此可能导致非常碎片化的资源分配。为了给作业提供最小的响应时间，建议设置为零（不等待）。为了最小化资源的碎片化，**建议将其值设置为 KillWait 加 2**。在这种情况下，设置 KillWait 为小值可能是有益的。CompleteWait 的默认值为零秒。值不得超过 65533 |
| ControlAddr                   | 已弃用选项，请参见 SlurmctldHost                             |
| ControlMachine                | 已弃用选项，请参见 SlurmctldHost                             |
| CpuFreqDef                    | 运行作业步骤时默认使用的 CPU 调节器，默认使用系统默认设置。如果未指定 --cpu-freq 选项，则不进行调节器设置尝试 -- Conservative：尝试使用 Conservative CPU 调节器。 -- OnDemand：尝试使用 OnDemand CPU 调节器。 -- Performance：尝试使用 Performance CPU 调节器。 -- PowerSave：尝试使用 PowerSave CPU 调节器 |
| CpuFreqGovernors              | 允许通过 salloc、sbatch 或 srun 选项 --cpu-freq 设置的 CPU 频率调节器列表，默认为OnDemand、Performance 、UserSpace -- Conservative：尝试使用 Conservative CPU 调节器。 -- OnDemand：尝试使用 OnDemand CPU 调节器（默认值） -- Performance：尝试使用 Performance CPU 调节器（默认值） -- PowerSave：尝试使用 PowerSave CPU 调节器 -- SchedUtil：尝试使用 SchedUtil CPU 调节器。 -- UserSpace：尝试使用 UserSpace CPU 调节器（默认值） -- Conservative：尝试使用 Conservative CPU 调节器。 -- OnDemand：尝试使用 OnDemand CPU 调节器（默认值） -- Performance：尝试使用 Performance CPU 调节器（默认值） -- PowerSave：尝试使用 PowerSave CPU 调节器 -- SchedUtil：尝试使用 SchedUtil CPU 调节器 -- UserSpace：尝试使用 UserSpace CPU 调节器（默认值） |
| CredType                      | 创建作业步骤凭证时使用的加密签名工具 -- cred/munge：指示使用 Munge，默认 -- cred/slurm：使用 Slurm 的内部凭证格式 |
| DebugFlags                    | 定义应提供更详细事件日志记录的特定子系统。大多数 DebugFlags 将在 SlurmctldDebug 设置为 'verbose' 或更高时生成额外的日志消息。更多的日志可能会影响性能 -- Accrue：记录计数器记账细节 -- Agent：RPC 代理（来自 Slurm 守护进程的出站 RPC） -- AuditRPCs：对于所有进入 slurmctld 的 RPC，在处理连接之前打印发起地址、认证用户和 RPC 类型 -- Backfill：回填调度器详细信息 -- BackfillMap：回填调度器的详细日志，记录时间内保留资源的非常详细映射。与 Backfill 结合使用以获取回填调度器工作的详细和完整视图 -- BurstBuffer：突发缓冲区插件 -- Cgroup：Cgroup 详细信息 -- CPU_Bind：作业和步骤的 CPU 绑定详细信息 -- CpuFrequency：使用 --cpu-freq 选项的作业和步骤的 CPU 频率详细信息 -- Data：通用数据结构详细信息 -- DBD_Agent：RPC 代理（出站 RPC 到 DBD） -- Dependency：作业依赖调试信息 -- Elasticsearch：Elasticsearch 调试信息（已弃用）。作业完成的别名 -- Energy：AcctGatherEnergy 调试信息 -- Federation：联合调度调试信息 -- FrontEnd：前端节点详细信息 -- Gres：通用资源详细信息 -- Hetjob：异构作业详细信息 -- Gang：帮派调度详细信息 -- GLOB_SILENCE：在配置文件中不显示 glob "*" 符号的错误消息 -- JobAccountGather：常见作业账户收集详细信息（非插件特定） -- JobComp：作业完成插件详细信息 -- JobContainer：作业容器插件详细信息 -- License：许可证管理详细信息 -- Network：网络详细信息。警告：激活此标志可能导致记录密码、令牌或其他认证凭证 -- NetworkRaw：转_dump 关键网络通信的原始十六进制值。警告：此标志将导致非常详细的日志，并可能导致记录密码、令牌或其他认证凭证 -- NodeFeatures：节点特性插件调试信息 -- NO_CONF_HASH：当 slurm.conf 文件在 Slurm 守护进程之间不同时时，不记录 -- Power：电源管理插件和电源节省（挂起/恢复程序）详细信息 -- Priority：作业优先级 -- Profile：AcctGatherProfile 插件详细信息 -- Protocol：通信协议详细信息 -- Reservation：高级预留 -- Route：消息转发调试信息 -- Script：与 Slurm 调用的任何脚本相关的调试信息。这包括 slurmctld 执行的脚本，例如 PrologSlurmctld 和 EpilogSlurmctld -- SelectType：资源选择插件 -- Steps：slurmctld 的作业步骤资源分配 -- Switch：交换机插件 -- TLS：TLS 插件 -- TraceJobs：追踪 slurmctld 中的作业。将打印详细的作业信息，包括状态、作业 ID 和分配节点计数 -- Triggers：slurmctld 触发器 -- WorkQueue：工作队列详细信息 |
| DefCpuPerGPU                  | 每个分配的 GPU 分配的默认 CPU 数量。如果作业未指定 --cpus-per-task 和 --cpus-per-gpu，则使用此值。 |
| DefMemPerCPU                  | 每个可用分配的 CPU 默认可用的实际内存大小（以 MB 为单位）    |
| DefMemPerGPU                  | 每个分配的 GPU 默认可用的实际内存大小（以 MB 为单位），默认值为 0（无限制） |
| DefMemPerNode                 | 每个分配的节点默认可用的实际内存大小（以 MB 为单位），默认值为 0（无限制） |
| DependencyParameters          | 依赖参数选项 -- disable_remote_singleton：默认情况下，当一个联邦作业有单例依赖时，联邦中的每个集群必须清除单例依赖才能满足作业的单例依赖。启用此选项意味着只有原始集群必须清除单例依赖。此选项必须在联邦中的每个集群中设置 -- kill_invalid_depend：如果作业有无效依赖且永远无法运行，终止它并将其状态设置为 job_cancelled。默认情况下，作业保持待处理状态，原因是 dependency_never_satisfied -- max_depend_depth：测试循环作业依赖的最大作业数。在测试此数量的作业依赖后停止测试。默认值为 10 个作业 |
| DisableRootJobs               | 如果设置为 `YES`，则用户 root 将被禁止运行任何作业。默认值为 `NO`，意味着用户 root 可以执行作业。DisableRootJobs 也可以按分区设置 |
| EioTimeout                    | srun 等待 slurmstepd 关闭用于中继用户应用程序与 srun 之间的数据的 TCP/IP 连接的秒数。默认值为 60 秒。不得超过 65533 |
| EnforcePartLimits             | 如果设置为 `ALL`，则超出分区大小和/或时间限制的作业将在提交时被拒绝。如果作业提交到多个分区，则作业必须满足所有请求分区的限制。如果设置为 `NO`，则作业将被接受并保持在队列中，直到更改分区限制（时间和节点限制）。如果设置为 `ANY`，则作业必须满足任何请求分区以提交。默认值为 `NO` |
| Epilog                        | 用户作业完成时在每个节点上作为用户 root 执行的脚本的路径名（例如 "/usr/local/slurm/epilog"）。如果不是绝对路径名，将在 slurm.conf 文件相同目录中搜索。可以使用 glob 模式运行多个 epilog 脚本。默认没有 epilog |
| EpilogMsgTime                 | slurmctld 守护进程处理来自 slurmd 守护进程的 epilog 完成消息所需的微秒数。默认值为 2000 微秒 |
| EpilogSlurmctld               | slurmctld 在作业分配终止时执行的程序的全路径名（例如 "/usr/local/slurm/epilog_controller"） |
| FairShareDampeningFactor      | 减少超过用户或组的公平份额分配资源的影响。默认值为 1         |
| FederationParameters          | 用于定义联合选项 -- fed_display：如果设置，则客户端状态命令将默认以联合视图显示信息 |
| FirstJobId                    | 提交给 Slurm 的第一个作业使用的作业 ID。默认值为 1           |
| GetEnvTimeout                 | 控制作业在尝试从缓存文件加载用户环境之前等待的时间（秒）。默认值为 2 秒 |
| GresTypes                     | 要管理的通用资源的逗号分隔列表（例如 GresTypes=gpu,mps）     |
| GroupUpdateForce              | 如果设置为非零值，则即使 /etc/group 文件没有更改，也会定期更新有关哪些用户是允许使用分区的组的成员的信息 |
| GroupUpdateTime               | 控制更新有关哪些用户是允许使用分区的组的成员的信息的频率。默认值为 600 秒 |
| GpuFreqDef                    | 默认 GPU 频率，用于运行作业步骤时 -- low：可能的最低频率 -- medium：尝试将频率设置在可用范围的中间  -- high：可能的最高频率  -- highm1：（高减一）将选择下一个最高可用频率 |
| HashPlugin                    | 确定用于网络通信的哈希插件类型 -- hash/k12：使用 KangorooTwelve 加密哈希函数生成哈希（默认值） -- hash/sha3：使用 SHA-3 加密哈希函数生成哈希 |
| HealthCheckInterval           | HealthCheckProgram 执行之间的时间间隔（秒）。默认值为零，表示禁用执行 |
| HealthCheckNodeState          | 确定哪些节点状态应执行 HealthCheckProgram。多个状态值可以用逗号分隔 |
| HealthCheckProgram            | 定期在所有未处于 NOT_RESPONDING 状态的计算节点上作为用户 root 执行的脚本的全路径名 |
| InactiveLimit                 | 非响应作业分配命令（例如 srun 或 salloc）在多长时间后会导致作业被终止的时间间隔（秒） |
| InteractiveStepOptions        | 启用时，启动 salloc 将自动启动一个 srun 进程，并使用 InteractiveStepOptions 启动节点上的终端 |
| JobAcctGatherType             | 作业记账数据收集方式<br/>-- jobacct_gather/cgroup (推荐)：使用cgroups插件收集统计信息<br/>-- jobacct_gather/linux：使用Linux内核的进程统计功能收集统计信息<br/>-- jobacct_gather/none：不使用作业记账功能 |
| JobAcctGatherFrequency        | 作业记账数据收集频率（秒），默认 30 秒                       |
| JobAcctGatherParams           | JobAcctGather 插件的参数 -- NoShared：排除共享内存的 RSS。此选项不能与 UsePSS 一起使用。仅与 jobacct_gather/linux 插件兼容 -- UsePss：使用 PSS 值而不是 RSS 来计算实际的内存使用情况。PSS 值将作为 RSS 保存。此选项不能与 NoShared 一起使用。仅与 jobacct_gather/linux 插件兼容 -- OverMemoryKill：每次通过 JobAcctGather 插件收集会计信息时，杀死被检测到使用超过请求内存的步骤中的进程。此参数应谨慎使用，因为超出内存分配的作业可能会影响其他进程和/或机器健康 -- DisableGPUAcct：不进行 GPU 使用的会计，并跳过任何 GPU 驱动程序库调用。此参数可以帮助提高性能，尤其是在 GPU 驱动程序响应缓慢时 |
| JobCompHost                   | 执行作业完成数据库的机器名称。仅用于数据库类型存储插件       |
| JobCompLoc                    | 此选项根据 JobCompType 设置 -- jobcomp/elasticsearch：将完成的作业记录信息发送到 Elasticsearch 服务器 URL -- jobcomp/filetxt：将完成的作业记录信息发送到配置的文件 -- jobcomp/kafka：将完成的作业记录信息发送到 Kafka 服务器 -- jobcomp/lua：将完成的作业记录信息由jobcomp.lua脚本处理 -- jobcomp/mysql：将完成的作业记录信息写入 MySQL 数据库 -- jobcomp/script：将完成的作业记录信息由此选项配置名称的脚本处理 |
| JobCompParams                 | 作业完成插件参数 -- flush_timeout：最大时间（毫秒）以等待所有未完成的生产请求等完成，默认值为 500 毫秒 -- poll_interval：调用 librdkafka API poll 函数之间的秒数，默认值为 2 秒 -- requeue_on_msg_timeout：指示交付报告回调重新排队未成功交付的消息 -- topic：目标 Kafka 的topic以发送消息，默认值为 ClusterName |
| JobCompPass                   | 用于访问存储作业完成数据的数据库的密码。仅用于数据库类型存储插件 |
| JobCompPort                   | 作业完成数据库服务器的监听端口。仅用于数据库类型存储插件     |
| JobCompType                   | 作业完成日志机制类型 -- jobcomp/none：作业完成后，作业记录将从系统中清除 -- jobcomp/elasticsearch：作业完成后，作业记录写入指定的 Elasticsearch 服务器，地址由 JobCompLoc 参数指定 -- jobcomp/filetxt：作业完成后，作业记录应写入指定的文本文件，由 JobCompLoc 参数指定 -- jobcomp/kafka：作业完成后，作业记录应发送到 Kafka 服务器，地址由 JobCompLoc 中引用的文件路径和/或其他 JobCompParams 指定 -- jobcomp/lua：作业完成后，作业记录应由位于默认脚本目录中的 jobcomp.lua 脚本处理 -- jobcomp/mysql：作业完成后，作业记录应写入指定的 MySQL 或 MariaDB 数据库，由 JobCompLoc 参数指定 -- jobcomp/script：作业完成后，将执行指定的脚本（由 JobCompLoc 参数指定），并提供作业信息的环境变量 |
| JobCompUser                   | 访问作业完成数据库的用户帐户。仅用于数据库类型存储插件       |
| JobContainerType              | 标识用于通过 Linux 命名空间进行作业隔离的插件 -- job_container/tmpfs：用于在文件系统上为作业创建一个私有命名空间，其中包含每个作业的临时文件系统（/tmp和/dev/shm）。必须设置`PrologFlags=Contain`才能使用此插件 |
| JobFileAppend                 | 控制作业输出或错误文件在作业开始时存在时的处理方式。设置为 1 时，追加到现有文件。默认情况下，任何现有文件都会被截断 |
| JobRequeue                    | 控制批处理作业的默认重排能力。设置为 1 时，允许批处理作业被重排 |
| JobSubmitPlugins              | 旨在站点特定的插件，可用于设置默认作业参数和/或记录事件      |
| KillOnBadExit                 | 如果设置为 1，当任何任务崩溃或中止时，步骤将立即终止         |
| KillWait                      | 作业的进程在达到时间限制时，SIGTERM 和 SIGKILL 信号之间的间隔，默认为 30 秒 |
| MaxBatchRequeue               | 批处理作业在标记为 JobHeldAdmin 之前可以自动重排的最大次数   |
| NodeFeaturesPlugins           | 用于支持节点特征的插件，这些特征可能随时间变化 -- node_features/knl_cray：仅用于 Cray 系统上的 Intel Knights Landing 处理器 (KNL) -- node_features/knl_generic：用于通用 Linux 系统上的 Intel Knights Landing 处理器 (KNL) -- node_features/helpers：用于通过任意脚本或程序报告和修改节点的特性 |
| LaunchParameters              | 标识作业启动插件的参数配置 -- batch_step_set_cpu_freq：根据给定的 --cpu-freq 或 slurm.conf 中的 CpuFreqDef 选项为批处理步骤设置 CPU 频率。默认情况下，仅使用 srun 启动的步骤会利用 CPU 频率设置选项 -- cray_net_exclusive：允许 Cray XC 集群上的作业独占网络资源。此选项仅应在提供每个节点一次仅对单个作业提供独占访问的集群上设置，并且不应在作业内使用并行步骤，否则可能会导致节点资源超分配 -- enable_nss_slurm：允许通过 slurmstepd 为作业提供 passwd 和 group 解析，而无需从基于网络的服务中查找 -- lustre_no_flush：如果在 Cray XC 集群上设置，则在作业步骤完成时不刷新 Lustre 缓存。此设置将在重新配置后生效，仅适用于新启动的作业 -- mem_sort：在步骤启动时对 NUMA 内存进行排序。用户可以通过 SLURM_MEM_BIND 环境变量或 `--mem-bind=nosort` 命令行选项覆盖此默认设置 -- mpir_use_nodeaddr：启动任务时，Slurm 会在 MPIR_proctable 中创建条目，以供并行调试器、分析器和相关工具附加到正在运行的进程。默认情况下，MPIR_procdesc 结构中的 host_name 设置为 NodeName。如果指定此选项，将在此上下文中使用 NodeAddr -- disable_send_gids：默认情况下，slurmctld 会查找并发送作业的 user_name 和扩展 GIDs，而不是在每个节点上独立进行查找。这有助于缓解在涉及许多节点的作业启动时的名称服务可扩展性问题。使用此选项将禁用此功能。如果指定了 enable_nss_slurm，则忽略此选项 -- slurmstepd_memlock：将 slurmstepd 进程当前的内存锁定在 RAM 中。 -- slurmstepd_memlock_all：将 slurmstepd 进程当前和未来的内存锁定在 RAM 中。 -- test_exec	在尝试在步骤中的节点上启动可执行程序之前，让 srun 验证该程序的存在以及用户的执行权限。 -- use_interactive_step：让 salloc 使用交互步骤在分配的计算节点上启动 shell，而不是在调用 salloc 的本地位置。这是通过使用交互步骤选项启动 srun 命令来实现的。调用时带有命令参数的 salloc 不受此影响。 -- ulimit_pam_adopt：当使用 pam_slurm_adopt 将外部进程加入作业 cgroup 时，会设置 RLIMIT_RSS，就像在常规步骤中运行的任务一样 |
| Licenses                      | 规范可分配给作业的许可证（或其他资源）。许可证名称后可以跟冒号和计数。 |
| LogTimeFormat                 | slurmctld 和 slurmd 日志文件中时间戳的格式。可以配置：`iso8601`、`iso8601_ms`、`rfc5424`、`rfc5424_ms`、`rfc3339`、`clock`、`short` 和 `thread_id`。默认值为 `iso8601_ms` |
| MailDomain                    | 用于限定用户名的域名，如果未通过 `--mail-user` 选项显式给出电子邮件地址。未设置时，本地 MTA 需要自行限定本地地址。对 MailDomain 的更改只会影响新作业 |
| MailProg                      | 用于发送用户请求的电子邮件的程序的完全合格路径名。默认值为 `/bin/mail`（如果 `/bin/mail` 不存在但 `/usr/bin/mail` 存在，则为 `/usr/bin/mail`）。程序会用适合默认邮件命令的参数调用，但会以环境变量的形式传递关于作业的额外信息 |
| MaxArraySize                  | 作业数组任务的最大索引值，最大值为 `MaxArraySize` 的值减一，以允许索引值为零。配置 `MaxArraySize` 为 0 以禁用作业数组使用。该值不得超过 4000001。 `MaxJobCount` 的值应远大于 `MaxArraySize`。默认值为 1001 |
| MaxDBDMsgs                    | 当无法与 SlurmDBD 通信时，slurmctld将排队等待处理的消息，以便在 SlurmDBD 可用时处理。为了避免耗尽内存，slurmctld仅会排队一定数量的消息。默认值为 10000，或 `MaxJobCount * 2 + Node Count * 4` 中的较大者。该值不能少于 10000 |
| MaxJobCount                   | slurmctld一次性在内存中可以存在的最大作业数量。与 `MinJobAge` 结合使用，以确保 slurmctld 守护进程不会耗尽其内存或其他资源。一旦达到此限制，提交额外作业的请求将失败。默认值为 10000 个作业 |
| MaxJobId                      | 提交给 Slurm 的作业的最大作业 ID，未请求特定值的作业 ID。作业 ID 是无符号的 32 位整数，前 26 位保留用于本地作业 ID，剩余 6 位保留用于标识集群 ID。最大允许的本地作业 ID 为 67,108,863（0x3FFFFFF）。默认值为 67,043,328（0x03ff0000） |
| MaxMemPerCPU                  | 每个分配的 CPU 可用的最大实际内存大小（以 MB 为单位）。用于避免内存超分配和导致分页。默认值为 0（无限） |
| MaxMemPerNode                 | 在作业分配中每个分配的节点可用的最大实际内存大小（以 MB 为单位）。默认值为 0（无限） |
| MaxNodeCount                  | 控制器中可能存在的节点的最大计数。默认情况下，`MaxNodeCount` 将设置为在 `slurm.conf` 中找到的节点数。如果小于在 `slurm.conf` 中找到的节点数，则将忽略 `MaxNodeCount` |
| MaxStepCount                  | 任何作业可以发起的最大步骤数。此参数旨在限制坏批处理脚本的影响。默认值为 40000 步 |
| MaxTasksPerNode               | Slurm 允许作业步骤在单个节点上生成的最大任务数。默认值为 512。不得超过 65533 |
| MCSParameters                 | MCS = 多类别安全 MCS 插件参数。支持的参数特定于 `MCSPlugin`。对该值的更改在 Slurm 守护进程重新配置时生效 |
| MCSPlugin                     | MCS = 多类别安全：将安全标签与作业关联，并确保节点只能在使用相同安全标签的作业之间共享 -- mcs/none：默认值。没有与作业关联的安全标签，在作业之间共享节点时没有特定的安全限制 -- mcs/account：只有同一账户的用户可以共享节点（需要启用计费功能） -- mcs/group：只有同一组的用户可以共享节点 -- mcs/user：节点不能与其他用户共享 |
| MessageTimeout                | 允许完成通信的往返时间（以秒为单位）。默认值为 10 秒。对于共享节点的系统，slurmd 守护进程可能被分页出并需要更高的值 |
| MinJobAge                     | 完成作业的记录在 slurmctld 内存中清除前的最小年龄。默认值为 300 秒。零值会阻止任何作业记录清除 |
| MpiDefault                    | 标识要使用的默认 MPI 类型。当前支持的版本包括：pmi2、pmix 和 none（默认，适用于许多其他版本的 MPI） |
| MpiParams                     | MPI 相关参数。多个参数可以用逗号分隔。当前支持的参数包括：`ports=#-#` 和 `disable_slurm_hydra_bootstrap` |
| OverTimeLimit                 | 作业可以超过其时间限制的分钟数。默认值为零。不得超过 65533 分钟。支持值 `UNLIMITED` |
| PluginDir                     | 确定查找 Slurm 插件的目录位置。默认值为配置时给出的前缀 + `/lib/slurm` |
| PlugStackConfig               | Slurm 堆叠插件的配置文件位置，默认位置为 `plugstack.conf`    |
| PreemptMode                   | 用于抢占作业或启用班级调度的机制 -- OFF：默认值，禁用作业抢占和帮调度。仅与 PreemptType=preempt/none 兼容。常见用法是在分区上设置此参数以禁用该分区的抢占 -- CANCEL：被抢占的作业将被取消。 -- GANG：启用同一分区内作业的帮调度（时间切片），并允许恢复挂起的作业。必须在集群级别指定 GANG 选项。注意，帮调度独立于每个分区执行 -- REQUEUE：通过重新排队（如果可能）或取消作业来抢占作业。为重新排队的作业必须设置 --requeue sbatch 选项或在 slurm.conf 中设置集群范围的 JobRequeue 参数为 1 -- SUSPEND：被抢占的作业将被挂起，稍后帮调度程序将恢复它们。需要在集群级别指定 GANG 选项。挂起的作业仍将使用已分配节点上的内存 -- WITHIN：对于 PreemptType=preempt/qos，允许同一 qos 内的作业相互抢占。建议仅在系统 qos 值的相关子集上直接设置 |
| PreemptParameters             | 抢占作业参数 -- min_exempt_priority：作业全局优先级的阈值。只有优先级低于此值的作业将被标记为可抢占 -- reclaim_licenses：如果设置，则可以抢占作业以回收许可证。否则，请求忙碌许可证的作业将不得不等待，即使它们具有抢占优先权。此选项的逻辑仅在 select/cons_tres 插件中可用 -- reorder_count：指定在重新排序可抢占作业时应尝试的次数，以最小化被抢占作业的数量。默认值为 1。高值可能对性能产生不利影响。此选项的逻辑仅在 select/cons_tres 插件中可用 -- send_user_signal：在抢占时发送用户信号（例如 --signal=<sig_num>），即使信号时间尚未到达。在宽限期抢占的情况下，如果用户信号已指定且未发送，则将发送用户信号，否则将发送 SIGTERM 给任务 -- strict_order：如果设置，则执行额外的逻辑，尝试仅抢占优先级最低的作业。当存在多个可抢占作业的优先级时，可能希望设置此配置参数。此选项的逻辑仅在 select/cons_tres 插件中可用 -- suspend_grace_time：指定在使用 PreemptMode=SUSPEND 时的抢占宽限时间（单位为秒）。当作业被挂起时，将发送 SIGTSTP 信号，等待指定的挂起宽限时间后，将发送 SIGSTOP 信号。默认值为 2 秒 -- youngest_first：如果设置，则抢占排序算法将根据作业的开始时间进行排序，以优先抢占较新的作业而不是较旧的作业。（需要 preempt/partition_prio 或 preempt/qos 插件） |
| PreemptType                   | 指定用于识别可以被抢占的作业的插件 -- preempt/none：禁用作业抢占。这是默认设置 -- preempt/partition_prio：作业抢占基于分区的优先级层级（PriorityTier）。高优先级层级分区中的作业可以抢占低优先级层级分区中的作业。此选项与 PreemptMode=OFF 不兼容 -- preempt/qos：作业抢占规则由 Slurm 数据库中的服务质量（Quality Of Service，QOS）规格指定。在 PreemptMode=SUSPEND 的情况下，抢占作业必须提交到具有更高优先级层级的分区或相同的分区。提交到相同的分区也是支持的，这会导致抢占者的 QoS 与被抢占者的 QoS 进行协同调度。此选项与 PreemptMode=OFF 不兼容。PreemptMode=SUSPEND 的配置仅支持 SelectType=select/cons_tres 插件 |
| PreemptExemptTime             | 全局选项，设置所有作业在被考虑抢占之前的最小运行时间。任何 QOS 的 PreemptExemptTime 优先于全局选项。仅在 PreemptMode=REQUEUE 和 PreemptMode=CANCEL 时生效。-1 表示禁用此选项，0 等效于禁用。接受的时间格式包括：`minutes`, `minutes:seconds`, `hours:minutes:seconds`, `days-hours`, `days-hours:minutes`, `days-hours:minutes:seconds` |
| PrEpParameters                | 要传递给 PrEpPlugins 的参数                                  |
| PrEpPlugins                   | 供程序员编写 Prolog 和 Epilog（PrEp）脚本的插件资源。默认且当前唯一实现的插件是 prep/script。可以指定额外插件的逗号分隔列表 |
| PriorityCalcPeriod            | 半衰期衰减重新计算的时间间隔（分钟）。仅在 PriorityType=priority/multifactor 时适用。默认值为 5（分钟） |
| PriorityDecayHalfLife         | 控制在确定用户、账户和集群的优先级时，考虑过去资源使用的时间长度。使用记录会随时间衰减，衰减半衰期为 PriorityDecayHalfLife。如果设置为 0，则不应用衰减。此选项仅在 PriorityType=priority/multifactor 时适用。默认值为 7-0（7 天） |
| PriorityFavorSmall            | 指定小作业应优先获得调度优先权。仅在 PriorityType=priority/multifactor 时适用。支持的值为`YES`和`NO`。默认值为`NO` |
| PriorityFlags                 | 修改优先级行为的标志。仅在 PriorityType=priority/multifactor 时适用 -- ACCRUE_ALWAYS：如果设置，优先级年龄因子将增加，尽管作业因依赖、暂停或未来开始时间而不合格。累积限制将被忽略 -- CALCULATE_RUNNING：如果设置，将不仅为待处理作业重新计算优先级，还将为正在运行和暂停的作业重新计算优先级 -- DEPTH_OBLIVIOUS：如果设置，优先级将基于正常的多因素计算进行计算，但树中关联的深度不会对其优先级产生不利影响。此选项会自动启用 NO_FAIR_TREE -- NO_FAIR_TREE：禁用“公平树”算法，恢复到“经典”公平共享优先级调度 -- INCR_ONLY：如果设置，优先级值将仅增加，作业优先级永远不会降低 -- MAX_TRES：如果设置，节点上的加权 TRES 值（例如 TRESBillingWeights）将被计算为节点上单个 TRES 的最大值（例如 cpus、mem、gres）加上所有全局 TRES 的总和（例如许可证） -- NO_NORMAL_ALL：如果设置，将设置所有 NO_NORMAL_* 标志 -- NO_NORMAL_ASSOC：如果设置，关联因子不会与最高关联优先级进行归一化 -- NO_NORMAL_PART：如果设置，分区因子不会与最高分区 PriorityJobFactor 进行归一化 -- NO_NORMAL_QOS：如果设置，QOS 因子不会与最高 qos 优先级进行归一化 -- NO_NORMAL_TRES：如果设置，TRES 因子不会与作业的分区 TRES 计数进行归一化 -- SMALL_RELATIVE_TO_TIME：如果设置，作业的大小组件将基于作业的大小与其时间限制的比值，而不仅仅是作业的大小 |
| PriorityMaxAge                | 指定作业年龄的最大值，超过此值的作业将获得相同的基于年龄的优先级。适用的单位为时间字符串。默认值为 7-0（7 天） |
| PriorityParameters            | PriorityType 插件参数配置                                    |
| PrioritySiteFactorParameters  | PrioritySiteFactorPlugin 插件参数配置                        |
| PrioritySiteFactorPlugin      | 指定一个可选插件，与`priority`/`multifactor`一起使用，旨在初始设置并持续更新 SiteFactor 优先级因子。默认值为`site_factor`/`none` |
| PriorityType                  | 指定作业调度优先级的类型<br/> -- priority/basic：作业按先到先服务（FIFO）方式进行评估<br/>-- priority/multifactor 作业优先级由<a href="priority.md#multifactor-plugin">多因子插件</a>综合决定 |
| PriorityUsageResetPeriod      | 在此间隔内，关联的使用情况将重置为 0。此选项用于强制执行每个关联的时间使用硬限制 -- NONE：从不清除历史使用（默认值） -- NOW：立即清除历史使用。启动和重新配置时执行 -- DAILY：每天午夜清除 -- WEEKLY：每周日的 00:00 清除 -- MONTHLY：每月第一天的 00:00 清除 -- QUARTERLY：每季度第一天的 00:00 清除 -- YEARLY：每年第一天的 00:00 清除 |
| PriorityWeightAge             | 设置队列等待时间组件对作业优先级贡献的程度的整数值。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightAssoc           | 设置关联组件对作业优先级贡献的程度的整数值。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightFairshare       | 设置公平分享组件对作业优先级贡献的程度的整数值。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightJobSize         | 设置作业大小组件对作业优先级贡献的程度的整数值。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightPartition       | 分区因子，由 priority/multifactor 插件用于计算作业优先级。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightQOS             | 设置服务质量组件对作业优先级贡献的程度的整数值。仅在 PriorityType=priority/multifactor 时适用。默认值为 0 |
| PriorityWeightTRES            | 逗号分隔的 TRES 类型和权重列表，设置每种 TRES 类型对作业优先级的贡献程度。默认值为 0 |
| PrivateData                   | 控制隐藏普通用户的信息类型。默认情况下，所有信息对所有用户可见 -- accounts：（非 SlurmDBD 记账）阻止用户查看任何账户定义，除非他们是该账户的协调人 -- events：阻止用户查看事件信息，除非他们具有操作员状态或更高权限 -- jobs：阻止用户查看属于其他用户的作业或作业步骤。 (非 SlurmDBD 会计) 只有当他们是关联的协调人时，才能查看作业记录 -- nodes：阻止用户查看节点状态信息 -- partitions：阻止用户查看分区状态信息 -- reservations：阻止普通用户查看他们无法使用的预留信息 -- usage：阻止用户查看其他用户的使用情况，这适用于 sshare。 (非 SlurmDBD 记账) 阻止用户查看其他用户的使用情况，这适用于 sreport -- users：（非 SlurmDBD 记账）阻止用户查看除自己以外的任何用户信息，同时使用户只能看到他们处理的关联信息协调人可以看到所有用户的关联信息，但在列出用户时只能看到自己 |
| ProctrackType                 | 标识用于作业步骤级别的进程跟踪的插件 -- proctrack/cgroup：使用 Linux cgroups 来限制和跟踪进程，并且是支持 cgroup 的系统的默认选项 -- proctrack/linuxproc：使用 Linux 进程树，通过父进程 ID 进行跟踪 -- proctrack/pgid：使用进程组 ID 进行跟踪。注意：这是 BSD 系列的默认选项 |
| Prolog                        | Prolog 的程序路径，用于 slurmd 在请求运行新作业分配的作业步骤时执行 |
| PrologEpilogTimeout           | Slurm 等待 Prolog 和 Epilog 的时间间隔（秒），在超时后终止它们。默认情况下，等待无限期 |
| PrologFlags                   | 控制 Prolog 行为的标志 -- Alloc：如果设置，Prolog 脚本将在作业分配时执行。默认情况下，Prolog 在任务启动之前执行。因此，当启动 salloc 时，不会执行 Prolog。此标志在 Cray 系统启用集群兼容模式时很有用 -- Contain：在作业分配时，使用 ProcTrack 插件在所有分配的计算节点上创建作业容器。此容器可用于未在 Slurm 控制下启动的用户进程 -- DeferBatch：如果设置，slurmctld 将等待所有分配节点上的 Prolog 完成后再发送批处理作业启动请求。仅使用 Alloc 标志时，slurmctld 会在作业分配中的第一个节点完成 Prolog 后立即启动批处理步骤 -- NoHold：如果设置，Alloc 标志也应设置。这将允许 salloc 在每个节点上的 Prolog 完成之前不被阻塞。当步骤到达 slurmd 时，阻塞将在任何执行发生之前发生。这是一种更快的工作方式。此标志不能与 Contain 或 X11 标志结合使用 -- ForceRequeueOnFail：当批处理作业由于 Prolog 失败而无法启动时，总是自动重新排队，即使作业请求不重新排队 -- RunInJob：使 Prolog/Epilog 在 extern slurmstepd 中运行。这将其包含在作业的进程之一中。如果配置了 cgroup，将包含在其中。设置 RunInJob 标志隐含地设置了 Contain 和 Alloc 标志 -- Serial：默认情况下，Prolog 和 Epilog 脚本在每个节点上并发运行。此标志强制这些脚本在每个节点内串行运行，但会显著降低每个节点的作业吞吐量 -- X11：启用 Slurm 内置的 X11 转发功能。这与 ProctrackType=proctrack/linuxproc 不兼容。设置 X11 标志隐含地启用 Contain 和 Alloc 标志 |
| PrologSlurmctld               | slurmctld 守护进程在授予新作业分配之前执行的程序的完整路径名 |
| PropagatePrioProcess          | 控制用户生成的任务的调度优先级（nice 值） -- 0：任务将继承 slurm 守护进程的调度优先级（默认值） -- 1：任务将继承提交它们的命令（例如：srun 或 sbatch）的调度优先级。除非作业由用户 root 提交，任务的调度优先级不会高于生成它们的 slurm 守护进程 -- 2：任务将继承提交它们的命令（例如：srun 或 sbatch）的调度优先级，但限制其 nice 值始终比 slurm 守护进程高一（即任务的调度优先级低于 slurm 守护进程） |
| PropagateResourceLimits       | 资源限制名称。slurmd 守护进程使用这些名称从提交节点的用户进程环境中获取相关的（软）限制值 -- ALL：列表中所有限制（默认） -- NONE：不列出任何限制 -- AS：进程的最大地址空间（虚拟内存） -- CORE：核心文件的最大大小 -- CPU：最大 CPU 时间 -- DATA：进程数据段的最大大小 -- FSIZE：创建文件的最大大小。如果用户将 FSIZE 设置为小于当前 slurmd.log 的大小，作业启动将失败并出现 `File size limit exceeded` 错误 -- MEMLOCK：可以锁定到内存中的最大大小 -- NOFILE：最大打开文件数 -- NPROC：可用的最大进程数 -- RSS：最大常驻集大小 -- STACK：最大栈大小 |
| PropagateResourceLimitsExcept | 资源限制名称排除列表。默认情况下，所有资源限制将被传播，除了出现在此列表中的限制 |
| RebootProgram                 | 在每个计算节点上执行的程序，以便重启该节点。当授权用户执行 `scontrol reboot` 命令或提交带有 `--reboot` 选项的作业后，将在每个节点空闲时调用该程序。重启后，节点将返回正常使用 |
| ReconfigFlags                 | 控制在发出 `scontrol reconfig` 命令时可能采取的各种操作的标志。当前选项包括： -- KeepPartInfo：保持分区状态的内存值 -- KeepPartState：仅保留当前状态值，重置其他动态更新的参数 -- KeepPowerSaveSettings：保持当前的节能设置 |
| RequeueExit                   | 启用自动重新排队对于以指定值退出的批处理作业。可通过逗号分隔多个退出代码或使用 `-` 分隔符指定数字范围。重新排队的作业将处于待处理状态并稍后重新调度 |
| RequeueExitHold               | 启用自动重新排队对于以指定值退出的批处理作业，这些作业在用户手动释放之前将被保留 |
| ResumeFailProgram             | 当节点未能在 ResumeTimeout 内恢复时执行的程序。参数将是失败节点的名称 |
| ResumeProgram                 | 当处于节能模式的节点被分配工作时执行的程序。该程序在节点恢复服务时被调用。如果 ResumeProgram 无法恢复节点，节点状态将设置为 DOWN。默认情况下不执行任何程序 |
| ResumeRate                    | 节能模式下节点恢复正常操作的速率，单位为每分钟的节点数。默认值为每分钟 300 个节点 |
| ResumeTimeout                 | 在发出节点恢复请求和节点实际可用之间允许的最大时间（秒）。超时未响应的节点将被标记为 DOWN。默认值为 60 秒。 |
| ResvEpilog                    | 在保留结束时执行的程序的全路径名。                           |
| ResvOverRun                   | 描述保留结束后允许运行的作业时间，单位为分钟，默认值为 0（立即杀死作业）。 |
| ResvProlog                    | 在保留开始时执行的程序的全路径名。                           |
| ReturnToService               | 控制 DOWN 节点何时返回服务 -- 0：节点将保持在 DOWN 状态，直到系统管理员显式更改其状态（默认值） -- 1：仅在由于非响应而设置为 DOWN 时，节点将在注册时可用 -- 2：任何原因下的 DOWN 节点在注册时可用 |
| SchedulerParameters           | -- allow_zero_lic：启用后，超出配置 licenses 数量的作业不会被拒绝<br/>-- assoc_limit_stop：启用后，如果作业由于关联限制而无法启动，那么将作业所在分区加入黑名单，不会尝试在该分区中启动任何低优先级的作业<br/>-- batch_sched_delay：批处理作业调度延迟时间（秒），默认值为 3 秒<br/>-- bb_array_stage_cnt：为突发缓冲资源分配提供的作业数组任务数量，默认值为 10<br/>-- bf_allow_magnetic_slot：允许使用回填策略时为作业创建插槽<br/>-- bf_busy_nodes：在调度延迟启动的作业时，优先选择正在使用的节点<br/>-- bf_continue：回填调度策略会定期释放锁<br/>-- bf_hetjob_immediate：立即尝试启动异构作业<br/>-- bf_hetjob_prio：异构作业组件排序策略<br/>-- bf_interval：回填调度间隔（秒），默认30秒<br/>-- bf_job_part_count_reserve：回填调度为每个分区预留资源的高优先级作业数量（默认0表示全部预留，抑制所有低优先级作业）<br/>-- bf_licenses：回填调度会跟踪 licenses 可用性<br/>-- bf_max_job_array_resv：回填调度为作业数组预留的最大任务数，默认值为 20<br/>-- bf_max_job_assoc：回填调度为每个用户关联使用的最大回填作业数，默认值为 0（无限制）<br/>-- bf_max_job_part：回填调度在每个分区的最大回填作业数，默认值为 0（无限制）<br/>-- bf_max_job_start：每次回填调度可以启动的最大作业数。默认值为 0（无限制）<br/>-- bf_max_job_test：尝试进行回填调度的最大作业数，默认值为 500<br/>-- bf_max_job_user：回填调度为每个用户使用的最大回填作业数，默认值为 0（无限制）<br/>-- bf_max_job_user_part：用户为每个分区尝试进行回填调度的最大作业数，默认值为 0（无限制）<br/>-- bf_max_time：回填调度运行最大时间（秒），默认值为 bf_interval<br/>-- bf_min_age_reserve：在作业等待并可运行的情况下，后备和主调度逻辑将不会保留资源 -- bf_min_prio_reserve：后备和主调度逻辑将不会保留资源，除非待处理作业的优先级等于或高于指定值 -- bf_node_space_size：后备节点空间表的大小 -- bf_one_resv_per_job：禁止为单个作业添加多个后备保留 -- bf_resolution：维护有关作业开始和结束时机的数据的秒数 -- bf_running_job_reserve：为正在运行的整个节点作业创建后备保留 -- bf_window：在考虑调度作业时向前看的分钟数。默认值为 1440（1 天） -- bf_window_linear：为了性能原因，后备调度器将减少对作业预计结束时间计算的精度 -- bf_yield_interval：后备调度器将在指定的微秒数内定期放弃锁 -- bf_yield_sleep：后备调度器将在指定的微秒数内定期放弃锁 -- build_queue_timeout：定义用于构建作业队列的最大时间 -- correspond_after_task_cnt：定义分割后的数组任务数量以进行潜在的依赖关系检查 -- default_queue_depth：当运行的作业完成或发生其他例行操作时，尝试调度的作业默认数量。默认值为 100 -- defer：设置此选项将避免在作业提交时逐个调度，而是推迟到稍后的时间 -- defer_batch：仅对批处理作业推迟调度 -- delay_boot：如果作业等待的时间少于指定的时间，则不重新启动节点 -- disable_job_shrink：拒绝用户请求缩小正在运行的作业 -- disable_hetjob_steps：禁用跨异构作业分配的作业步骤 -- enable_hetjob_steps：启用跨异构作业分配的作业步骤 -- enable_user_top：允许非特权用户使用 "scontrol top" 命令 -- extra_constraints：允许通过 salloc、sbatch 和 srun 的 --extra 选项进行节点过滤 -- Ignore_NUMA：抑制对 NUMA 节点的优化 -- ignore_prefer_validation：如果设置，则请求 --prefer 的任何特性在系统中创建无效请求时不会生成错误 -- max_array_tasks：指定作业数组中可以包含的最大任务数。默认限制为 MaxArraySize -- max_rpc_cnt：如果 slurmctld 守护进程中的活动线程数等于或大于此值，则推迟调度作业 -- max_sched_time：调度循环在退出前的执行时间（秒）。确保该值低于 MessageTimeout。默认为 MessageTimeout 的一半，最小 1 秒，最大 2 秒 -- max_script_size：批处理脚本的最大大小（字节）。默认值为 4 兆字节，较大值可能影响性能 -- max_submit_line_size：提交行的最大大小（字节）。默认为 1 兆字节，最大 2 兆字节 -- max_switch_wait：作业因期望交换计数延迟的最大秒数。默认 300 秒 -- no_backup_scheduling：备份控制器不会调度作业，但允许提交和修改作业 -- no_env_cache：启用后，环境加载失败的作业将失败，而非使用缓存 -- nohold_on_prolog_fail：Prolog 失败时作业重新排队但不被保留，以便调度到其他主机 -- pack_serial_at_end：将串行作业放在可用节点的末尾，减少资源碎片 -- partition_job_depth：每个分区尝试调度的默认作业数量。默认值为 0（无限制） -- reduce_completing_frag：控制在作业完成时的资源调度，减少潜在碎片。需与 CompleteWait 配合使用 -- requeue_setup_env_fail：作业环境设置失败时重新排队，并排空执行节点 -- salloc_wait_nodes：salloc 命令在所有节点准备好前等待 -- sbatch_wait_nodes：sbatch 脚本在所有节点准备好前等待 -- sched_interval：主调度循环执行的频率（秒）。默认 60 秒，-1 禁用循环 -- sched_max_job_start：主调度逻辑单次执行的最大作业数量。默认 0（无限制） -- sched_min_interval：主调度循环执行的最小时间间隔（微秒）。默认 2 微秒 -- spec_cores_first：专用核心从第一个插槽的第一个核心中选择 -- step_retry_count：步骤完成时重试的最少步骤数量。默认 8 步骤 -- step_retry_time：步骤完成后，重试待处理步骤的等待时间。默认 60 秒 -- time_min_as_soft_limit：将 --time-min 限制视为软时间限制，允许作业超时 -- whole_hetjob：请求对异构作业的所有组成部分进行操作 |
| SchedulerTimeSlice            | 每个时间片的秒数（启用团体调度时）。值在 5 到 65533 秒之间，默认 30 秒。 |
| SchedulerType                 | 调度器类型<br/>-- sched/backfill：后备调度，允许低优先级作业在不延误高优先级作业的情况下启动（**默认**） <br/>-- sched/builtin：FIFO 调度，按照优先级顺序启动作业 |
| ScronParameters               | 启用 scrontab 提交和管理周期性作业的选项 -- enable：启用使用 scrontab 提交和管理周期性作业 -- explicit_scancel：取消 scrontab 作业时，用户必须使用 --cron 标志显式请求取消作业 |
| SelectType                    | 资源选择模式<br/>-- select/linear：按整个节点分配<br/>-- select/cons_tres：按核心/内存/GPU等资源分配 |
| SelectTypeParameters          | 资源选择模式参数，取决于 SelectType 的参数选项<br/>SelectType=select/linear 仅支持 **CR_ONE_TASK_PER_CORE** 和 **CR_Memory**<br/>-- CR_CPU：CPU 是可消耗资源<br/>-- CR_CPU_Memory：CPU 和内存是可消耗资源<br/>-- CR_Core：核心是可消耗资源<br/>-- CR_Core_Memory：核心和内存是可消耗资源<br/>-- CR_ONE_TASK_PER_CORE：默认每个核心分配一个任务（不能与 CR_CPU* 参数共存）<br/>-- CR_CORE_DEFAULT_DIST_BLOCK：默认按块分配来分配核心<br/>-- CR_LLN：将资源分配给最空闲的节点（基于空闲 CPU 数量）<br/>-- CR_Pack_Nodes：使用盒分配来分配节点<br/>-- LL_SHARED_GRES：通用资源（GRES）分配时，优先选择负载最轻的设备<br/>-- CR_Socket：插槽是可消耗资源<br/>-- CR_Socket_Memory：内存和插槽是可消耗资源<br/>-- CR_Memory：内存是可消耗资源<br/>-- MULTIPLE_SHARING_GRES_PJ：允许每个节点多个共享 GRES<br/>-- ENFORCE_BINDING_GRES：在每个作业中默认启用 --gres-flags=enforce-binding<br/>-- ONE_TASK_PER_SHARING_GRES：在每个作业中默认启用 --gres-flags=one-task-per-sharing |
| SlurmctldAddr                 | 用于与当前活动 slurmctld 守护进程通信的可选地址。            |
| SlurmctldDebug                | slurmctld 日志的详细程度 -- quiet：不记录任何信息 -- fatal：仅记录致命错误 -- error：仅记录错误信息 -- info ：记录错误和一般信息（默认） -- verbose：记录错误和详细信息 -- debug：记录错误、详细信息和调试信息 -- debug2 ：记录错误、详细信息和更多调试信息 -- debug3 ：记录错误、详细信息和甚至更多调试信息 -- debug4 ：记录错误、详细信息和更多调试信息 -- debug5 ：记录错误、详细信息和更多调试信息 |
| SlurmctldHost                 | 执行 Slurm 控制守护进程的主机名。可选地跟随 IP 地址或标识名称，支持多主机列表以实现高可用性 |
| SlurmctldLogFile              | slurmctld 日志的完整路径名。默认值为无（通过 syslog 记录日志） |
| SlurmctldParameters           | Slurmctld 参数配置 allow_user_triggers：允许非 root/slurm_user 用户设置触发器 -- cloud_dns：允许通过 DNS 获取云节点的网络地址，避免节点创建后手动更新 -- disable_triggers：禁用注册新触发器的能力 -- enable_configless：允许配置无配置文件操作，支持动态获取配置和脚本 -- enable_job_state_cache：启用作业状态细节的独立缓存，减少其他操作的影响 -- idle_on_node_suspend：在暂停节点时将其标记为空闲，以便后续恢复 -- node_reg_mem_percent：节点允许注册的内存百分比，默认 100 -- no_quick_restart：禁止在启动新实例时杀死旧实例 -- power_save_interval：省电线程检查恢复和暂停节点的频率，默认 10 秒 -- power_save_min_interval：省电线程的最小检查频率，默认 0 -- max_powered_nodes：集群中最大可供电节点数量 -- max_dbd_msg_action：超过 MaxDBDMsgs 的操作，选项为 'discard'（默认）和 'exit' -- reboot_from_controller：从控制器运行重启程序，传递需要重启的节点列表 -- rl_bucket_size：令牌桶的大小，默认值为 30 -- rl_enable：启用每个用户的 RPC 限速支持 -- rl_log_freq：记录用户超出 RPC 限制的最大频率，默认值为 0 -- rl_refill_period：每秒添加的令牌频率，默认值为 1 -- rl_refill_rate：每个周期添加到令牌桶的令牌数量，默认值为 2 -- rl_table_size：用户哈希表中的条目数量，默认值为 8192 -- enable_stepmgr：启用全局 slurmstepd 步骤管理，支持作业步骤管理 -- user_resv_delete：允许任何用户删除保留 -- validate_nodeaddr_threads：启动时并行处理节点地址查找，默认值为 1 |
| SlurmctldPidFile              | slurmctld 进程 ID 文件的完整路径名，默认值为 `/var/run/slurmctld.pid` |
| SlurmctldPort                 | slurmctld 监听的端口号，默认值为 6817                        |
| SlurmctldPrimaryOffProg       | 主服务器切换为备用时执行的程序，默认不执行任何程序           |
| SlurmctldPrimaryOnProg        | 备用服务器切换为主要时执行的程序，默认不执行任何程序         |
| SlurmctldSyslogDebug          | slurmctld 在 syslog 中记录事件的详细程度，默认 `fatal`       |
| SlurmctldTimeout              | 备用控制器等待主控制器响应的时间间隔，默认值为 120 秒        |
| SlurmdDebug                   | slurmctld 在 syslog 中记录事件的详细程度，默认 `fatal`       |
| SlurmdLogFile                 | slurmd 日志文件的完整路径名，默认值为无（通过 syslog 记录日志） |
| SlurmdParameters              | Slurmd参数配置 -- allow_ecores：允许使用 E-Core 进行调度和任务放置 -- config_overrides：将每个节点的配置视为 slurm.conf 中指定的配置 -- l3cache_as_socket：使用 hwloc l3cache 作为 socket 计数 -- numa_node_as_socket：使用 hwloc NUMA Node 作为 socket -- shutdown_on_reboot：设置后在接收到重启请求时关闭 Slurmd -- contain_spank：在作业容器内运行 spank 调用 |
| SlurmdPidFile                 | slurmd 进程 ID 文件的完整路径名，默认值为 `/var/run/slurmd.pid` |
| SlurmdPort                    | slurmd 监听的端口号，默认值为 6818                           |
| SlurmdSpoolDir                | lurmd 状态信息和批处理作业脚本信息的写入目录，默认值为 `/var/spool/slurmd` |
| SlurmdSyslogDebug             | slurmd 在 syslog 中记录事件的详细程度，默认值为 `fatal`      |
| SlurmdTimeout                 | slurmctld 等待 slurmd 响应的时间（秒），默认值为 300，最大值为 65533。值为零表示不检查 slurmd 状态 |
| SlurmdUser                    | slurmd 以该用户身份执行，默认值为 `root`，该用户必须在集群所有节点上存在 |
| SlurmSchedLogFile             | 调度事件日志文件的完整路径名，配置日志时需要同时设置此参数和 SlurmSchedLogLevel |
| SlurmSchedLogLevel            | 调度事件日志的初始级别，0 表示禁用，1 表示启用，默认值为 0   |
| SlurmUser                     | slurmctld 以该用户身份执行，推荐使用非 `root` 用户           |
| SrunEpilog                    | 完成作业步骤后由 srun 执行的可执行文件的完整路径名           |
| SrunPortRange                 | srun 创建的监听端口范围，用于网络配置。必须大于 Cray 系统的 8192-60000 |
| SrunProlog                    | 在作业步骤启动前由 srun 执行的可执行文件的完整路径名         |
| StateSaveLocation             | slurmctld 保存其状态的目录的完整路径名，默认值为 `/var/spool` |
| SuspendExcNodes               | 指定不应进入省电模式的节点，支持 Slurm 的 hostlist 表达式    |
| SuspendExcParts               | 指定不应进入省电模式的分区                                   |
| SuspendExcStates              | 指定不应自动关闭的节点状态，默认情况下这些状态如果闲置将被关闭 |
| SuspendProgram                | 当节点闲置超过一定时间时执行的程序，预期将节点置于省电模式   |
| SuspendRate                   | 节点进入省电模式的速度（每分钟节点数），默认值为 60          |
| SuspendTime                   | 节点闲置或关闭后进入省电模式的时间（秒），默认为 INFINITE（无穷大） |
| SuspendTimeout                | 节点关闭请求和实际关闭之间允许的最大时间（秒），默认值为 30  |
| SwitchParameters              | 可选的交换机插件参数                                         |
| SwitchType                    | 指定用于应用程序通信的交换机或互连类型，默认无特殊插件 switch/hpe_slingshot：用于 HPE Slingshot 系统，专门优化了高性能计算的网络通信 switch/nvidia_imex：用于在 NVIDIA IMEX 域内分配唯一通道，以支持高效的内存共享和数据传输 |
| TaskEpilog                    | 作业所有者在每个任务终止后执行的程序的完整路径名             |
| TaskPlugin                    | 指定任务启动插件类型 task/affinity：通过 `sched_setaffinity()` 绑定进程到特定资源，支持 `--cpu-bind` 和/或 `--mem-bind` 选项，优化资源使用 task/cgroup：使用 Cgroups cpuset 接口进行进程限制，同样支持 `--cpu-bind` 和/或 `--mem-bind` 选项，适合需要资源隔离的环境 task/none：适用于不需要特殊任务处理的系统，默认设置，不支持绑定选项 |
| TaskPluginParam               | 任务插件的可选参数 -- Cores：默认情况下将任务绑定到核心，覆盖自动绑定设置 -- None：默认情况下不进行任务绑定，覆盖自动绑定设置 -- Sockets：默认情况下将任务绑定到插槽，覆盖自动绑定设置 -- Threads：默认情况下将任务绑定到线程，覆盖自动绑定设置 -- SlurmdOffSpec：如果节点上标识了专用核心或 CPU（即配置了 CoreSpecCount 或 CpuSpecList），那么运行在计算节点上的 Slurm 守护进程（如 slurmd 和 slurmstepd）将不使用这些资源 -- Verbose：默认情况下在任务运行之前详细报告绑定信息 -- Autobind：在自动绑定未找到匹配时设置默认绑定，可以选择 Threads、Cores 或 Sockets（例如，TaskPluginParam=autobind=threads） |
| TaskProlog                    | 在每个任务启动之前执行的程序的完整路径名                     |
| TCPTimeout                    | 允许建立 TCP 连接的时间，默认值为 2 秒                       |
| TmpFS                         | 用户作业可用于临时存储的文件系统的完整路径名，默认值为 `/tmp` |
| TopologyParam                 | 网络拓扑选项的逗号分隔选项 -- Dragonfly：针对 Dragonfly 网络优化资源分配，仅在 TopologyPlugin=topology/tree 时有效 -- RoutePart：使用分区节点列表替代插件的默认路由计算来路由通信对于多个分区的节点，将使用第一个出现的分区 -- SwitchAsNodeRank：将一个叶子交换机下的所有节点分配相同的节点排名，这在节点命名与网络拓扑不匹配时很有用 -- RouteTree：根据 topology.conf 文件中定义的交换机层级进行路由，而不仅仅是调度，适用于 TopologyPlugin=topology/tree -- TopoOptional：仅在作业包含交换机选项时优化网络拓扑的资源分配这可以降低大部分作业资源分配的碎片化，使得后续的拓扑优化变得更加高效 |
| TopologyPlugin                | 确定网络拓扑并优化作业分配的插件 -- topology/3d_torus：使用最佳匹配逻辑针对三维拓扑进行资源分配 -- topology/block：用于块网络拓扑 -- topology/default：其他系统的默认设置，使用最佳匹配逻辑针对一维拓扑进行资源分配 -- topology/tree：用于具有 select/cons_tres 插件的分层网络 |
| TrackWCKey                    | 布尔值，设置显示和跟踪工作负载特征键                         |
| TreeWidth                     | slurmd 使用的虚拟树网络的宽度（扇出），默认值为 16           |
| UnkillableStepProgram         | 如果进程在指定时间内不可杀死，将执行此程序                   |
| UnkillableStepTimeout         | Slurm 等待的时间（秒），在决定进程不可杀死之前。默认值为 60 秒 |
| UsePAM                        | 如果设置为 1，则启用 PAM（可插拔认证模块）。默认值为 0       |
| VSizeFactor                   | 作业或作业步骤的虚拟内存限制相对于其实际内存限制的百分比。默认值为 0，禁用虚拟内存限制 |
| WaitTime                      | srun 命令默认等待的秒数，在第一个任务终止后终止所有剩余任务。默认值为 0，禁用此功能 |
| X11Parameters                 | 与 Slurm 的内置 X11 转发实现一起使用                         |