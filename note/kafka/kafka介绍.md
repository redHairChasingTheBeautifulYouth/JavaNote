### kafka
- 分布式流处理平台。
- 在系统之间构建实时数据流管道。
- 以topic分类对记录进行存储
- 每个记录包含key-value+timestamp
- 每秒钟百万消息吞吐量。


	producer			//消息生产者
	consumer			//消息消费者
	consumer group		//消费者组
	kafka server		//broker,kafka服务器
	topic				//主题,副本数,分区.
	zookeeper			//hadoop namenoade + RM HA | hbase | kafka
	
	
###### 消费者组
将消息发布到一个主题（topic）上，由消费者订阅，将消费者分组，同一组里只能由一个消费者消费这个消息，完美实现队列和发布订阅模式 

##### 安装kafka
- 1.准备zk
- 2.jdk
- 3.tar开
- 4.环境变量

##### 配置 kakfa/config/server.properties
- 配置broker.id--broker.id=202
- 配置log存放--log.dirs=/home/centos/kafka/logs
- 监听端口--PLAINTEXT://:9092
- zookeeper--zookeeper.connect=s201:2181,s202:2181,s203:2181
- 
##### 启动kafka
- a)先启动zk
- b)启动kafka

 [s202 ~ s204]
			$>bin/kafka-server-start.sh config/server.properties
- c)验证kafka服务器是否启动

$>netstat -anop | grep 9092
	



