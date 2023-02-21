# Exercises - Spark Streaming & Kafka II

## Kafka

1. Prepare the environment on Kafka:

    1. Create the topic `topic-spark` with `1` partition and replication factor of `1`.

    ```bash
    kafka-topics.sh \
        --bootstrap-server kafka:9092 \
        --topic topic-spark \
        --create \
        --partitions 1 \
        --replication-factor 1
    ```

    2. Insert the following messages on the topic:

    - `"Msg1"`
    - `"Msg2"`
    - `"Msg3"`

    ```bash
    kafka-console-producer.sh \
        --broker-list kafka:9092 \
        --topic topic-spark
    # >Msg1
    # >Msg2
    # >Msg3
    ```

    3. Create a consumer on Kafka to read the topic `topic-spark`.

    ```bash
    kafka-console-consumer.sh \
        --bootstrap-server kafka:9092 \
        --topic topic-spark \
        --from-beginning
    # output:
    # Msg1
    # Msg2
    # Msg3
    ```
    
## Spark

1. Create a consumer on Scala using Spark Streaming to read the topic `topic-spark` on the Kafka cluster `kafka:9092`.

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
    "group.id" -> "exercises_i",
    "auto.offset.reset" -> "earliest",
    "enable.auto.commit" -> (false: java.lang.Boolean)
)

val topics = Array("topic-spark")

val dstream = KafkaUtils.createDirectStream[String, String](
    ssc,
    LocationStrategies.PreferConsistent,
    ConsumerStrategies.Subscribe[String, String](topics, kafkaParams)
)
```

2. Visualize the topic with the following informations:

- Topic's name
- Partition
- Value

```scala
val infos = dstream.map(x => (
    x.topic,
    x.partition,
    x.value
))

infos.print()
// output:
// -------------------------------------------                                     
// Time: 1650750610000 ms
// -------------------------------------------
// (topic-spark,0,Msg1)
// (topic-spark,0,Msg2)
// (topic-spark,0,Msg3)
```

3. Save the topic on the directory `hdfs://namenode:8020/user/rafael/kafka/dstream`.

```scala
infos.saveAsTextFiles()
```

​	Output:

```
-------------------------------------------
Time: 1650751244000 ms
-------------------------------------------
(topic-spark,0,Msg1)
(topic-spark,0,Msg2)
(topic-spark,0,Msg3)

...

-------------------------------------------
Time: 1650751362000 ms
-------------------------------------------
(topic-spark,0,Msg4)

-------------------------------------------
Time: 1650751364000 ms
-------------------------------------------
(topic-spark,0,Msg5)

-------------------------------------------
Time: 1650751366000 ms
-------------------------------------------
(topic-spark,0,Msg6)

-------------------------------------------
Time: 1650751368000 ms
-------------------------------------------

-------------------------------------------
Time: 1650751370000 ms
-------------------------------------------
(topic-spark,0,Test1)

-------------------------------------------
Time: 1650751372000 ms
-------------------------------------------
(topic-spark,0,Test2)
(topic-spark,0,Test3)
```
