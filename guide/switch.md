# 主备切换

当某个节点发生故障时，高可用系统会自动触发主备切换，保障整体的可用性。同时您也可以手动触发副本集的主备切换功能。

## 一键切换主备

您可以在控制台列表页或者集群概览中触发副本集的"主备切换"功能。

![image](/images/manage/switch_1.png)

![image](/images/manage/switch_2.png)

点击后，出现弹窗提示如下：

![image](/images/manage/switch_3.png)

确认风险后，点击确定集群即进入“主备切换中”状态，当集群状态转变为运行中时，说明切换成功。

![image](/images/manage/switch_4.png)

### 指定节点提升为主节点

用户可以在集群概览的“节点信息”列表页将某个节点“提升为主节点”。

![image](/images/manage/switch_5.png)

点击后，出现弹窗提示如下：

![image](/images/manage/switch_6.png)

确认风险后，点击确定集群即进入“主备切换中”状态， 当集群状态转变为运行中且主节点为指定节点时，说明切换成功。

![image](/images/manage/switch_4.png)
