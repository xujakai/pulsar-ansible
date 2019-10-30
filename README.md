# pulsar-ansible
使用ansible快速搭建apache pulsar集群

### 一、环境要求

1.ansible  2.8.X

2.firewall、systemctl 

3.ssh免密登陆、[快速配制](https://www.topme.pro/archives/202)

### 二、前提条件

1.zookeeper集群

2.pulsar安装包

### 三、生产环境配制

- 配置集群：inventory/development/group_vars/all.yml  （可选）
- 配制节点：inventory/development/cluster.ini  （必选）

```
# Application Layer Nodes
[clusterBrokerNodes]
192.168.3.9
192.168.3.85
192.168.3.11

[clusterBrokerAddNodes]

[clusterBrokerRemoveNodes]
192.168.3.9
192.168.3.85
192.168.3.11


# Storage Layer Nodes
[clusterBookkeeperNodes]
192.168.3.9
192.168.3.85
192.168.3.11

[clusterBookkeeperAddNodes]

[clusterBookkeeperRemoveNodes]
192.168.3.9
192.168.3.85
192.168.3.11
```

#### 1.创建新集群

ansible-playbook -i inventory/development/cluster.ini clusterSetup.yml

#### 2.重启集群

ansible-playbook -i inventory/development/cluster.ini clusterRollingRestart.yml

#### 3.添加broker

ansible-playbook -i inventory/development/cluster.ini clusterAddBroker.yml

#### 4.添加bookeeper

ansible-playbook -i inventory/development/cluster.ini clusterAddBookkeeper.yml

#### 5.移除Broker＆bookeeper

ansible-playbook -i inventory/development/cluster.ini clusterDecommissionNodes.yml

#### 6.升级集群

ansible-playbook -i inventory/development/cluster.ini clusterUpgrade.yml

### 四、检验集群

bin/pulsar-admin brokers list use