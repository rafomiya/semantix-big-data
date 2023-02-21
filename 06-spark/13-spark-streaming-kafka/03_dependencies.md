# Dependencies working with Spark Streaming & Kafka 0.10

​	This part of this course is only available with Scala, not with Python.

​	First of all, we need to add Kafka's package:

​	On spark-shell:

```bash
spark-shell --packages org.apache.spark:spark-streaming-kafka-0-10_2.11:2.4.1
```

​	Scala SBT:

```scala
libraryDependencies += "org.apache.spark" % "spark-streaming-kafka-0-10" % "2.4.1"
```
