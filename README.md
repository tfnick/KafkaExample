Kafka使用示例

----------

#### 容器化启动kafka + zookeeper

docker-compose up

#### 容器化查询kafka topic

1， 查看zookeeper内网地址

```shell
docker ps
```
获取zookeeper容器id

```shell
docker inspect ZK容器ID
```

进入kafka容器执行：
```shell
/opt/bitnami/kafka/bin/kafka-topics.sh --list --zookeeper ZK_IP:2181
```

查看kafka默认配置

/opt/bitnami/kafka/config/server.properties

```properties
broker.id=1
listeners=PLAINTEXT://1.2.1.173:9093
num.network.threads=32
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600
log.dirs=/opt/appdata/kafka-data
# default partitions for new topic
num.partitions=1
num.recovery.threads.per.data.dir=1
log.retention.hours=120
log.retention.bytes=128849018880
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
zookeeper.connect=zk1:2181,zk2:2181,zk3:2181/kafka
zookeeper.connection.timeout.ms=6000
delete.topic.enable=true
# allow to create topic if not exsits
auto.create.topics.enable=false
```










------

#Kafka 0.8.2.2示例
 - [Producer示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.8.2.2/src/main/java/com/jasongj/kafka/ProducerDemo.java) 
 - [HashPartitioner示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.8.2.2/src/main/java/com/jasongj/kafka/HashPartitioner.java) 实现HashPartitioner从而保证key相同的消息被发送到同一个Partition
 - [RoundRobinPartitioner示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.8.2.2/src/main/java/com/jasongj/kafka/HashPartitioner.java) 提供RoundRobin消息路由算法，实现Load balance
 - [High Level Consumer示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.8.2.2/src/main/java/com/jasongj/kafka/DemoHighLevelConsumer.java) 通过High level API中的consumer group实现group内的消息单播和group间的消息广播
 - [Low Level Consumer示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.8.2.2/src/main/java/com/jasongj/kafka/DemoLowLevelConsumer.java) 使用Low level API可实现精确的消息消费控制

#Kafka 0.10.1.0示例
 - [Producer示例](https://github.com/habren/KafkaExample/tree/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/producer) Producer支持send callback
 - [Partitioner示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/producer/HashPartitioner.java) Partitioner接口与旧版本相比有所区别，可以实现更多语义的消息路由/消息分发
 - [Consumer示例](https://github.com/habren/KafkaExample/tree/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/consumer) Kafka 0.10.*版本中新的Consumer使用同一套API同时实现0.8.*及以前版本中的High Level API及Low Level API
 - [Stream Low Level Processor API示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/stream/WordCountProcessor.java) 
 - [Stream Topology示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/stream/WordCountTopology.java) 使用Kafka Stream的Low-level Processor API实现word count
 - [Stream DSL示例](https://github.com/habren/KafkaExample/blob/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/stream/WordCountDSL.java) 通过Kafka Stream的DSL API实现word count功能
 - [Purchase Analysis](https://github.com/habren/KafkaExample/blob/master/demokafka.0.10.1.0/src/main/java/com/jasongj/kafka/stream/PurchaseAnalysis.java) 如何使用KStream与KTable Join，如何创建自己的Serializer/Deserializer和Serde，以及如何使用Kafka Stream的Transform和Kafka Stream的Window
