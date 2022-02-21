![alt text](https://github.com/MhmtErsy/mongodb-kafka-connector-demo/blob/ccca5c7ee2eeb69709f1415d279c707cb72b3477/plugins/mongodb-kafka-connect-mongodb-1.5.0/assets/mongodb-kafka.png)
# mongodb-kafka-connector-demo
Real Time MongoDB Change Data Capture via Kafka Connect - Demo

 On this demo, I have performed Change Data Capture from MongoDB cloud using Kafka Connect standalone mode


## For Linux
##### - Edit plugin.path on config/connect-standalone.properties

`plugin.path=/home/mehmet/plugins/mongodb-kafka-connect-mongodb-1.5.0/`

##### - Set connection.uri, db, collection on /home/mehmet/plugins/mongodb-kafka-connect-mongodb-1.5.0/etc/MongoSourceConnector.properties

`connection.uri=mongodb+srv://admin:admin@cluster0.shryf.mongodb.net/test`

`database=test`

`collection=iris`
- You can leave blank other fields for now. [Click](https://docs.mongodb.com/kafka-connector/current/kafka-source/#source-connector-configuration-properties "Click") for more information about other configurations.

 ### Run zookeeper & kafka-server on the terminal
 
 `cd /home/mehmet/`
`"$KAFKA_HOME/bin/zookeeper-server-start.sh" $KAFKA_HOME/config/zookeeper.properties`

`"$KAFKA_HOME/bin/kafka-server-start.sh" $KAFKA_HOME/config/server.properties`

### Run Kafka Connect

`"$KAFKA_HOME/bin/connect-standalone.sh" $KAFKA_HOME/config/connect-standalone.properties plugins/mongodb-kafka-connect-mongodb-1.5.0/etc/MongoSourceConnector.properties`

### When you list topic, you will see a topic that named "db.collectionname", so you must see test.iris topic

`"$KAFKA_HOME/bin/kafka-topics.sh" --list --zookeeper localhost:2181`

### When you run a consumer, you can see the change events on records. If your MongoDB collection transactions are inactive, you can insert or delete a few data to observe change events on Kafka topic.

`"$KAFKA_HOME/bin/kafka-console-consumer.sh" --topic test.iris --from-beginning --bootstrap-server localhost:9092`



## For Windows

##### - Edit plugin.path on config/connect-standalone.properties

`plugin.path=C:\mongodb-kafka-connector-demo\plugins\mongodb-kafka-connect-mongodb-1.5.0\`

##### - Edit connection.uri, db, collection on plugins\mongodb-kafka-connect-mongodb-1.5.0\etc\MongoSourceConnector.properties

`connection.uri=mongodb+srv://admin:admin@cluster0.shryf.mongodb.net/test`

`database=test`

`collection=iris`
- You can leave blank other fields for now. [Click](https://docs.mongodb.com/kafka-connector/current/kafka-source/#source-connector-configuration-properties "Click") for more information about other configurations.

 ### Run zookeeper & kafka-server on CMD
`"bin/windows/zookeeper-server-start.bat" config/zookeeper.properties`

`"bin/windows/kafka-server-start.bat" config/server.properties`

### Run Kafka Connect
`"bin\windows\connect-standalone.bat" config\connect-standalone.properties plugins\mongodb-kafka-connect-mongodb-1.5.0\etc\MongoSourceConnector.properties`

### When you list topic, you will see a topic that named "db.collectionname", so you must see test.iris topic
`"bin/windows/kafka-topics.bat" --list --zookeeper localhost:2181`

### When you run a consumer, you can see the change events on records. If your MongoDB collection transactions are inactive, you can insert or delete a few data to observe change events on Kafka topic.

`"bin\windows\kafka-console-consumer.bat" --topic test.iris --from-beginning --bootstrap-server localhost:9092`


