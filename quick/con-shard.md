# 如何连接分片集

## 介绍
分片集模式可以将数据分布于多台机器上。MongoDB支持通过分片进行横向扩展。横向扩展包括将系统数据集和负载划分到多个服务器上，根据需要添加额外的服务器来增加容量。扩大部署的容量只需要根据需要添加额外的服务器，这可能比单机的高端硬件的总成本低。MongoDB分片集支持超大的数据集和高吞吐量操作, 具有大数据量、高扩展性、高性能、灵活数据模型、高可用性特性。

## 格式
一般的客户端，可以使用MongoDB URL的模式进行分片集连接。标准的URI连接协议如下:
```http
mongodb://[username:password@]host1[:port1][,...hostN[:portN]][/[database][?options]]
```

## 连接示例

假设控制台上有这么一个分片集：

![image](/images/quick/list3.png)

列表中访问地址即 mongos 节点地址,  是`10.60.219.92:27017`

因此，我们可以得到这个分片集的连接模式的MongoDB URL为：
```http
mongodb://10.60.219.92:27017/
```

连接的截图如下图所示：

![image](/images/quick/connectShard.png)

在 url 中指定用户名和密码连接:

```http
mongodb://root:thisispassword@10.60.219.92:27017/admin
```

截图如下：
  
![image](/images/quick/connectReplicaSet2.png)

“读写分离”:

```http
mongodb://root:thisispassword@10.60.219.92:27017/admin?readPreference=secondary
```

## 参考文档：

* https://www.mongodb.com/docs/v3.6/reference/connection-string/#standard-connection-string-format
* https://www.mongodb.com/docs/v3.6/reference/connection-string/#read-preference-options

