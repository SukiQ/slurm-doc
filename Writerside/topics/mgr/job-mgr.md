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
      <li>使用 --account 设置作业计费的账户</li>
    </list>
    <p><br/></p>
    <code-block lang="bash">
          sbatch --partition=sivi --job-name=sivi-job --mincpus=3  task.sh
      </code-block>
  </tab>  
  <tab id="api" title="API" group-key="api">How to install on macOS.</tab> 
</tabs>


## 修改作业

使用 `scontrol update` 命令，参数<a href="scontrol.md#job-params">详见</a>

- JobId 必填
- 使用 Partition 修改作业的分区
- 使用 StdIn StdOut StdErr 控制作业输入输出错误文件
- 使用 Priority 直接更改作业的优先级，或使用 SiteFactor Nice 通过<a href="priority.md#multifactor-plugin">多因子插件</a>改变作业多优先级

```bash
scontrol update JobId=160 SiteFactor=100
```

## 删除作业

使用 `scancel` 命令删除

```bash
scancel 130
```