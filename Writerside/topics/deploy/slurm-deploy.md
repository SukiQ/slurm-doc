# Slurm安装

- 新增环境变量

```bash
LD_LIBRARY_PATH=/usr/local/openmpi/lib:/usr/local/munge/lib64:/usr/local/slurm/lib64:/usr/local/pmix/lib
```

- 编译源

```bash
# 24 版本编译指令 必须加mysql的安装路径
./configure --prefix=/usr/local/slurm24 --with-munge=/usr/local/munge --sysconfdir=/usr/local/slurm24/etc --localstatedir=/usr/local/slurm24/local --runstatedir=/usr/local/slurm24/run --libdir=/usr/local/slurm24/lib64 --build=x86_64-redhat-linux-gnu --host=x86_64-redhat-linux-gnu --with-systemdsystemunitdir=/usr/lib/systemd/system --with-mysql_config=/home/deploy/fdec/mysql-8.0.27/bin --enable-slurmrestd --with-json=/usr/local --with-http-parser=/usr/local --with-jwt=/usr/local --with-json=/usr/local

#  如果要支持openmpi，configure需要增加参数：--with-pmix=/usr/local/pmix --with-munge=/usr/local/munge --with-hwloc=/usr/local/hwloc --with-ucx=/usr/local/ucx

make
sudo make install
```

- 创建用户

```bash
sudo groupadd slurm -g 650
sudo useradd  -g slurm -u 650 -s /bin/bash slurm
sudo groupadd slurmrestd -g 651
sudo useradd  -g slurmrestd -u 651 -s /bin/bash slurmrestd
sudo chown -R slurm:slurm slurm

# 修改slurm 和 slurmrestd 用户的 .bashrc,增加

export PATH=/usr/local/munge/bin:/usr/local/slurm24/bin:/usr/local/slurm24/sbin:$PATH
export LD_LIBRARY_PATH=/home/liuhongyu/mysql-8.0.27/lib:/usr/local/lib:/usr/local/lib64:/usr/local/munge/lib64:/usr/local/slurm24/lib64:$LD_LIBRARY_PATH
```

- 配置数据库

```sql
create user 'slurm' identified WITH mysql_native_password  by '123456';

create database slurm_acct_db;
grant all on slurm_acct_db.* TO 'slurm'@'%'  with grant option;

create database slurm_jobcomp_db;
grant all on slurm_jobcomp_db.* TO 'slurm'@'%'  with grant option;
```

- 创建配置文件

```bash
#  解压包路径下
cd etc  
sudo mkdir -p /usr/local/slurm24/etc
sudo mkdir -p /usr/local/slurm24/log
sudo mkdir -p /usr/local/slurm24/run
sudo mkdir -p /usr/local/slurm24/slurm
sudo cp slurm.conf.example /usr/local/slurm24/etc/slurm.conf
sudo cp slurmdbd.conf.example /usr/local/slurm24/etc/slurmdbd.conf
sudo cp cgroup.conf.example /usr/local/slurm24/etc/cgroup.conf
sudo chown -R slurm:slurm /usr/local/slurm24/etc
sudo chown -R slurm:slurm /usr/local/slurm24/log
sudo chown -R slurm:slurm /usr/local/slurm24/run
sudo chown -R slurm:slurm /usr/local/slurm24/slurm
```

- 修改`/usr/local/slurm24/etc/slurm.conf`关键配置项适应当前部署环境

```ini
#  修改目录/文件相关参数
SlurmctldLogFile=/var/log/slurm/slurmctld.log
SlurmdLogFile=/var/log/slurm/slurmd.log

SlurmctldPidFile=/var/run/slurm/slurmctld.pid
SlurmdPidFile=/var/run/slurm/slurmd.pid

SlurmdSpoolDir=/var/spool/slurm/slurmd
StateSaveLocation=/var/spool/slurm/slurmctld

#  修改管理节点主机名
SlurmctldHost=node112
#  修改worker节点主机名范围
NodeName=node[112-114] CPUs=1 State=UNKNOWN
```

- 创建slurm日志路径, spool 路径

```bash
sudo mkdir -p /var/log/slurm
sudo chown -R slurm:slurm /var/log/slurm
sudo mkdir -p /var/spool/slurm
sudo chown -R slurm:slurm /var/spool/slurm
sudo mkdir -p /var/run/slurm
sudo chown -R slurm:slurm /var/run/slurm
sudo chmod 777 /var/log/
```

8. 修改`/usr/local/slurm24/etc/slurmdbd.conf`配置项，设置数据库连接参数 , 只需要修改主节点

```ini
PidFile=/var/run/slurm/slurmdbd.pid

StorageHost=10.1.9.109
StoragePort=3306
StoragePass=123456
```

- 修改系统服务参数文件  `/etc/sysconfig/slurmd`, 主节点需要修改`/etc/sysconfig/slurmctld`,`/etc/sysconfig/slurmdbd`，`/etc/sysconfig/slurmrestd`，增加两行

```bash
PATH=$PATH:/usr/local/slurm24/bin:/usr/local/slurm24/sbin:/usr/local/munge/bin
LD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib64:/usr/local/munge/lib64:/usr/local/slurm24/lib64:$LD_LIBRARY_PATH
```

- 创建系统服务（需要先切换到slurm解压目录的etc目录下）

```bash
sudo cp slurmd.service /usr/lib/systemd/system/
#以下三条命令只需要主节点执行
sudo cp slurmctld.service /usr/lib/systemd/system/
sudo cp slurmdbd.service /usr/lib/systemd/system/
sudo cp slurmrestd.service /usr/lib/systemd/system/

sudo systemctl daemon-reload
#主节点执行下面四条
sudo systemctl start slurmctld
sudo systemctl start slurmdbd
sudo systemctl start slurmrestd
sudo systemctl start slurmd

#工作节点只需要执行下面一条
sudo systemctl start slurmd

ps -ef|grep slurm  # 检查是否启动成功
```



##  验证安装


```bash
sudo su - slurm
sinfo 
srun -n 2 hostname
```

- sinfo 结果样例


```bash
[slurm@node112 bin]$ ./sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
debug*       up   infinite      3   idle node[112,113,114]
```

- srun结果样例


```bash
[slurm@node112 ~]$ srun -n 2 hostname
node112
node112
```



## 打包安装

<note>
  编译安装较为复杂，通常编译安装好一个环境以后，其他节点的安装通过打包安装更为简单
</note>

- 将已经编译安装好的 munge和slurm打包，在编译安装主机上执行以下命令：

```bash
cd /usr/local

sudo tar -cvf /tmp/munge.tar munge
sudo tar -cvf /tmp/slurm.tar slurm
sudo gzip /tmp/munge.tar
sudo gzip /tmp/slurm.tar
```

- munge.tar.gz 和slurm.tar.gz 复制到打包安装部署主机上的 `/usr/local` 目录下。然后解压。

```bash
cd /usr/local
sudo tar -xvf munge.tar.gz
sudo tar -xvf slurm.tar.gz
```

- 创建用户

```bash
sudo groupadd munge
sudo useradd  -g munge -s /bin/bash munge
sudo groupadd slurm
sudo useradd  -g slurm -s /bin/bash slurm
```

- 配置和启动，从已安装节点复制文件到打包安装节点的同样目录下：


```bash
/etc/sysconfig/slurmd
/usr/lib/systemd/system/slurmd.service
/usr/lib/systemd/system/munge.service
```

- 设置服务目录权限，相关服务均以自身用户启动，不设置权限会有大量报错。


```bash
cd /usr/local
sudo chown -R munge:munge munge
sudo chown -R slurm:slurm slurm

```

- 创建系统服务，并启动

```bash
sudo systemctl daemon-reload

sudo systemctl start munge
sudo systemctl start slurmd

ps -ef|grep munge  # 检查是否启动munge成功
ps -ef|grep slurm  # 检查是否启动slurm成功
```

- 执行完成后，再次执行验证安装



##  登录节点安装

- 将其他节点的`/usr/local/munge` 和 `/usr/local/slurm` 复制到登录节点的`/usr/local`目录下

- 创建munge用户

```bash
sudo groupadd munge -g 601
sudo useradd  -g munge -u 601 -s /bin/bash munge 
cd /usr/local
sudo chown -R munge:munge munge
```

- 部署munge启动脚本，并启动

```bash
sudo cp /usr/local/munge/lib/systemd/system/munge.service /usr/lib/systemd/system/
sudo systemctl daemon-reload
sudo systemctl start munge
```

- 创建slurm用户

```bash
sudo groupadd slurm -g 650
sudo useradd  -g slurm -u 650 -s /bin/bash slurm
cd /usr/local
sudo chown -R slurm:slurm slurm
```

- 修改slurm 用户的 `.bashrc`,

```bash
export PATH=/usr/local/munge/bin:/usr/local/slurm/bin:/usr/local/slurm/sbin:/usr/local/openmpi/bin:$PATH

export PATH=$PATH:/usr/local/slurm/bin:/usr/local/slurm/sbin:/usr/local/munge/bin
export LD_LIBRARY_PATH=/usr/local/munge/lib64:/usr/local/slurm/lib64:$LD_LIBRARY_PATH
```



##  用户管理

为满足多用户使用，需要建立操作系统用户、slurm用户、slurm账户。同时所有slurm租户用户（不包括名称为slurm的管理用户）在slurm的管理节点和工作节点上全部关闭远程登录能力（`usermod -L <username>`）。

- 新增租户用户操作，在slurm管理节点使用slurm用户执行

```bash
#创建slurm租户
sacctmgr add account ccc

#创建一个slurm用户并关联其slurm账户
sacctmgr add user ccc Account=ccc
```

- 在所有机器上执行, 创建操作系统用户组，一般一个租户一个用户组，租户下所有用户都归属该用户组。租户下用户各自建立一个操作系统用户，租户自身需要建立一个默认的操作系统用户。用户的home目录需要设置为共享存储上对应的路径。

```bash
# 创建用户组需要指定组id

groupadd <group name> -g <group id ,该id必须统一指定，保证所有服务器上该gid都一致>

useradd <user name> -u <user id, 该id必须统一指定，保证所有服务器上该uid都一致> -g <group id, 保证gid为该用户归属的租户统一gid> -s /bin/bash -d <用户home目录>
```

- 限制分区用户使用，指定分区给某租户的操作系统group， 非此操作系统group提交的任务无法执行


```bash
scontrol update  PartitionName=foraaa Nodes=node114  AllowAccounts=ccc AllowGroups=ccc  
```

- 修改的用户的 `.bashrc`

```bash
export PATH=/usr/local/slurm/bin:/usr/local/slurm/sbin:$PATH
```