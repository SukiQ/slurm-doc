# 通用资源

Slurm支持定义和调度任意类型的通用资源（GRES），包括：

- **GPU设备**
- **CUDA多进程服务(MPS)**
- **多实例GPU(MIG)**
- **插件实现分片资源(Sharding)**

可以在配置文件（slurm.conf）指定通用资源类型 `GresTypes` 为gpu , mps , bandwidth