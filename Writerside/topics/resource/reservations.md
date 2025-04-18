# 资源预留

Slurm 支持为指定**用户**或指定**账户**预留资源（如节点、CPU、许可证、突发缓冲区等），并在**指定时间段内**独占使用

<warning>仅  root 或 SlurmUser 用户可管理资源预留</warning>



## 创建资源预留

使用 `scontrol create reservation` 创建资源预留，参数<a href="scontrol.md#reservation-params">详见</a>

- ReservationName 必填
- 预留时间 StartTime 必填，EndTime/ Duration 必填一项
- 预留对象 Accounts / Users /Groups 必填一项，可以填多表示需同时满足
- 用于停机系统维护的资源预留一般通过指定 Flags=MAINT
- 通过指定 Flags=HOURLY / DAILY/ WEEKLY 定期执行资源预留 
- 分区 PartitionName 必填（不指定则为默认分区）
- 预留资源必填，可以使用 Nodes / NodeCnt 指定节点，也可以使用 CoreCnt / TRES 指定细粒度资源

```bash
scontrol create reservation  StartTime=08:10 EndTime=08:20 Nodes=ALL Users=root
```



## 查看资源预留

使用 `scontrol show reservation` 创建资源预留，参数<a href="scontrol.md#reservation-params">详见</a>

```bash
scontrol show reservation 

>ReservationName=root_1 StartTime=2025-04-11T08:10:00 EndTime=2025-04-11T08:20:00 Duration=00:10:00
 Nodes=k8smaster2,sivi-[140-141] NodeCnt=3 CoreCnt=48 Features=(null) PartitionName=(null)  Flags=SPEC_NODES,ALL_NODES
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
