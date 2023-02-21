# Avro Streams

​	When creating a KSQL Stream with an Avro schema already defined on the Schema Registry, we can do as follows:

```sql
create stream avro_stream with
(
	kafka_topic='test-avro',
    value_format='avro'
);
```

​	Since the schema is already defined, we don't need to pass it again on the creation of the stream.
