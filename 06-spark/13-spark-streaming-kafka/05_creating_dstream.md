# Creating and visualizing the DStream

## Setup configs

​	To start working with DStreams integrated with Kafka, we need to configure two very important things: Location Strategies and Consumer Strategies.

​	Location Strategies:

- `PreferConsistent`: distribute partitions equally through the available executors (most used).
- `PreferBrokers`: if your executors are on the same host that their Kafka connectors.
- `PreferFixed`: specifies a explicit mapping of partitions for the hosts.

​	Consumer Strategies:

- `Subscribe`: subscribes in a fixed collection of topics.
- `SubscribePattern`: uses a regex to specify the collection of topics.
- `Assign`: specifies a fixed collection of partitions (not very used).

## Creating the DStream

```scala
val ssc = new StreamingContext(sc, Seconds(10))
val topics = Array("testTopic")
val dstream = KafkaUtils.createDirectStream[String, String](
    ssc,
    LocationStrategies.PreferConsistent,
    ConsumerStrategies.Subscribe[String, String](topics, kafkaParams)
)
```

​	Now that the `dstream` is created, we apply RDD operations, such as `map`, to visualize the topic's structure:

```scala
val info_dstream = dstream.map(record => (
    record.topic,
    record.partition,
    record.key,
    record.value
))

info_dstream.print()
```
