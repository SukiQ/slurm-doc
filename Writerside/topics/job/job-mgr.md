# 作业管理

作业（Job） 是用户提交的计算任务单位，由资源请求（如CPU、内存、GPU等）和实际运行的程序组成

<img src="job-mgr-0.png" alt="image.png" width="700" />

- **BOOT_FAIL**: 由于节点启动失败而终止
- **CANCELLED**: 被用户或管理员取消
- **COMPLETED**: 成功完成作业执行
- **DEADLINE**: 由于达到作业规定的最晚完成时间（--deadline）而终止
- **FAILED**: 作业执行失败
- **NODE_FAIL**: 由于节点故障而终止
- **OUT_OF_MEMORY**: 遇到内存不足而失败
- **PENDING**: 排队等待启动
- **PREEMPTED**: 由于被抢占而终止
- **RUNNING**: 作业执行中
- **SUSPENDED**: 已分配资源但执行暂停，例如由于抢占或用户请求暂停
- **TIMEOUT**: 由于达到作业时间限制而终止

## 提交作业

使用 `sbatch` 命令<a href="sbatch.md">提交作业</a>，或通过API的<a href="api-submit-job.md">提交作业接口</a>

<?xml version="1.0" encoding="utf-8"?>

<tabs group="sbatch-job"> 
  <tab id="cmd" title="命令行" group-key="cmd"> 
    <list type="bullet"> 
      <li>使用 --job-name 设置作业名称</li>
      <li>使用 --account 设置作业计费的账户</li>
      <li>使用 --partition 设置作业分区，如果未指定则使用默认分区</li>
      <li>使用 --nodelist 请求固定的节点，或是 --nodes --exclude --extra-node-info 等参数动态选择节点</li>
      <li>使用 --input --output --error 控制作业输入输出错误文件</li>
    </list> 
  </tab>  
  <tab id="api" title="API" group-key="api">How to install on macOS.</tab> 
</tabs>


## 创建分区

使用 `scontrol create` 命令，或者编辑 `slurm.conf` 文件创建分区，参数<a href="scontrol.md#partitions-params">详见</a>

- PartitionName 必填
- 使用 AllocNodes，AllowAccounts，AllowGroups，DenyAccounts，DisableRootJobs 等参数定义分区创建的权限
- 使用 Nodes 指定分区的节点列表
- 使用 MaxCPUsPerNode，MaxMemPerCPU，MaxMemPerNode，MaxNodes 等参数定义分区的资源
- 使用 CpuBind 控制<a href="resource-binding.md">资源绑定</a>模式

## 删除分区

使用 `scontrol delete` 命令删除分区

```bash
scontrol delete PartitionName=sivi
```

## 修改分区

使用 `scontrol update` 命令修改分区，参数<a href="scontrol.md#partitions-params">详见</a>

```bash
scontrol update PartitionName=sivi Nodes=zznode-[140-141]
```