# 使用方法

1. 将代码 clone 到本地
```
git clone git@github.com:allen0125/docker-hbase.git
cd docker-hbase
```
2. /etc/hosts 中添加以下两项
```
0.0.0.0 hbase-master
0.0.0.0 hbase-region
```
3. 启动
```
docker-compose -f docker-compose-distributed-local.yml up
```
等待所有服务完全启动后，就可以让我们的程序通过监听在本地 2181 端口的 zookeeper 去发现并访问 hbase 了。

Hbase 数据录入

为了验证代码逻辑，我还需要写一些数据到 hbase 中，操作如下：

1. 进入容器

```
docker exec -it hbase-master bash
```
2. 进入 hbase 安装目录

```
cd /opt/hbase-1.2.6/
```

1. 运行 hbase shell
```
bin/hbase shell
```

然后就可以使用SQL语句进行操作了，例如：

```shell
create 'mods_model_storage', 'f'
put 'mods_model_storage','model1','f:model', 'model content1'
put 'mods_model_storage','model2','f:model', 'model content2'

scan 'mods_model_storage'
ROW                     COLUMN+CELL
 model1                 column=f:model, timestamp=1617605399565, value=model content1
 model2                 column=f:model, timestamp=1617605400576, value=model content2
2 row(s) in 0.0330 seconds
```

---
# Original README
[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/big-data-europe/Lobby)

# docker-hbase

# Standalone
To run standalone hbase:
```
docker-compose -f docker-compose-standalone.yml up -d
```
The deployment is the same as in [quickstart HBase documentation](https://hbase.apache.org/book.html#quickstart).
Can be used for testing/development, connected to Hadoop cluster.

# Local distributed
To run local distributed hbase:
```
docker-compose -f docker-compose-distributed-local.yml up -d
```

This deployment will start Zookeeper, HMaster and HRegionserver in separate containers.

# Add Hostname

```
0.0.0.0 hbase-master
0.0.0.0 hbase-region
```

# Distributed
To run distributed hbase on docker swarm see this [doc](./distributed/README.md):

