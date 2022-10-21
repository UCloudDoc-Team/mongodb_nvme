# 安全组

NVMe型MongoDB实例支持安全组功能。 当用户账号开通安全组功能后， 在支持安全组的地域创建集群时， 集群下所有节点会加入业务侧自定义安全组中。

默认事项：
- 扩缩容：后续集群扩容的节点也会默认加入到业务侧自定义安全组中。

## 查看安全组

在网站首页产品列表中找到“私有网络 UVPC”点击进入

![image](/images/secgroup/secgroup-list.png)

点击操作栏的“详情”按钮可查看当前此安全组绑定的资源以及安全规则。

![image](/images/secgroup/secgroup-detail.png)

## 修改安全组

具体操作请参考[安全组操作文档](https://docs.ucloud.cn/vpc/introduction/secgroup)
