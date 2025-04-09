# 超额订阅

## 订阅类型

可以在配置文件（slurm.conf）或提交作业时指定共享类型 `OverSubscribe`

- **OverSubscribe=FORCE**：分区中的所有资源（GRES 除外）都可以共享，而用户无法禁用，后面可以跟数字，（`OverSubscribe=FORCE:4`）代表每个资源可被多少个作业同时使用
- **OverSubscribe=YES**：分区中的所有资源（GRES 除外）都可以共享，仅当用户在提交作业时使用 `--oversubscribe` 选项时才会开启超额订阅，同样后面可以跟数字表示并行作业数
- **OverSubscribe=NO**：选定的资源将分配给单个作业。任何资源都不会共享



## 选择类型

可以在配置文件（slurm.conf）指定选择类型 `SelectType`

- **select/linear**：整体模式，可以控制**节点**是否共享，不支持详细资源的共享
- **select/cons_tres**：默认配置，支持按核心、内存、GPU 等可消耗资源（TRES）精细管理，可灵活共享资源

若选择 `cons_tres` 模式，则可以通过 `SelectTypeParameters` 参数管理超额订阅的资源

| SelectTypeParameters         | 描述          |
|------------------------------|-------------|
| CR_Core / CR_Core_Memory     | 以CPU核心为粒度分配超额订阅资源 |
| CR_CPU / CR_CPU_Memory       | 以CPU为粒度分配超额订阅资源 |
| CR_Socket / CR_Socket_Memory | 以CPU插槽为粒度分配超额订阅资源 |

