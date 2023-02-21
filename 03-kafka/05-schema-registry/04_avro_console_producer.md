# Avro Console Producer

​	`kafka-avro-console-producer` is a tool that allows you to send data quickly through the manually. Differently from the `kafka-avro-console-consumer`, the `kafka-avro-console-producer` requires an id of the schema of the data.

## Create a schema

```bash
# inside the schema-registry
kafka-avro-console-producer \
--broker-list broker:29092 \
--topic test-avro \
--property schema.registry.url=http://localhost:8081 \
--property value.schema= '{"type":"record","name":"myrecord","fields":[{"name":"id","type":"int"},{"name":"name", "type":"string"}]}'
# cursor waiting for a input
>{"id": 1, "name": "Rafael"}
>{"id": 2, "name": "Ronald"}
```

## Evolve a schema

​	When adding new fields, you need to specify a `default` value for that field. This value will be placed on all the 

```bash
kafka-avro-console-producer \
--broker-list broker:29092 \
--topic test-avro \
--property schema.registry.url=http://localhost:8081 \
--property value.schema= '{"type":"record","name":"myrecord","fields":[{"name":"id","type":"int"},{"name":"name", "type":"string"},{"name":"city","type":"string","default":"null"}]}'
>{"id": 3, "name": "Richard", "city": "New York"}
>{"id": 4, "name": "Robert", "city": "New Jersey"}
```

​	In the above example, the fields where `id=1` or `id=2` will have the `city` set to `null`.
