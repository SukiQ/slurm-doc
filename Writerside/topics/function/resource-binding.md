# 资源绑定

Slurm 提供了多种资源绑定机制来优化任务执行性能，包括 CPU、内存和 GPU 等资源的绑定控制

<note>优先级：执行时 > 按节点/按分区 > 全局配置</note>

<img src="resource-0.png" alt="image.png" width="700" />

- **绑定sockets**：将任务绑定到CPU插槽，减少跨插槽内存访问，适用于任务数等于插槽数的场景，或是内存密集型应用
- **绑定cores**：将任务绑定到单独的物理核心，适用于计算密集型应用
- **绑定threads**：将任务绑定到逻辑线程，适用于高并发轻量级应用、I/O密集型应用
- **绑定numa**：将任务绑定到NUMA本地域，适用于大内存带宽应用、GPU计算



## 执行时绑定


| 绑定类型         | 描述                                        |
| ---------------- | ------------------------------------------- |
| quiet            | 任务运行前静默绑定（默认行为）              |
| verbose          | 任务运行前详细报告绑定情况                  |
| none             | 不将任务绑定到CPU（默认，除非启用自动绑定） |
| map_cpu:<列表>   | 绑定任务到CPU核心（通过CPU的id）            |
| mask_cpu:<列表>  | 绑定任务到CPU核心（通过CPU的标记）          |
| rank_ldom        | 按任务等级绑定到NUMA域                      |
| map_ldom:<列表>  | 绑定任务到NUMA域（通过NUMA 的id）           |
| mask_ldom:<列表> | 绑定任务到NUMA域（通过NUMA 的标记）         |
| sockets          | 自动绑定任务到CPU插槽                       |
| cores            | 自动绑定任务到物理核心                      |
| threads          | 自动绑定任务到逻辑线程                      |
| ldoms            | 自动绑定任务到NUMA域                        |
| help             | 显示cpu-bind帮助信息                        |

```bash
srun --cpu-bind=<绑定类型> [绑定参数]
```



## 按节点/分区绑定

| 绑定模式 | 描述                   |
| -------- | ---------------------- |
| none     | 不进行 CPU 绑定        |
| socket   | 自动绑定任务到CPU插槽  |
| core     | 自动绑定任务到物理核心 |
| thread   | 自动绑定任务到逻辑线程 |
| ldom     | 自动绑定任务到NUMA域   |
| off      | 禁用之前设置的绑定     |

<tabs group="bind_cpu">
    <tab id="cmd" title="命令行" group-key="cmd">
       <code-block lang="bash">
          #按节点绑定
          scontrol update NodeName=node01 CpuBind=core
          #按分区绑定
          scontrol update PartitionName=debug CpuBind=core
       </code-block>
    </tab>
   <tab id="conf" title="配置" group-key="conf">
       <code-block lang="bash">
          CpuBind=core
      </code-block>
  </tab>
</tabs>



## 按插件绑定

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| Cores         | 将任务默认绑定到物理核心                                     |
| None          | 不执行任务绑定                                               |
| Sockets       | 将任务默认绑定到CPU插槽                                      |
| Threads       | 将任务默认绑定到逻辑线程                                     |
| SlurmdOffSpec | 为节点配置专用核心/CPU时，Slurm守护进程（slurmd/slurmstepd）将在这些资源外运行 |
| OOMKillStep   | 当步骤中任何任务触发OOM事件时，杀死所有节点上的整个步骤      |
| Verbose       | 默认在任务运行前详细报告绑定情况                             |
| Autobind      | 当**自动绑定**未找到匹配时的默认绑定设置                     |

```bash
TaskPluginParam=Cores
```

