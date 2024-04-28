## Kafka command linen
To execute command line script from kafka container `docker <container-id> exec kafka <command --with=arguments>`

If running `command.sh` do not work, the image must have the kafka command line arguments under bin directory (that is without .sh extension)

### Creating a Kafka Topic
```
kafka-topics.sh --create --topic test_topic --partitions 1 --replication-factor 1 --bootstrap-server kafka:9092
```

### Consume messages
```
kafka-console-consumer.sh --topic test_topic --from-beginning --bootstrap-server kafka:9092
```

### Publish messages
The following command reads data to send from stdin, for commodity you can also ssh into the container to execute it

```
kafka-console-producer.sh --topic test_topic --broker-list kafka:9092
```

## Container configurations

### Kafka
- KAFKA_BROKER_ID — Id number of the broker, if not set a default one will be generated
- KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR — Required when you have less than 3 brokers
- KAFKA_ZOOKEEPER_CONNECT — Url to the zookeeper container
- KAFKA_INTER_BROKER_LISTENER_NAME — Sets the name of the connection for internal communication
- KAFKA_LISTENERS — Sets the ports where the server will receive connections for both OUTSIDE and INTERNAL listeners
- KAFKA_ADVERTISED_LISTENERS — Sets the connection addresses that will be used by the clients

### ZooKeeper
- ZOOKEEPER_SERVER_ID — Unique server ID for all ZooKeeper services
- ZOOKEEPER_CLIENT_PORT — The port to listen for client connections
- ZOOKEEPER_TICK_TIME — The basic time unit in milliseconds used by ZooKeeper.