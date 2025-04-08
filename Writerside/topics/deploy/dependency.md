# 依赖安装

<warning>
    所有服务器的slurm相关用户的uid与gid必须完全统一一致，否则会出现使用错误的account提交任务
</warning>



- 所有主机需要将集群内所有主机的ip和hostname关系配置到 `/etc/hosts` 中
- 在所有待安装主机上执行，安装基础包

```bash
sudo yum install -y autoconf  automake libtool openssl-devel libevent-devel bzip2 python3 ncurses-devel 
```

- 在所有待安装主机做时钟同步



## munge安装

- 下载munge地址：https://github.com/dun/munge/releases
- 解压，进入解压目录。执行

```bash
./bootstrap

./configure --prefix=/usr/local/munge \
--sysconfdir=/usr/local/munge/etc \
--localstatedir=/usr/local/munge/local \
--with-runstatedir=/usr/local/munge/run \
--libdir=/usr/local/munge/lib64

make 
sudo make install
```

- 创建用户

```bash
sudo groupadd munge -g 601
sudo useradd  -g munge -u 601 -s /bin/bash munge 
```

- 创建key文件

```bash
sudo mkdir -p /usr/local/munge/run/munge
sudo chown -R munge:munge /usr/local/munge
sudo chmod -R 755 /usr/local/munge/run
sudo su - munge
#  主节点执行如下命令生成，被管节点复制生成的文件 /usr/local/munge/etc/munge/munge.key 到从节点同样目录下
/usr/local/munge/sbin/mungekey   
chmod 600 /usr/local/munge/etc/munge/munge.key
```

- 部署启动脚本

```bash
sudo cp /usr/local/munge/lib/systemd/system/munge.service /usr/lib/systemd/system/
sudo systemctl daemon-reload
sudo systemctl start munge
```



## json库安装

```bash
git clone --depth 1 --single-branch -b json-c-0.15-20200726 https://github.com/json-c/json-c.git json-c
mkdir json-c-build
cd json-c-build
cmake ../json-c
make
sudo make install
```



## http-parser库安装

```bash
git clone --depth 1 --single-branch -b v2.9.4 https://github.com/nodejs/http-parser.git http_parser
cd http_parser
make
sudo make install
```



## yaml库安装

```bash
git clone --depth 1 --single-branch -b 0.2.5 https://github.com/yaml/libyaml libyaml
cd libyaml
./bootstrap
./configure
make
sudo make install
```



## jwt库安装

<note>
   jansson 2.13+
</note>

- 下载 `jansson-2.13`，解压。切换到解压包路径

```bash
./configure --prefix=/usr/local
make -j
sudo make install
```

- 安装`libjwt`

```bash
git clone --depth 1 --single-branch -b v1.12.0 https://github.com/benmcollins/libjwt.git libjwt
cd libjwt
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
autoreconf --force --install
./configure --prefix=/usr/local
make -j
sudo make install
```



## 密钥安装

1. 生成或密钥文件（如果存在可复制）

```bash
dd if=/dev/random of=/var/spool/slurm/statesave/jwt_hs256.key bs=32 count=1
```

2. 设置权限

```bash
chown slurm:slurm /var/spool/slurm/statesave/jwt_hs256.key
chmod 0600 /var/spool/slurm/statesave/jwt_hs256.key
chown slurm:slurm /var/spool/slurm/statesave
chmod 0755 /var/spool/slurm/statesave
```

3. 将密钥路径配置添加到`slurmd.conf`和`slurmdbd.conf`

```bash
AuthAltTypes=auth/jwt
AuthAltParameters=jwt_key=/home/slurm/private.key
```



## openmpi 安装

- 下载hwloc地址：https://github.com/open-mpi/hwloc/releases，解压，进入解压目录


```bash
./configure --prefix=/usr/local/hwloc 
make
sudo make install 
```

- 下载pmix地址：https://github.com/openpmix/openpmix/releases，解压，进入解压目录


```bash
./configure --prefix=/usr/local/pmix --with-libevent=/usr/local/libevent --with-hwloc=/usr/local/hwloc
make
sudo make install  
```

- 下载ucx地址：https://github.com/openucx/ucx/releases，解压，进入解压目录


```bash
./configure --prefix=/usr/local/ucx
make
sudo make install
```

- 下载openmpi地址：https://download.open-mpi.org/release，解压，进入解压目录


```bash
./configure --prefix=/usr/local/openmpi --with-pmix=/usr/local/pmix --with-ucx=/usr/local/ucx --with-hwloc=/usr/local/hwloc --with-libevent
make
sudo make install 
```
