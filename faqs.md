# FAQs


## MongoDB实例功能和开源MongoDB有区别吗？

MongoDB实例和原生MongoDB完全一致。

## MongoDB的安全性如何？

### 访问安全性

MongoDB实例仅支持通过云主机进行内网登陆且按账户进行隔离，因此仅有同一账户的云主机能够对MongoDB实例进行登录。

MongoDB实例是强制鉴权的，只能通过认证的。

### 数据安全性

所有的MongoDB实例的数据文件所存放的RSSD云盘， RSSD云盘提供数据保护。

MongoDB实例提供自动备份功能， 在指定的时间自动数据备份，同时也提供了手工备份功能，以便用户能够在特定时间点主动对数据进行备份。

MongoDB集群数据三副本存储， 提供冗余保护。

## 如何备份与恢复？

MongoDB实例支持手动备份，用户可以保存某些关键时间点的重要数据备份，当前手工备份的允许保留个数为3个，如果超过3个，会自动删除最早的手动备份。创建手动备份时，用户只需要输入备份名称，后台会立刻开始进行备份工作。

备份可以下载至本地或云主机。

如果要恢复MongoDB实例，建议用户先将备份文件下载至本地，由专业人员确认无误后导入MongoDB实例中，以规避数据风险。


## 如何使用鉴权？

从数据安全性和可维护等角度，MongoDB实例是强制鉴权的，所有实例均采用keyfile认证，等效于auth=true。MongoDB实例的管理员账号和密码是申请时所填写的管理员用户名和密码。

MongoDB实例统一使用keyfile

    ymSs/7YgMlxlMMTR9K3B6eKyopWD98MX1KIuySyI8Kk1Coqw1sYZp2Nh4nN5yrul+0J21pIpNOzXU3Mbbl2zihF/qMEkofAWJPeORzZd2VR0c2rwHG4xxuxNRFOK3BSTTSIyAgMfnBVTPwC671E18SJi3r/RohfGxy8NveipsZCqTTRDVcGXKqFf4i3vBRLXil+it1oxPb63ayjYJ7Uz1piVQQRtHlD+KzUEaTzhl/CW9Da8xhq1Lm2bxNUWov/ltDfJSyke+a+a1OlbpGTYwD5WeYINbGYYbJMpC1P6ELCQ2kD1c/Dyae7WNLcDO3ICJSOvGigKIGo3om5M8CeiUJ/xHA67RkJak2idSlXOopIEdjjAxtFRPWaF8jEoMgtOSty2OQMBpBYDYcwgRRFL8+fQQvHd1c6sQoXUoN1JbBqhtNxpvlm05keinIP9Al+EeIA1itZjUBcjC5zZgAAPHbXe803TosCupq/jS2W6K8MBEOUg+42u4r8g4Sp2LKdbqqdza1PlBHFQmExSz2pAN61DwZPKjMlBArlCpa5Kk/44DzOc9Lc3bW51AdieG5xFad6d9qS0LLFFeG4tB5HcbUCCKWkVdUM5ocCb0TTRfJ2KNTRaJUTfKq4WLCe1zrIeHCvQIbKVJLgyo/3HHgse331daqVRm+rAAPWwgXVKbo/+XfYkS28ftDMOA6spIN1Vsba+UGdLjGFiq40xLSCA5z0RvB88oYouuyw16VAQuv1JzUk4tzZ9f5Snr1MlyI5rrjO6DZeDT3WYOK9TGRDshWHuVjDCtvDTYPjACy0Jy4Uhikze+pz9gAUbmJNUeU14CZb5EA1/mkICjpbIJigG1lduERa1g5OFv3cS4UIyh8V/zE11rjVdLva0Fq58w713kO6t40xG2QWbpTX/D5VWVH7j0Uq4QX3xSUPvCzIrcGXV0whPRM93BGCgEZVIkdOfDv2+VGDMDmL3mWyJ8/ysjaN1VOnf

## 如何访问MongoDB实例？

申请MongoDB实例后会获取一个IP和Port。

### 命令行操作

登录云主机，在命令行中输入：

    mongo --host $ip --port $port --authenticationDatabase $db --username $admin --password $admin_passwd

例如：

    mongo --host 10.4.12.80 --port 27017 --authenticationDatabase admin --username root --password root

或者：

    mongo $ip:$port/$db -u $admin -p $admin_passwd

例如：

    mongo 10.4.12.80:27017/admin -u root -p root

### API操作

用户可以使用开源的MongoDB API库来连接MongoDB，出于安全性考虑，MongoDB仅能在内网进行访问。

## 如何访问业务MongoDB？

因为在MongoDB安全机制作用下，刚开始用户是无法直连业务db的，否则一直提示无权限，这时需要通过以下步骤：

1、登录到admin库。

2、切换到业务db，如game。

3、使用createUser。

4、使用mongo客户端连接到业务库，如：

    mongo 10.4.12.80:27017/game -u root -p root

MongoDB的2.6版本开始对安全机制做了比较多改进，具体方法可以参见， 注意角色的概念：

<http://docs.mongodb.org/master/reference/method/db.createUser/>


**MongoDB的内存是如何管理？**

MongoDB使用mmap管理内存，内存使用率经常是100%，也有时候经过备份
操作（自动备份和手动备份），内存也会立即升到100%，通常情况下无需担心。内存上升后，通常情况下是不会主动释
放的。

如果是平时的工作载荷，内存使用出现瓶颈，建议是在线升级内存。

**MongoDB的磁盘是如何管理？**

MongoDB采用预分配机制分配大文件用于存放数据，drop、remove、
compact等操作是不会释放磁盘空间的，但是可以使预分配的空间重用。如果磁盘使用率过高，这时候需要注意
是否会100%。如果磁盘空间使用率接近100%，建议采用以下方法克服：

1、升级磁盘；

2、创建secondary，通过复制方式将数据从primary同步到
secondary，这时候secondary的存储空间往往会较小一些，然后执行一次主从切换；

3、修复db，执行db.repairDatabase，这会阻塞住整个实例的读写服务，不建议使用；

## 如何管理和查看慢查询？

在业务库执行db.setProfilingLevel()启动和关闭慢查询，方法参见：

<http://docs.mongodb.org/manual/reference/method/db.setProfilingLevel/>

执行db.getProfilingStatus()查看慢查询设置状态。

执行db.system.profile.find() 查看收集到的慢查询，有助于查询优化的工作。

**怎么查到MongoDB的统计信息?**

统计可以在 MongoDB管理页面看到，包括CPU使用率、内存使用、内存使用率、连接数、各类QPS指标等。

**如何使用mongostat监控？**

mongostat是官方提供的一种监控工具，使用方法是:

    mongostat -h $ip --port $port --authenticationDatabase admin -u $admin -p $admin_password --discover

如:

    mongostat -h 10.4.4.50 --port 27017 --authenticationDatabase admin -u root -p root  --discover

**如何查看副本集属性信息与同步状态？**

使用客户端mongo连接到primary节点，执行命令rs.status()查 看副本集属性，其中“set”字段是副本集的id。

执行命令rs.printReplicationInfo() 查看oplog的使用情况。

使用客户端mongo连接到
secondary节点，执行命令rs.printSlaveReplicationInfo()查看与primary节点的同
步状态，可以看到是否落后primary。

## 利用HAproxy外网访问UDB-MONGO

与使用MySQL-Proxy使UDB-MYSQL能够被外网访问一样，可以通过使用HAproxy来使UDB-MONGO被外网进行访问。

具体流程如下：

    安装HAproxy
    
    # yum install -y haproxy
    
    根据如下内容修改配置文件，默认的配置文件路径： /etc/haproxy/haproxy.cfg 
    
        global
           log         127.0.0.1 local2
           chroot      /var/lib/haproxy
           pidfile     /var/run/haproxy.pid
           maxconn     4000    
           user        haproxy
           group       haproxy
           daemon    
           stats socket /var/lib/haproxy/statsdefaults
        defaults
           log                     global   
           option                  dontlognull
           option http-server-close
           option                  redispatch
           retries                 3
           timeout http-request    10s
           timeout queue           1m
           timeout connect         10s 
           timeout client          1m 
           timeout server          1m
           timeout http-keep-alive 10s
           timeout check           10s
           maxconn                 3000
       listen mongod    
           bind uhost-ip:27017
           mode tcp    
           balance roundrobin
           server mongo1 mongodb-ip:27017
       listen mongo-web    
           bind uhost-ip:28017
           mode http
           balance roundrobin
           server mongo1 mongodb-ip:28017
    
     配置中的uhost-ip为云主机的内网IP，mongodb-ip为UDB-MONGO的内网IP。

重启服务

```
# service haproxy restart
# chkconfig haproxy on
```

在防火墙中开启相应端口

在这个配置中，由于外网客户端需要通过27017和28017端口访问haproxy所在的UHost的机器（参考配置中两行bind语句），请编辑这台UHost机器所属的防火墙配置，放开端口27017和28017的访问限制。

通过公网连接MongoDB

```
# mongo uhost-eip:27017/admin -u root -p
```

公网访问MongoDB的WEB控制台地址：<http:%%//%%uhost-eip:28017>

## 在云主机上使用wget下载云数据库的Log时报错，如何解决？

在云主机上下载云数据云数据库的Log备份时需要在url前后加上双引号。

例：下载地址为：<http://udbbackup.ufile.ucloud.cn/udb-3u022a/>

    wget -O ppp.tgz "http://udbbackup.ufile.ucloud.cn/udb-3u022a/"

\-O 设置本地名称

## 如何修改local库的大小？

一旦DB申请成功后，不再支持修改oplogSize的大小，只支持申请DB之前修改。

如果是普通的sharding
server，我们UDB的默认local库大小是5G。如果您需要设置成指定的大小，可以在新建MongoDB时前，先新建一个自定义配置文件，修改oplogSize大小来设置，并使用该自定义配置文件来创建DB。

如果写操作比较频繁，建议根据申请的磁盘容量适当调大oplogSize的大小。

如果是config server，系统会默认生成一个大概几十M的local库，即使申请DB阶段设置local库大小也无效

## 如何查询MongoDB实例的服务器端版本和其他安装信息？

登陆Mongo shell，运行如下指令查看。

    udb-test:PRIMARY> db.serverBuildInfo()
    {
      "version" : "2.4.9",
      "gitVersion" : "52fe0d21959e32a5bdbecdc62057db386e4e029c",
      "sysInfo" : "Linux ip-10-2-29-40 2.6.21.7-2.ec2.v1.2.fc8xen #1 SMP Fri Nov 20 17:48:28 EST 2009 x86_64 BOOST_LIB_VERSION=1_49",
      "loaderFlags" : "-fPIC -pthread -rdynamic",
      "compilerFlags" : "-Wnon-virtual-dtor -Woverloaded-virtual -fPIC -fno-strict-aliasing -ggdb -pthread -Wall -Wsign-compare -Wno-unknown-pragmas -Winvalid-pch -Werror -pipe -fno-builtin-memcmp -O3",
      "allocator" : "tcmalloc",
      "versionArray" : [2, 4, 9, 0],
      "javascriptEngine" : "V8",
      "bits" : 64,
      "debug" : false,
      "maxBsonObjectSize" : 16777216,
      "ok" : 1
    }


## 如何连接MongoDB云数据库？

### 连接副本集

如果MongoDB采用的是副本集方式，那么连接MongoDB时需要设置一个正确的连接URI，这样后续Primary节点宕机才可以成功的进行漂移，应用层无需变更连接设置，自动具有高可用。各类语言的驱动都支持URI连接。一般副本集连接的URI字符串格式如下，包括账户、密码和副本集各个节点的IP和端口。

    URI: mongodb://user:password@ip1:port1,ip2:port2,…

假如URI的内容如下：

    mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test

那么正确的连接方式是：

    client=MongoClient('mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test')

MongoDB只支持在Primary节点上进行写操作，不过读操作可以有以下几种，客户可以根据自身业务需求选择合适的读取策略。

primary：默认设置，所有的读操作都在Primary节点

primaryPreferred：优先读取Primary节点，Primary不可用的话读取Secondary节点

secondary：所有的读操作都读取Secondary节点

secondaryPreferred：优先读取Secondary，Secondary不可用的情况下读取Primary

nearest：读取网络延迟最低的节点

举个例子，假如需要实现读写分离，即优先读取Secondary节点，连接超时为500ms，那么URI配置如下：

    mongodb://uclouder:edFO09SkdU@10.9.57.241:27017,10.9.40.112:27017,10.9.35.45:27017/test?connectTimeoutMS=500&readPreference=secondaryPreferred

### 连接分片集群

连接到分片集群的方式和连接到普通MongoDB实例的方式完全相同，不过当存在多个mongos实例的情况下，即使URI里写全了mongos实例的IP也无法自动做到mongos本身的高可用和负载均衡，通常这个可以通过搭建HaProxy或者LVS的方式实现。
假设存在三个mongos节点，分别为IP1，IP2，IP3，而HaProxy的代理IP为IP4，采用简单的roundrobin轮询策略，则连接URI举例如下：

    mongodb://uclouder:edFO09SkdU@IP4:27017/test?connectTimeoutMS=500&readPreference=secondaryPreferred
