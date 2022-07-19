# 如何通过副本集模式连接?

## 介绍
副本集模式连接指的是把副本集看作一个整体，自动探测现在的主节点并进行连接的模式。这样能够做到，无论现在副本集哪个是主节点，客户端都可以连到正确的节点上，并且切换后不需要额外修改客户端的程序。同时，结合read preference参数，能够做类似写操作在主库进行，读操作在从库进行的”读写分离“功能。

## 格式
一般的客户端，可以使用MongoDB URL的模式进行副本集连接。MongoDB URL的格式是：
```http
mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]
```
其中使用副本集模式连接关键的参数是：replicaSet=xxxx（xxxx指代副本集名称，在控制台的详情页能够获取），只要指定这个参数，并且在IP列表中指定多个副本集节点的IP，就做到了副本集模式连接

## 例子
假设控制台上有这么一个副本集：

![image](/images/quick/rsConnectURL.png)

访问地址一栏可以获取到副本集的URL连接地址。复制后将'****'修改为副本集的密码即可进行连接。

连接的截图如下图所示：

![image](/images/quick/ConnectReplicaset4.png)

副本集连接也可通过参数方式指定连接的用户(-u)，密码(-p)，database(--authenticationDatabase)等，截图如下：

![image](/images/quick/ConnectReplicaset5.png)

## 使用副本集连接模式实现“读写分离”
使用副本集模式的`readPreference`参数能够实现写操作在主库进行，读操作在从库进行的”读写分离“功能。
它有这么几个值：

* `primary`: 读请求全部走primary (secondary节点纯粹是做高可用的容灾使用)：这个是最经典的连接方法，把副本集当作一个纯粹的高可用集群使用，而且肯定能保证读到的数据是最准确的
* `secondary`: 写请求全部走primary，读请求全部走secondary。这个是把副本集作为读写分离集群来使用。他能提高读操作的吞吐（通过添加多个secondary的方法）。但是它的缺点是可能读到的数据和主库是不一致的。所以在对于数据一致性有较高的场景下慎用。
* `primaryPreferred`: 优先走primary，只有少数情况才去secondary读取数据。
* `secondaryPreferred`: 优先走secondary，只有少数情况才去primary读取数据
* `nearest`：根据客户端到各个节点的延时选择节点：如果延时在某个阈值内，随机选择节点；如果所有节点延时在某个阈值外，选择延时最小的

上面的例子中，可以使用下面的方法实现读写分离的效果：
```http
mongodb://root:thisispassword@10.60.52.158:27017,10.60.188.13:27017,10.60.128.181:27017/admin?replicaSet=umongodb-rs-xjnas2un&readPreference=secondary
```

![image](/images/quick/connectReplicaSet3.png)

## 参考文档：

* https://www.mongodb.com/docs/v3.6/reference/connection-string/#replica-set-option
* https://www.mongodb.com/docs/v3.6/reference/connection-string/#read-preference-options

