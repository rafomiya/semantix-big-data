# Exercises - Schema Registry

1. Visualize the data from the topic `users`;

```sql
set 'auto.offset.reset'='earliest';
print 'users';
-- partial output:
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_2, value: {"registertime":1489319256896,"userid":"User_2","regionid":"Region_6","gender":"FEMALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_8, value: {"registertime":1515617157058,"userid":"User_8","regionid":"Region_8","gender":"FEMALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_2, value: {"registertime":1517615408147,"userid":"User_2","regionid":"Region_2","gender":"MALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_3, value: {"registertime":1505589787312,"userid":"User_3","regionid":"Region_4","gender":"FEMALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_2, value: {"registertime":1489739459719,"userid":"User_2","regionid":"Region_6","gender":"MALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_9, value: {"registertime":1515152236936,"userid":"User_9","regionid":"Region_8","gender":"MALE"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_8, value: {"registertime":1509063594980,"userid":"User_8","regionid":"Region_1","gender":"OTHER"}
-- rowtime: 3/13/22 9:10:49 PM UTC, key: User_4, value: {"registertime":1494767204754,"userid":"User_4","regionid":"Region_3","gender":"MALE"}
-- ...
```

2. Create the topic `users-avro`.

```bash
kafka-topics --bootstrap-server localhost:9092 --create --topic users-avro
# output:
# Created topic users-avro.
```

a) Use the `kafka-avro-console-producer` to send  1 menssage.

```bash
kafka-avro-console-producer \
--broker-list http://broker:29092 \
--topic users-avro \
--property schema.registry.url=http://localhost:8081 \
--property value.schema='{"type":"record","name":"users","fields":[{"name":"userid","type":"string"},{"name":"regionid","type":"string"},{"name":"gender","type":"string"}]}'
# input:
{"userid":"User_2","regionid":"Region_1","gender":"OTHER"}
```

b) Use the `kafka-avro-console-consumer` to consume the message.

```bash
kafka-avro-console-consumer \
--bootstrap-server broker:29092 \
--topic users-avro \
--property schema.registry.url=http://localhost:8081 \
--from-beginning
# output:
# {"userid":"User_2","regionid":"Region_1","gender":"OTHER"}
```

3. Visualize the data from `users-avro` on ksqlDB.

```sql
set 'auto.offset.reset'='earliest'
print 'users-avro';
-- output:
-- rowtime: 3/14/22 6:26:06 PM UTC, key: <null>, value: {"userid": "User_2", "regionid": "Region_1", "gender": "OTHER"}
```

4. Create the stream `users_avro1` to the topic `users-avro`.

```sql
create stream users_avro1 with
(
    kafka_topic='users-avro',
    value_format='avro'
);
-- output:
-- 
--  Message        
-- ----------------
--  Stream created 
-- ----------------
```

5. Visualize the data from stream `users-avro1`.

```sql
select * from users-avro1
emit changes
limit 10;
-- +---------------------------------+---------------------------------+---------------------------------+---------------------------------+---------------------------------+
-- |ROWTIME                          |ROWKEY                           |USERID                           |REGIONID                         |GENDER                           |
-- +---------------------------------+---------------------------------+---------------------------------+---------------------------------+---------------------------------+
-- |1647282366441                    |null                             |User_2                           |Region_1                         |OTHER                            |
```

6. Use the `kafka-avro-console-producer` to add a new field called `unit` with the default value of `1`.

```bash
kafka-avro-console-producer \
--broker-list http://broker:29092 \
--topic users-avro \
--property schema.registry.url=http://localhost:8081 \
--property value.schema='{"type":"record","name":"users","fields":[{"name":"userid","type":"string"},{"name":"regionid","type":"string"},{"name":"gender","type":"string"},{"name":"unit","type":"int","default":1}]}'
```

7. Use the `kafka-avro-console-consumer` to consume the messages.

```bash
kafka-avro-console-consumer \
--topic users-avro \
--bootstrap-server broker:29092 \
--property schema.registry.url=http://localhost:8081 \
--from-beginning
# output:
# {"userid":"User_2","regionid":"Region_1","gender":"OTHER"}
```

8. Compare the schemas from `users-avro` on the Control Center.

```json
// output:
{
  "fields": [
    {
      "name": "userid",
      "type": "string"
    },
    {
      "name": "regionid",
      "type": "string"
    },
    {
      "name": "gender",
      "type": "string"
    }
  ],
  "name": "users",
  "type": "record"
}
```

9. Visualize the data from the stream of the topic `users-avro`.

```sql
set 'auto.offset.reset'='earliest';
select * from users_avro1 emit changes limit 10;
```
