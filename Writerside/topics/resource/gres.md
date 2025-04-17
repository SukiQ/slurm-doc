# 通用资源

Slurm支持定义和调度任意类型的**特殊资源**（通用资源），例如 GPU、MPS（CUDA多进程服务）等

可以在配置文件（slurm.conf）指定通用资源类型 GresTypes ，这些资源类型需要在节点配置中定义或者在通用资源配置文件 gres.conf 中定义（推荐）

目前 Slurm 自带的管理资源支持：

- **gpu**：GPU
- **mps**：CUDA多进程服务
- **nic**：网卡
- **shard**：GPU分片

## 定义通用资源

- 在节点定义

<tabs group="gres"> 
  <tab id="config" title="配置" group-key="config">
    <p><br/></p>
       <code-block lang="bash">
         # 定义资源类型
          GresTypes=gpu,mps,bandwidth 
          # 定义资源配置，格式为 资源名称:资源类型:是否是消耗资源:资源数量
          NodeName=tux[0-7] Gres=gpu:tesla:2,gpu:kepler:2
      </code-block>
  </tab>  
  <tab id="cmd" title="命令" group-key="cmd">

  <p><br/></p>
      <code-block lang="bash">
        # 修改通用资源
        scontrol update NodeName=sivi Gres=gpu:tesla:2
      </code-block>
  </tab> 
</tabs>


- 在配置文件（gres.conf）定义

```bash
# 定义资源
AutoDetect=nvml
Name=gpu Type=gtx560 File=/dev/nvidia0 COREs=0,1
Name=gpu Type=tesla  File=/dev/nvidia1 COREs=2,3
Name=mps Count=100 File=/dev/nvidia0 COREs=0,1
Name=mps Count=100  File=/dev/nvidia1 COREs=2,3
# 绑定节点
NodeName=tux[0-2]  Name=gpu File=/dev/nvidia[0-3]
```



## 使用通用资源

在提交作业时可以通过 --gres 绑定通用资源

```bash
sbatch --gres=gpu:4 gres_test.bash 
```

