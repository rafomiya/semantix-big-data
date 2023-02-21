# Exercises - Structured Streaming & Kafka

1. Read the Kafka topic `topic-kvspark` in batch mode.

```scala
val kvsparkBatch = spark.
    read.
    format("kafka").
    option("kafka.bootstrap.servers", "kafka:9092").
    option("subscribe", "topic-kvspark").
    load()
```

2. Visualize the topic's schema.

```scala
kvsparkBatch.printSchema
// output:
// root
//  |-- key: binary (nullable = true)
//  |-- value: binary (nullable = true)
//  |-- topic: string (nullable = true)
//  |-- partition: integer (nullable = true)
//  |-- offset: long (nullable = true)
//  |-- timestamp: timestamp (nullable = true)
//  |-- timestampType: integer (nullable = true)
```

3. Visualize the topic with the fields `key` and `value` casted to strings.

```scala
import org.apache.spark.sql.types.StringType

val kvsparkString = kvsparkBatch.select(col("key").cast(StringType), col("value").cast(StringType))
kvsparkString.show(5)
// output:
// +---+-----+                                                                     
// |key|value|
// +---+-----+
// |  1| Msg1|
// |  3| Msg3|
// |  2| Msg2|
// +---+-----+
```

4. Read the Kafka topic `topic-kvspark` in streaming mode.

```scala
val kvsparkStream = spark.
    readStream.
    format("kafka").
    option("kafka.bootstrap.servers", "kafka:9092").
    option("subscribe", "topic-kvspark").
    load()
```

5. Visualize the topic's schema in streaming.

```scala
kvsparkStream.printSchema
// output:
// root
//  |-- key: binary (nullable = true)
//  |-- value: binary (nullable = true)
//  |-- topic: string (nullable = true)
//  |-- partition: integer (nullable = true)
//  |-- offset: long (nullable = true)
//  |-- timestamp: timestamp (nullable = true)
//  |-- timestampType: integer (nullable = true)
```

6. Alter the topic in streaming with the field `key` and `value` casted to string.

```scala
val kvsparkStreamString = kvsparkStream.withColumn("key", col("key").cast(StringType)).withColumn("value", col("value").cast(StringType))
kvsparkStreamString.printSchema
// output:
// root
//  |-- key: string (nullable = true)
//  |-- value: string (nullable = true)
//  |-- topic: string (nullable = true)
//  |-- partition: integer (nullable = true)
//  |-- offset: long (nullable = true)
//  |-- timestamp: timestamp (nullable = true)
//  |-- timestampType: integer (nullable = true)
```

7. Save the topic in streaming on the topic `topic-kvspark-output` each 5 segundos.

​	Creating the topic through Kafka:

```bash
kafka-topics.sh \
    --bootstrap-server kafka:9092 \
    --topic topic-kvspark-output \
    --create \
    --partitions 1 \
    --replication-factor 1
```

​	Saving into the new topic, each 5 seconds:

```scala
import org.apache.spark.sql.streaming.Trigger


kvsparkStreamString.
    writeStream.
    format("kafka").
    option("kafka.bootstrap.servers", "kafka:9092").
    option("topic", "topic-kvspark-output").
    option("checkpointLocation", "/user/rafael/kafka_checkpoint").
    trigger(Trigger.Continuous("5 seconds")).
    start()
```

​	Producing data through Kafka:

```bash
kafka-console-producer.sh --broker-list kafka:9092 --topic topic-kvspark --property parse.key=true --property key.separator=,
# >1,test message
2,test 2
3,test3
4,rafael
5,sinner
6,rafael
```

​	Verifying the saved data through a Spark batch reading:

```scala
val kvsparkOutput = spark.read.format("kafka").option("kafka.bootstrap.servers", "kafka:9092").option("subscribe", "topic-kvspark-output").load()

val kvsparkOutputString = kvsparkOutput.select(col("key").cast(StringType), col("value").cast(StringType))

kvsparkOutputString.show
// output:
// +---+------------+
// |key|       value|
// +---+------------+
// |  1|test message|
// |  2|      test 2|
// |  3|       test3|
// |  4|      rafael|
// |  5|      sinner|
// |  6|      rafael|
// +---+------------+
```

8. Save the topic on the directory `hdfs://namenode:8020/user/rafael/kafka/topic-kvspark-output`.

```scala
val kvsparkStreamOutput2 = kvsparkStreamString.
    writeStream.
    format("csv").
    option("checkpointLocation", "/user/rafael/kafka-checkpoint2").
    option("path", "/user/rafael/kafka/topic-kvspark-output").
    start()
```

​	Verifying the saved data on HDFS:

```bash
hdfs dfs -ls /user/rafael/kafka/topic-kvspark-output/
# Found 5 items
# drwxr-xr-x   - root supergroup          0 2022-04-25 04:47 /user/rafael/kafka/topic-kvspark-output/_spark_metadata
# -rw-r--r--   2 root supergroup         54 2022-04-25 04:47 /user/rafael/kafka/topic-kvspark-output/part-00000-28c9ae6f-1941-4c80-88c6-71d6ed96b3c1-c000.csv
# -rw-r--r--   2 root supergroup        108 2022-04-25 04:47 /user/rafael/kafka/topic-kvspark-output/part-00000-69ff3bdc-b4c5-47cf-86f4-9f393c040007-c000.csv
# -rw-r--r--   2 root supergroup          0 2022-04-25 04:44 /user/rafael/kafka/topic-kvspark-output/part-00000-97989320-d43c-4aca-9cf0-f11c4564cfd4-c000.csv
# -rw-r--r--   2 root supergroup        167 2022-04-25 04:47 /user/rafael/kafka/topic-kvspark-output/part-00001-f85da4e6-6864-4424-a307-7e83ec76a45d-c000.csv

hdfs dfs -cat /user/rafael/kafka/topic-kvspark-output/part-00001-f85da4e6-6864-4424-a307-7e83ec76a45d-c000.csv
# 1,test message,topic-kvspark,1,5,2022-04-25T04:47:48.082Z,0
# 3,test3,topic-kvspark,1,6,2022-04-25T04:47:48.101Z,0
# 4,rafael,topic-kvspark,1,7,2022-04-25T04:47:48.102Z,0
```
