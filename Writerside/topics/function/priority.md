# 作业优先级

默认情况下，Slurm使用多因子插件（priority/multifactor plugin）设置优先级，但是也可以在 slurm.conf 文件中设置 PriorityType=priority/basic 来实现基本的先进先出调度策略

多因子插件的影响因子如下：

- **Age**：作业在队列中的等待时间
- **Association**：关联对象的因子
- **Fairshare**： 分配的计算资源与消耗的计算资源的差额
- **Job size**：为作业分配的节点数或CPU数量
- **Nice**：用户可以控制的优先级参数
- **Partition**：与节点分区相关
- **QOS**： 与服务质量相关
- **Site**：`job_submit` 和 `site_factor` 插件的影响因子
- **TRES**: 对于作业来说，每个可消耗资源都有自己的因子