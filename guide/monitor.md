# 告警管理

## 资源列表

[资源监控入口](https://console.ucloud.cn/umon/overview)

![image](/images/monitor/enter.png)

在资源监控列表中，提供了基本的监控数据的展示，通过页面左上角资源类型来确定所需要查看的资源，并可通过筛选框对所选的资源类型进行筛选。
在资源类型中选择 “云数据库 MongoDB UDB （NVMe）” 即可筛选出 MongoDB(NVMe)所有节点的资源列表。

![image](/images/monitor/list.png)

注意: 由于 MongoDB(NVMe) 无论是副本集还是分片集都是集群模式, 即集群中含有多个可用的节点, 而每个节点的监控是单独进行的, 因此这里展示的是所有的具体的节点资源, 而不是集群的资源名称。

每个节点的名称可以在 MongoDB "详情"中找到

![image](/images/monitor/detail.png)

![image](/images/monitor/detail_2.png)

部分节点只是虚拟节点(如下图红色框中), 所以实际在资源监控中并不会展示。

![image](/images/monitor/node.png)

副本集中所有子节点都是“真实节点”。

分片集中配置节点, 路由节点均是"真实节点". 数据分片中每个具体的数据节点是"真实节点"。

对于“真实节点“, 可以复制其名称, 在资源监控列表中搜索到。

![image](/images/monitor/search.png)

## 数据视图

点击资源列表中的“数据视图”按钮，即可进入所选资源的详细数据视图页面。

![image](/images/monitor/view_1.png)

![image](/images/monitor/view_2.png)

## 对比图表

在资源监控页面中，除了“资源列表”标签外，还提供了多个资源的“对比图表”功能，用于对多个资源的某监控指标视图进行对比方式的查看。

## 管理告警模版

点击右侧中“告警模版”选项, 即可对当前告警模版进行管理。 点击 “创建模版” 即可对某个资源类型创建新的告警模版。

![image](/images/monitor/template.png)

要创建 MongoDB(NVMe) 对应的告警模版, 类型中要选择对应的产品名称, 这里是“云数据库 MongoDB UDB （NVMe）”,模版的创建可以从现有模版导入, 这时候会将原有模版的告警规则复制到当前新创建的模版中,
也可以选择不导入, 将创建空白的模版, 可以自己再添加新的告警规则。

![image](/images/monitor/create_template.png)

点击创建之后, 会进入告警模版的详情页, 点击左上角的“添加规则”, 会出现多种可选的告警规则, 根据实际需求添加自己需要关注的告警项。一个模版可以添加多个告警规则。

![image](/images/monitor/new_template.png)

规则添加后, 需要对该规则进行编辑, 比如这里填写之后的效果就是在3次探测周期中, 连续3次出现磁盘使用率大于等于100%, 即会向对应的通知组中的人员发送相应的告警信息。

![image](/images/monitor/new_template_2.png)

## 设置告警

选择资源，并点击“管理”以便对对应的资源所绑定的告警模板进行管理。

![image](/images/monitor/alert_manger.png)

选择设置之后, 会出现“告警管理”弹窗, 可以选择相应告警模版绑定到当前的资源, 如果当前告警模版列表中没有满足要求的, 可以自己创建行的告警模版, 或者对已有的告警模版进行编辑改动。
注意: 编辑已经的告警模版会影响到所有已绑定该告警模版的资源。

![image](/images/monitor/manger.png)

点击确定即将该告警模版应用到该资源上, 当监控到该资源触发模版中的相应告警规则之后, 即会发送短信或者邮件的告警信息(取决于通知组的告警方式设置)。

## 更多

更多资源监控相关的内容, [点击查看](https://docs.ucloud.cn/umon/README)。
