# Kafka Commands Revision

​	Access Kafka's container:

```bash
docker exec -it kafka bash
```

​	Create a topic:

```bash
kafka-topics \
    --bootstrap-server kafka:9092 \
    --topic testTopic \
    --create \
    --partitions 1 \
    --replication-factor 1
```

​	Create a producer:

```bash
kafka-console-producer \
    --broker-list kafka:9092 \
    --topic testTopic
```

​	Create a consumer:

```bash
kafka-console-consumer \
    --bootstrap-server kafka:9092 \
    --topic testTopic
```

​	Create a producer with key-value:

```bash
kafka-console-producer \
    --broker-list kafka:9092 \
    --topic testTopic \
    --property parse.key=true \
    --property key.separator=,
```

​	Create a producer sending a file:

```bash
kafka-console-producer \
    --broker-list kafka:9092 \
    --topic testTopic < file.log
```

​	Create a producer sending a key-value file:

```bash
kafka-console-producer \
    --broker-list kafka:9092 \
    --topic testTopic \
    --property parse.key=true \
    --property key.separator=: < file.log
```
