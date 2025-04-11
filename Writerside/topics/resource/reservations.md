# 资源预留

Slurm 支持为特定用户或账户预留资源（如节点、CPU、许可证、突发缓冲区等），并在**指定时间段内**独占使用

<warning>仅  root 或 SlurmUser 用户可管理资源预留</warning>



## 创建资源预留

使用 `scontrol create reservation` 创建资源预留，参数<a href="scontrol.md#reservation-params">详见</a>

```bash
scontrol create reservation  Start=08:10 END=08:20 Nodes=ALL Users=root
```



## 查看资源预留

使用 `scontrol show reservation` 创建资源预留，参数<a href="scontrol.md#reservation-params">详见</a>

```bash
scontrol show reservation 

>ReservationName=root_1 StartTime=2025-04-11T08:10:00 EndTime=2025-04-11T08:20:00 Duration=00:10:00
 Nodes=k8smaster2,zznode-[140-141] NodeCnt=3 CoreCnt=48 Features=(null) PartitionName=(null)  Flags=SPEC_NODES,ALL_NODES
 TRES=cpu=48
 Users=root Groups=(null) Accounts=(null) Licenses=(null) State=INACTIVE BurstBuffer=(null)
 MaxStartDelay=(null)
```



## 修改资源预留

使用 `scontrol update` 修改资源预留

```bash
scontrol update ReservationName=root_1  Start=08:20 END=08:30
```



## 删除资源预留

使用 `scontrol delete` 修改资源预留

```bash
scontrol delete ReservationName=root_1
```
