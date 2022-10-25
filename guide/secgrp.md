# 安全组

NVMe型MongoDB实例支持安全组功能。 当用户账号开通安全组功能后， 在支持安全组的地域创建集群时， 集群会自动加入默认安全组中。 默认安全组定义了全放行的规则， 一个UVPC下所有MongoDB集群共用一个默认安全组。 集群创建成功后用户可修改默认安全组以满足需求。如果用户需要多个安全组，可创建新的安全组并将对应集群加入新安全组实现自定义访问控制。

默认事项：
- 扩缩容：扩容的节点会默认加入到集群当前绑定的安全组中。

## 查看安全组

在网站首页产品列表中找到“私有网络 UVPC”点击进入

![image](/images/secgroup/secgroup-list.png)

点击操作栏的“详情”按钮可查看当前此安全组绑定的资源以及安全规则。

![image](/images/secgroup/secgroup-detail.png)

## 创建/修改安全组

具体操作请参考[安全组操作文档](https://docs.ucloud.cn/vpc/introduction/secgroup)
