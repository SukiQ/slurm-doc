# 调度配置

Slurm内置两种调度触发策略：

- **事件触发的快速调度（快速反应）**：提交作业，完成作业，配置变更等事件触发时，系统会立刻尝试调度。为了效率，Slurm 只会考虑最多 `default_queue_depth` 个作业（默认是 100 个）

- **定期的主调度循环（全面评估）**：每隔一段时间（由 `sched_interval` 控制，默认 60 秒）会重新检查所有作业



## 调度策略

可以在配置文件（slurm.conf）或提交作业时指定共享类型 `SchedulerType`，可选：

- **sched/backfill**：执行回填调度，在**不延迟高优先级作业预期启动时间的前提下**启动低优先级作业
- **sched/builtin**：先进先出 (FIFO) 调度程序，按优先级顺序启动作业，并且保持**分区内串行**，分区中只要有一个作业还没被调度，就不会调度这个分区里的其他低优先级作业



## 回填调度

如果没有合理的作业时间限制估值，回填调度将很困难，可以配置参数提供帮助

- **DefaultTime**: 默认作业时间限制（按分区指定值）
- **MaxTime**: 最大作业时间限制（按分区指定值）
- **OverTimeLimit**: 作业在被终止前可以超出其时间限制的量

详细的回填调度相关配置可以配置 **SchedulerParameters** 参数

- `bf_continue`：锁释放后继续回填调度（可能延迟新作业调度）
- `bf_interval=#`：回填调度尝试间隔（默认30秒）
- `bf_max_job_part=#`：单次回填周期每分区最大启动作业数（默认0无限制）
- `bf_max_job_start=#`：单次回填周期最大启动作业总数（默认0）
- `bf_max_job_test=#`：单次回填周期最大检查作业数（默认100）
- `bf_max_job_user=#`：单次回填周期每用户最大启动作业数（默认0）
- `bf_max_time=#`：回填调度最大耗时（秒），默认同`bf_interval`
- `bf_one_resv_per_job`：每作业仅允许一个回填预留（默认禁用）
- `bf_resolution=#`：回填调度时间精度（秒），默认60
- `bf_window=#`：未来时间窗口（分钟），默认1440（1天）。建议≥最长作业时限
- `bf_yield_interval=#`：锁释放间隔（微秒），默认2,000,000（2秒）
- `bf_yield_sleep=#`：锁释放时长（微秒），默认500,000（0.5秒）

