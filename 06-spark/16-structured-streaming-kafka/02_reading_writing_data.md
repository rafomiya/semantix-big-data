# Reading and Writing Data

## Reading From Topics

​	Creating Kafka Source for batch queries:

```python
batch_df = spark \
    .read \
    .format("kafka")  # as if it was only another data type, such as csv or json \
    .option("kafka.bootstrap.servers", "host1:port1,host2:port2") \
    .option("subscribe", "topic1") \
    .load()
```

​	Creating Kafka Source for streaming queries:

```python
stream_df = spark \
    .readStream \
    .format("kafka")  # as if it was only another data type, such as csv or json \
    .option("kafka.bootstrap.servers", "host1:port1,host2:port2") \
    .option("subscribe", "topic1") \
    .option("startingOffsets", "earliest") \
    .load()
```

​	Visualizing the key and value of a Kafka event: note that the key and value fields are binary, so we need to cast them to `StringType`.

```python
stream_df.printSchema()
# root
#  |-- key: binary (nullable = true)
#  |-- value: binary (nullable = true)
#  |-- topic: string (nullable = true)
#  |-- partition: integer (nullable = true)
#  |-- offset: long (nullable = true)
#  |-- timestamp: timestamp (nullable = true)
#  |-- timestampType: integer (nullable = true)

infos = stream_df.select(col("key").cast(StringType()), col("value").cast(StringType()))
infos.writeStream.format("console").start()
```

## Writing to Topics

​	Writing data from a dataframe/dataset to a topic:

```python
kafka_df.writeStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "host1:port1,host2:port2") \
    .option("topic", "topic2") \
    .trigger(Trigger.Continuous("1 second"))  # optional config that adds the trigger functionality* \
    .start()
```

​	The trigger functionality is basically a way of delaying the send of the data from a Spark dataframe/dataset to the specified Kafka topic. It will delay the specified time on the parameter. Since Spark 2.3, it is a "experimental" feature.


​	Writing data in batch from a dataframe/dataset to a topic:

​	The `value` field is optional, and the `key` field is mandatory. It is also mandatory that these are the names of the columns, so you may need to rename them with the `withColumnRenamed()` method.

```python
df \
    .withColumnRenamed("id", "key") \
    .withColumnRenamed("name", "value") \
    .write \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "host1:port1,host2:port2") \
    .option("topic", "topic2") \
    .save()
```
