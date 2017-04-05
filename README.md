# Openstack HA高可用集群部署脚本
## 1 关于脚本
该脚本使用Shell撰写,用于Openstack HA高可用集群的部署，实现了Pacemaker、Galera、RabbitMQ、Openstack、Ceph等集群的半自动化部署，可用于中小型规模Openstack云平台的快速部署。

## 2 部署环境简介

* 软件环境：

CentOS7.2+MariaDB+Openstack-Mitaka+Ceph-Jewel

* 硬件环境：

    * 3个控制节点+3个网络节点+计算节点至少一个
    * 管理网、虚拟机网、存储网三个网段
    * 每个节点具备3张网卡，每个网段的网卡需要统一命名
    * 默认要求要求各节点的三个网段尾数相同
    * 每个节点至少一块独立数据盘，用于Ceph OSD盘（可根据实际需求变更）
    

* 其他

    * 离线Yum安装，需提前准备好软件安装包，本例采用FTP本地安装源
    * root权限安装  
    * 管理网最初需要相互联通
    * 需要配置计算节点（作为Ceph集群的部署节点）到其他各节点之间的SSH
    
## 4 使用说明
* 根据实际环境，配置部署变量初始化0-set-config.sh，设置节点主机名、IP、VIP、网卡信息、网段信息、安装源、OSD磁盘信息、密码信息
```shell
  # vim  0-set-config.sh
```
* 执行all-in-one.sh或按顺序执行每个安装步骤
```shell
  # . all-in-one.sh
```
* 详细说明请阅读个人博客中“[Openstack云平台脚本部署](http://zjzone.cc/?s=Openstack%E4%BA%91%E5%B9%B3%E5%8F%B0%E8%84%9A%E6%9C%AC%E9%83%A8%E7%BD%B2)”系列文章

## 5 更新说明

对之前脚本进行了重构，改进之处主要包括： 

* 命令执行方式：不在通过将脚本文件scp各个节点，然后再执行，统一改成"pssh 命令”执行的方式 
* 并行执行命令：对于比较耗时的操作，尝试改用pssh进行个节点并行执行
* 友好的安装提示：带颜色的提示信息

## 6 问题反馈
如有问题，欢迎留言反馈。

* 个人博客: <http://zjzone.cc>
