# 资源限制

Slurm 支持从多个层级设置资源限制，资源限制对象包括关联和 QOS（服务质量），资源限制规则按照以下顺序执行:

<img src="resource-limits-0.png" alt="image.png" width="700" />

<note>如果出现限制重复，则使用第一次出现的限制</note>



## 资源限制配置

可以在配置文件（slurm.conf）指定资源限制策略 `AccountingStorageEnforce`

- associations：要求所有作业必须指定正确的关联（ cluster，account，user，partition ）
- limits：隐藏启用关联和QOS限制（不会阻止作业提交）
- qos：要求所有作业必须指定正确的 QOS (服务质量)
- safe：只有满足了 TRES 限制时，作业才会启动（安全启动）自动启用 limits 限制 + qos 限制
- wckeys：阻止用户使用无权访问的 wckey 运行作业，自动启用 associations 限制




## 通过关联限制

| 参数                    | 说明                            |
|:----------------------|:------------------------------|
| Fairshare             | 用于确定优先级的整数值                   |
| GrpJobs               | 关联及其子关联能运行的总作业数               |
| GrpJobsAccrue         | 关联及其子关联能累积年龄优先级的待处理作业数        |
| GrpSubmitJobs         | 关联及其子关联能提交的总作业数               |
| GrpTRES               | 关联及其子关联能使用的可追踪资源（TRES）总量      |
| GrpTRESMins           | 关联及其子关联可能使用的可追踪资源（TRES）分钟总数   |
| GrpTRESRunMins        | 关联及其子关联运行作业使用的可追踪资源（TRES）分钟总数 |
| GrpWall               | 关联及其子关联运行作业的最大总挂钟时间           |
| MaxJobs               | 关联能运行的总作业数                    |
| MaxJobsAccrue         | 关联能累积年龄优先级的最大待处理作业数           |
| MaxSubmitJobs         | 关联能提交的最大作业数                   |
| MaxTRESMinsPerJob     | 单个作业能使用的TRES分钟数限制             |
| MaxTRESPerJob         | 作业能拥有的最大TRES大小                |
| MaxTRESPerNode        | 作业分配中每个节点能使用的最大TRES大小         |
| MaxWallDurationPerJob | 单个作业能运行的最大挂钟时间                |
| MinPrioThreshold      | 保留资源所需的最低优先级                  |
| QOS                   | 关联能运行的QOS列表                   |



- 

## 通过服务质量限制

| 参数                      | 说明                          |
|:------------------------|:----------------------------|
| GraceTime               | 被抢占作业的宽限时间                  |
| GrpJobs                 | QOS能运行的总作业数                 |
| GrpJobsAccrue           | QOS能累积年龄优先级的待处理作业数          |
| GrpSubmitJobs           | QOS能提交的总作业数                 |
| GrpTRES                 | QOS作业能使用的TRES（可追踪资源）总量      |
| GrpTRESMins             | QOS作业可能使用的TRES（可追踪资源）分钟总数   |
| GrpTRESRunMins          | QOS运行作业使用的TRES（可追踪资源）分钟总数   |
| GrpWall                 | QOS运行作业的最大总挂钟时间             |
| LimitFactor             | 关联TRES限制的乘数因子               |
| MaxJobsAccruePerAccount | 账户能累积年龄优先级的最大待处理作业数         |
| MaxJobsAccruePerUser    | 用户能累积年龄优先级的最大待处理作业数         |
| MaxJobsPerAccount       | 账户能运行的最大作业数                 |
| MaxJobsPerUser          | 用户能运行的最大作业数                 |
| MaxSubmitJobsPerAccount | 账户能拥有的运行和待处理最大作业数           |
| MaxSubmitJobsPerUser    | 用户能拥有的运行和待处理最大作业数           |
| MaxTRESMinsPerJob       | 每个作业能使用的最大TRES（可追踪资源）分钟数    |
| MaxTRESPerAccount       | 账户能分配的最大TRES（可追踪资源）数        |
| MaxTRESPerJob           | 每个作业能使用的最大TRES（可追踪资源）数      |
| MaxTRESPerNode          | 作业分配中每个节点能使用的最大TRES（可追踪资源）数 |
| MaxTRESPerUser          | 用户能分配的最大TRES（可追踪资源）数        |
| MaxWallDurationPerJob   | 每个作业能使用的最大挂钟时间              |
| MinPrioThreshold        | 保留资源所需的最低优先级                |
| MinTRESPerJob           | 作业能拥有的最小TRES（可追踪资源）大小       |
| UsageFactor             | 作业TRES（可追踪资源）使用量的乘数因子       |