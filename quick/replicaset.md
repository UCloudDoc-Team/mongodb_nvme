# 一键副本集

1、在控制台选择“云数据库 MongoDB UDB（NVMe）”，点击“创建集群”，即可一键创建 MongoDB 副本集。

![image](/images/quick/createentry.png)

2、在新建集群页面中，选择所在地域及可用区，集群类型选择“副本集”，基础配置可选择：计算规格、硬盘、数据库版本，付费方式和节点个数，系统会根据选择计算费用，页面右侧会显示副本集所需支付费用。

![image](/images/quick/createbasic.png)

新建页面中，网络设置可以选择所属的VPC及子网，以及管理设置实例名称，管理员密码。MongoDB默认端口号为27017，管理员用户名默认为root。为了数据安全，管理员密码需要有一定的复杂度。

![image](/images/quick/createnetwork.png)

3、确认各项选择以及金额，点击确定按钮，进入订单支付页。

![image](/images/quick/createorder.png)

  - 确认支付：进行扣费和资源分配，初始化等操作。

4、支付完成后，页面跳转回MongoDB实例管理页，MongoDB实例进行初始化，待初始化完成之后即可使用。在MongoDB实例管理页，列出了所有MongoDB实例信息，包括实例名称、属性、IP地址、配置、状态、操作等。

![image](/images/quick/list.png)

5、选择某一个MongoDB实例后，点击名称或详情、跳转到其二级详细页面，详情页面可以查看实例信息、监控数据和进行常用数据库管理操作。

![image](/images/quick/repdetail.png)
