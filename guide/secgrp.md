# 安全组

NVMe型MongoDB实例支持安全组功能。 当用户账号开通安全组功能后， 在支持安全组的地域创建集群时， 您可以选择是否绑定安全组。如果当前安全组规则无法满足需求， 您也可以创建新的安全组。**同一个集群最多绑定5个安全组。**

![image](/images/guide/secgroup_1.png)

## 管理安全组

- 您可以通过集群的详情页查看当前集群绑定的安全组，也可以在 “私有网络 UVPC” 下的安全组页面查看当前安全组规则绑定了哪些集群。

### 通过 “集群详情页” 管理

在集群列表页面点击“详情”按钮后选择“安全规则”标签页， 查看当前集群使用的安全组。
您也可以在此页面管理安全组。

![image](/images/guide/secgroup_2.png)

#### 查看安全组详情

点击列表页“操作“栏下的“详情“按钮， 可以查看对应的安全组详情。

![image](/images/guide/secgroup_3.png)
![image](/images/guide/secgroup_4.png)

在安全组详情页的具体操作请参考 [安全组操作手册](https://docs.ucloud.cn/vpc/guide/secgroup)

#### 关闭安全组

如果您需要关闭当前集群的安全组功能。 您可以点击“关闭安全组”按钮后，确定后将解除当前集群绑定的全部安全组。

**注意**： 该操作不可逆， 一旦关闭安全组之后，无法再次开启。

![image](/images/guide/secgroup_5.png)

#### 配置安全规则

点击“配置安全规则”按钮， 可以修改当前绑定的安全组， 调整安全组的优先级等。

![image](/images/guide/secgroup_6.png)

#### 创建安全组

您也可以在当前页面点击“创建安全组”， 新建安全组后绑定到当前的集群。

![image](/images/guide/secgroup_7.png)

### 通过 “私有网络 UVPC” 管理

在网站首页产品列表中找到“私有网络 UVPC”点击进入

![image](/images/secgroup/secgroup-list.png)

点击操作栏的“详情”按钮可查看当前此安全组绑定的资源以及安全规则。

![image](/images/secgroup/secgroup-detail.png)

## 补充说明

- 扩缩容：扩容的节点会默认加入到集群当前绑定的安全组中。

## 更多安全组功能说明

请参考[安全组功能文档](https://docs.ucloud.cn/vpc/introduction/secgroup)
