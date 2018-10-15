### 命令操作
-  create [-s] [-e] path data acl

-s 表示节点是否有序

-e 表示是否为临时节点

默认情况下，是持久化节点

- get path [watch]

获得指定 path的信息

- set path data [version]

修改节点 path对应的data

乐观锁的概念

数据库里面有一个 version 字段去控制数据行的版本号

- delete path [version]

删除节点

### stat信息
```
cversion = 0       子节点的版本号
aclVersion = 0     表示acl的版本号，修改节点权限
dataVersion = 1    表示的是当前节点数据的版本号

czxid    节点被创建时的事务ID
mzxid   节点最后一次被更新的事务ID
pzxid    当前节点下的子节点最后一次被修改时的事务ID

ctime = Sat Aug 05 20:48:26 CST 2017
mtime = Sat Aug 05 20:48:50 CST 2017




cZxid = 0x500000015
ctime = Sat Aug 05 20:48:26 CST 2017
mZxid = 0x500000016
mtime = Sat Aug 05 20:48:50 CST 2017
pZxid = 0x500000015
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0   创建临时节点的时候，会有一个sessionId 。 该值存储的就是这个sessionid
dataLength = 3    数据值长度
numChildren = 0  子节点数
```