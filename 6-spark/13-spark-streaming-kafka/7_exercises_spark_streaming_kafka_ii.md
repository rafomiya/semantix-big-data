# Exercises - Spark Streaming & Kafka II

## Kafka

1. Prepare the environment on Kafka:

    1. Create a topic `topic-kvspark` with `2` partitions and replication factor of `1`.

    ```bash
    kafka-topics.sh \
        --bootstrap-server kafka:9092 \
        --create \
        --topic topic-kvspark \
        --partitions 2 \
        --replication-factor 1
    ```

    2. Insert the following messages on the topic (key, value):

    - `"1, Msg1"`
    - `"2, Msg2"`
    - `"3, Msg3"`

    ```bash
    kafka-console-producer.sh \
        --broker-list kafka:9092 \
        --topic topic-kvspark \
        --property parse.key=true \
        --property key.separator=', '
    # >1, Msg1
    # >2, Msg2
    # >3, Msg3
    ```

    3. Create a consumer on Kafka to read the topic `topic-kvspark`.

    ```bash
    kafka-console-consumer.sh \
        --bootstrap-server kafka:9092 \
        --topic topic-kvspark \
        --from-beginning
    # output:
    # Msg1
    # Msg3
    # Msg2
    ```

## Spark

1. Create a consumer in Scala using Spark Streaming to read the topic `topic-kvspark` on the Kafka cluster `kafka:9092`.

```scala
import org.apache.kafka.clients.consumer.ConsumerRecord
import org.apache.kafka.common.serialization.StringDeserializer
import org.apache.spark.streaming.{Seconds, StreamingContext}
import org.apache.spark.streaming.kafka010._
import org.apache.spark.streaming.kafka010.LocationStrategies.PreferConsistent
import org.apache.spark.streaming.kafka010.ConsumerStrategies.Subscribe

val ssc = new StreamingContext(sc, Seconds(2))

val kafkaParams = Map[String, Object](
    "bootstrap.servers" -> "kafka:9092",
    "key.deserializer" -> classOf[StringDeserializer],
    "value.deserializer" -> classOf[StringDeserializer],
    "group.id" -> "exercises_ii",
    "auto.offset.reset" -> "earliest",
    "enable.auto.commit" -> (false: java.lang.Boolean)
)

val topics = Array("topic-kvspark")

val dstream = KafkaUtils.createDirectStream[String, String](
    ssc,
    LocationStrategies.PreferConsistent,
    ConsumerStrategies.Subscribe[String, String](topics, kafkaParams)
)
```

2. Visualize the topic with the following informations.

- Topic's name
- Partition
- Key
- Value

```scala
val infos = dstream.map(x => (
    x.topic,
    x.partition,
    x.key,
    x.value
))

infos.print()
// output:
// -------------------------------------------                                     
// Time: 1650779164000 ms
// -------------------------------------------
// (topic-kvspark,0,2,Msg2)
// (topic-kvspark,1,1,Msg1)
// (topic-kvspark,1,3,Msg3)
```

3. Save the topic on the directory `hdfs://namenode:8020/user/rafael/kafka/dstreamkv`.

```scala
dstream.saveAsTextFiles("/user/rafael/kafka/dstreamkv")

ssc.start()
```


