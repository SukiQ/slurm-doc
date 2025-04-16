# sacctmgr

`scontrol` 用于查看或修改 Slurm 账号

```bash
sacctmgr [选项] [子命令]
```



- 选项


| 选项                        | 描述                                                   |
| --------------------------- | ------------------------------------------------------ |
| -s, --associations          | 与 show 或 list 一起使用以显示与实体的关联             |
| -h, --help                  | 打印帮助信息，描述 sacctmgr 的用法                     |
| -i, --immediate             | 立即提交更改，无需确认                                 |
| --json, --json=list, --json | 以 JSON 格式导出信息                                   |
| -n, --noheader              | 输出开头不添加标题                                     |
| -p, --parsable              | 输出将用`|`分隔，并在末尾加上`|`                       |
| -P, --parsable2             | 输出将用`|`分隔，末尾不加`|`                           |
| -Q, --quiet                 | 除错误消息外不打印任何消息                             |
| -r, --readonly              | 使正在运行的 sacctmgr 无法修改账务信息。适用于交互模式 |
| --yaml, --yaml=list, --yaml | 以 YAML 格式导出信息                                   |
| -v, --verbose               | 启用详细日志记录                                       |
| -V, --version               | 显示版本号                                             |

- 子命令

| 命令              | 描述                                                         |
| ----------------- | ------------------------------------------------------------ |
| add               | 添加一个实体。与 create 命令相同                             |
| archive           | 将数据库信息写入平面文件或加载先前已写入文件的信息           |
| clear stats       | 清除服务器统计信息                                           |
| create            | 添加一个实体                                                 |
| delete where      | 删除指定的实体                                               |
| dump              | 将集群数据转储到指定文件。如果未指定文件名，则默认使用 clustername.cfg 文件名 |
| help              | 显示 sacctmgr 选项和命令的描述                               |
| list              | 显示指定实体的信息。默认情况下，显示所有条目，可以通过在查询中指定 SPECS 来缩小结果 |
| load              | 从指定文件加载集群数据。该文件是通过运行 sacctmgr dump 命令生成的配置文件 |
| modify where  set | 修改一个实体                                                 |
| reconfigure       | 如果正在运行 SlurmDBD，则重新配置它                          |
| remove where      | 删除指定的实体                                               |
| show              | 显示指定实体的信息。默认情况下，显示所有条目，可以通过在查询中指定 SPECS 来缩小结果 |
| shutdown          | 关闭服务器                                                   |
| version           | 显示 sacctmgr 的版本号                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |



## 关联参数 {id="association-params"}

| 参数                          | 说明                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| DefaultQOS                    | 关联及其子关联的默认QOS                                      |
| Fairshare/Share               | <a href="priority.md#multifactor-plugin">多因子插件</a>公平共享权重 |
| GrpJobs                       | 关联及其子关联的运行中作业总数上限                           |
| GrpJobsAccrue                 | 关联及其子关联的可累积年龄优先级的待处理作业的总数上限       |
| GrpSubmit/GrpSubmitJobs       | 关联及其子关联处于 PENDING 或 RUNNING  状态作业的总数上限    |
| GrpTRES                       | 关联及其子关联的运行中作业可分配 TRES 总量上限               |
| GrpTRESMins                   | 关联及其子关联的过去/当前/未来作业累计TRES运行时间（分钟）上限 |
| GrpTRESRunMins                | 关联及其子关联所有运行中作业的TRES分钟数实时总和上限         |
| GrpWall                       | 关联及其子关联的运行中作业总TRES运行时间（分钟）上限         |
| MaxJobs                       | 用户在该关联下的单账户运行作业数上限                         |
| MaxJobsAccrue                 | 该关联下可累积年龄优先级的待处理作业数上限                   |
| MaxSubmit/MaxSubmitJobs       | 该关联的待处理或运行中作业总数上限                           |
| MaxTRESMins/MaxTRESMinsPerJob | 该关联下单作业的TRES分钟数上限                               |
| MaxTRES/MaxTRESPerJob         | 该关联下单作业的TRES资源上限                                 |
| MaxTRESPerNode                | 该关联下单节点分配的TRES资源上限                             |
| MaxWall/MaxWallDurationPerJob | 该关联下单作业的墙钟时间上限                                 |
| Priority                      | 该关联下作业的额外优先级                                     |
| QosLevel                      | 作业可用的QOS列表（支持=,+=,-=运算符）                       |



## 