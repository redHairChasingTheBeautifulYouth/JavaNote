### 数据模型
zookeeper的数据模型和文件系统类似，每一个节点称为：znode.  是zookeeper中的最小数据单元。每一个znode上都可以
保存数据和挂载子节点。 从而构成一个层次化的属性结构

节点特性
- 持久化节点 :节点创建后会一直存在zookeeper服务器上，直到主动删除
- 持久化有序节点:每个节点都会为它的一级子节点维护一个顺序
- 临时节点:临时节点的生命周期和客户端的会话保持一致。当客户端会话失效，该节点自动清理
- 临时有序节点:在临时节点上多勒一个顺序性特性

### 会话

NOT_CONNECTED->CONNECTING->CONNECED->CLOSED
### Watcher
zookeeper提供了分布式数据发布/订阅,zookeeper允许客户端向服务器注册一个watcher监听。当服务器端的节点触发指定事件的时候
会触发watcher。服务端会向客户端发送一个事件通知

watcher的通知是一次性，一旦触发一次通知后，该watcher就失效
### ACL
zookeeper提供控制节点访问权限的功能，用于有效的保证zookeeper中数据的安全性。避免误操作而导致系统出现重大事故。
CREATE /READ/WRITE/DELETE/ADMIN

