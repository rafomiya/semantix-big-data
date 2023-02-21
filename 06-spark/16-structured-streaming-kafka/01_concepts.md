# Structured Streaming & Kafka

​	The integration of Spark's Structured Streaming and Apache Kafka is available since Spark 2.0.0, but it is recommended to use it only from 2.3 and above.

​	When working with Spark Streaming, we had to follow these steps:

- Set `StreamingContext` parameters.
- Set `kafkaParams` (Kafka parameters).
- Set the DStream for topic consuming.

​	Now, working with Structured Streaming, we need to configure only the dataframe to read the topics.
