# Avro Console Consumer

​	The `kafka-avro-console-consumer` works in a very similar way to the `kafka-console-consumer`. The main difference is that the `kafka-avro-console-consumer` allows you to read the binary data inside Kafka.

​	Access:

```bash
# inside the schema-registry
kafka-avro-console-consumer \
--topic test-avro \
--bootstrap-server broker:29092 \
--property schema.registry.url=http://localhost:8081 \
--from-beginning
```

