# sbatch

`sbatch` 用于向 Slurm 批量提交作业

```bash
sbatch [选项] [脚本] [参数]
```



- 选项

| 参数                    | 说明                                       |
|-----------------------|------------------------------------------|
| -A, --account         | 将作业资源计入指定的账户                             |
| --acctg-freq          | 定义作业计费和采样间隔（秒）                           |
| -a, --array           | 提交作业数组，允许多个作业并行执行                        |
| --batch               | 用户可以指定批处理脚本运行所需的节点特性，支持 `AND` 和 `OR` 操作符 |
| --bb                  | 突发缓冲区的配置                                 |
| --bbf                 | 突发缓冲区的配置路径                               |
| -b, --begin           | 作业开始时间                                   |
| -D, --chdir           | 设置批处理脚本执行前的工作目录                          |
| --cluster-constraint  | 指定集群所需的特性                                |
| -M, --clusters        | 指定要发送命令的集群                               |
| --comment             | 作业注释                                     |
| -C, --constraint      | 用户可以指定作业所需的节点特性                          |
| --container           | 指定要使用的OCI容器路径                            |
| --container-id        | 指定OCI容器的唯一ID                             |
| --contiguous          | 要求节点分配必须是连续的                             |
| -S, --core-spec       | 为系统保留特定数量的专用核心                           |
| --cores-per-socket    | 限制节点选择，要求每个插槽的核心数量至少为指定                  |
| --cpu-freq            | 请求为作业步骤设置CPU频率                           |
| --cpus-per-gpu        | 每个分配的GPU请求分配指定数量的CPU                     |
| -c, --cpus-per-task   | 每个任务请求分配指定数量的CPU                         |
| --deadline            | 指定任务的截止时间                                |
| --delay-boot          | 指定任务等待时间                                 |
| -d, --dependency      | 任务依赖项                                    |
| -m, --distribution    | 作业分布策略                                   |
| -e, --error           | 指定错误输出文件名                                |
| -x, --exclude         | 排除节点                                     |
| --exclusive           | 独占节点                                     |
| --export              | 导出环境变量的范围                                |
| --export-file         | 导出环境变量文件路径                               |
| --extra               | 附加字段，充当过滤标识                              |
| -B, --extra-node-info | 限制节点选择                                   |
| --get-user-env        | 获取用户登录环境的变量                              |
| --gid                 | 指定组权限                                    |
| --gpu-bind            | 绑定GPU资源                                  |
| --gpu-freq[,verbose]  | 配置GPU频率                                  |
| -G, --gpus            | 指定总GPU数量或类型                              |
| --gpus-per-node       | 指定每个节点GPU数量或类型                           |
| --gpus-per-socket     | 指定每个插槽GPU数量或类型                           |
| --gpus-per-task       | 指定每个任务GPU数量或类型                           |
| --gres                | 指定通用可消耗资源。                               |
| --gres-flags          | 资源绑定选项                                   |
| -h, --help            | 显示帮助信息                                   |
| --hint                | 应用绑定提示                                   |
| -H, --hold            | 提交为保留状态                                  |
| --ignore-pbs          | 忽略PBS选项                                  |
| -i, --input           | 指定输入文件                                   |
| -J, --job-name        | 指定作业名称                                   |
| --kill-on-invalid-dep | 是否kill无效依赖                               |
| -L, --licenses        | 指定许可证                                    |
| --mail-type           | 邮件通知类型                                   |
| --mail-user           | 指定通知用户                                   |
| --mcs-label           | MCS组标签                                   |
| --mem                 | 指定内存需求                                   |
| --mem-bind            | 作业绑定内存                                   |
| --mem-per-cpu         | 每CPU内存需求                                 |
| --mem-per-gpu         | 每GPU内存需求                                 |
| --mincpus             | 最小CPU数                                   |
| --network             | 网络信息                                     |
| --nice                | 调整优先级                                    |
| -k, --no-kill         | 不自动终止作业，如果节点失败，用户需自负责任                   |
| --no-requeue          | 作业不会被重新排队，无法由管理员恢复                       |
| -F, --nodefile        | 从指定文件读取节点列表                              |
| -w, --nodelist        | 请求特定节点列表                                 |
| -N, --nodes           | 请求指定的节点数量                                |
| -n, --ntasks          | 请求最多运行的任务数                               |
| --ntasks-per-core     | 每个核心上调用最大任务数                             |
| --ntasks-per-gpu      | 每个 GPU 调用任务数                             |
| --ntasks-per-node     | 每个节点调用任务数                                |
| --ntasks-per-socket   | 每个插槽调用最大任务数                              |
| --open-mode           | 为输出和错误文件指定输出模式                           |
| -o, --output          | 指定输出文件名                                  |
| -O, --overcommit      | 允许超额分配资源                                 |
| -s, --oversubscribe   | 允许与其他作业共享资源                              |
| --parsable            | 仅输出作业 ID 和集群名称                           |
| -p, --partition       | 请求特定分区                                   |
| --prefer              | 指定希望的节点特性                                |
| --priority            | 请求特定作业优先级，可以指定数字或`TOP`                   |
| --profile             | 启用详细的数据收集                                |
| --propagate           | 指定要传播的资源限制                               |
| -q, --qos             | 请求作业的服务质量                                |
| -Q, --quiet           | 抑制 sbatch 的信息消息，仅显示错误                    |
| --reboot              | 强制分配的节点在作业开始前重启                          |
| --requeue             | 指定批处理作业可以重新排队                            |
| --reservation         | 从指定的保留中分配资源                              |
| --resv-ports          | 为作业保留通信端口                                |
| --segment             | 定义用于创建作业分配的段大小                           |
| --signal              | 在作业结束前发送信号                               |
| --sockets-per-node    | 限制节点选择，要求至少有指定数量的插槽                      |
| --spread-job          | 将作业分配尽可能均匀地分散到多个节点                       |
| --stepmgr             | 启用 per-job 的 slurmstepd 步骤管理             |
| --switches            | 定义所需的最大叶交换机数量及等待时间                       |
| --test-only           | 验证批处理脚本并估算作业调度时间                         |
| --thread-spec         | 为系统操作保留的特殊线程数                            |
| --threads-per-core    | 限制节点选择，要求每个核心至少有指定数量的线程                  |
| -t, --time            | 设置作业分配的总运行时间限制                           |
| --time-min            | 设置作业分配的最小时间限制                            |
| --tmp                 | 指定每个节点的临时磁盘空间的最小值                        |
| --tres-bind           | 指定资源跟踪的绑定选项                              |
| --tres-per-task       | 指定每个任务所需的可跟踪资源列表                         |
| --uid                 | 尝试以指定用户身份提交和/或运行作业                       |
| --usage               | 显示简要帮助信息并退出                              |
| --use-min-nodes       | 优先使用较小的节点计数                              |
| -v, --verbose         | 增加 sbatch 的信息消息的详细程度                     |
| -V, --version         | 显示版本信息并退出                                |
| -W, --wait            | 不退出，直到提交的作业终止                            |
| --wait-all-nodes      | 控制命令开始执行的时机                              |
| --wckey               | 指定与作业一起使用的 wckey                         |
| --wrap                | 将指定的命令字符串包装在简单的 "sh" shell 脚本中           |

