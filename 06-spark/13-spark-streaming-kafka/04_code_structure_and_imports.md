# Code Structure & Imports

​	This is how our code will be structured:

```scala​
import <...>


val ssc = new StreamingContext(<...>)
val kafkaParams = Map[String, Object](<...>)
val dstream = KafkaUtils.createDirectStream[String, String](<...>)
dstream.map(<...>)
<...>

ssc.start()
```

## Importations

​	Those are the necessary imports to work with Kafka 0.10 through Spark:

```scala​
import org.apache.kafka.clients.consumer.ConsumerRecord
import org.apache.kafka.common.serialization.StringDeserializer
import org.apache.spark.streaming.{Seconds, StreamingContext}
import org.apache.spark.streaming.kafka010._
import org.apache.spark.streaming.kafka010.LocationStrategies.PreferConsistent
import org.apache.spark.streaming.kafka010.ConsumerStrategies.Subscribe
```

## Kafka Parameters

​	Now, we will config Kafka API. To do so, these are the minimum required parameters to be defined:

```scala
val kafkaParams = Map[String, Object](
    "bootstrap.servers" -> "localhost:9092",  // or "kafka:9092"
    "key.deserializer" -> classOf[StringDeserializer],
    "value.deserializer" -> classOf[StringDeserializer],
    "group.id" -> "app-test",
    "auto.offset.reset" -> "earliest",
    "enable.auto.commit" -> (false: java.lang.Boolean)
)
```
