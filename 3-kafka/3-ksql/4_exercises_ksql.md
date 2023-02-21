# Exercises - KSQL

1. Create the topic `msg-user-csv`.

```bash
kafka-topics --bootstrap-server localhost:9092 --create --topic msg-user-csv
# output:
# Created topic msg-user-csv.
```

2. Create a producer to send 3 messages containing `id` and `first_name`, delimited by comma, to the topic `msg-user-csv`.

```bash
kafka-console-producer --broker-list localhost:9092 --topic msg-user-csv
>1,Rafael
>2,Gabriel
>3,Daniel
```

3. Visualize the data from the topic `msg-user-csv`.

```bash
kafka-topics --bootstrap-server localhost:9092 --topic msg-user-csv --describe
# output:
# Topic: msg-user-csv     PartitionCount: 1       ReplicationFactor: 1    Configs: 
#         Topic: msg-user-csv     Partition: 0    Leader: 1       Replicas: 1     Isr: 1  Offline: 
```

4. Create the stream `user_csv` to read the data from the topic `msg-user-csv`.

```sql
create stream user_csv
(
    `id` int,
    `first_name` varchar
) with (
    kafka_topic='msg-user-csv',
    value_format='delimited'
);
-- output:
-- {
--   "@type": "currentStatus",
--   "statementText": "create stream user_csv\n(\n    `id` int,\n    `first_name` varchar\n) with (\n    kafka_topic='msg-user-csv',\n    value_format='delimited'\n);",
--   "commandId": "stream/`USER_CSV`/create",
--   "commandStatus": {
--     "status": "SUCCESS",
--     "message": "Stream created"
--   },
--   "commandSequenceNumber": 2,
--   "warnings": []
-- }
```

5. Visualize the stream `user_csv`.

```sql
describe extended user_csv;
-- output:
-- {
--   "@type": "sourceDescription",
--   "statementText": "describe extended user_csv;",
--   "sourceDescription": {
--     "name": "USER_CSV",
--     "windowType": null,
--     "readQueries": [],
--     "writeQueries": [],
--     "fields": [
--       {
--         "name": "ROWTIME",
--         "schema": {
--           "type": "BIGINT",
--           "fields": null,
--           "memberSchema": null
--         }
--       },
--       {
--         "name": "ROWKEY",
--         "schema": {
--           "type": "STRING",
--           "fields": null,
--           "memberSchema": null
--         }
--       },
--       {
--         "name": "id",
--         "schema": {
--           "type": "INTEGER",
--           "fields": null,
--           "memberSchema": null
--         }
--       },
--       {
--         "name": "first_name",
--         "schema": {
--           "type": "STRING",
--           "fields": null,
--           "memberSchema": null
--         }
--       }
--     ],
--     "type": "STREAM",
--     "key": "",
--     "timestamp": "",
--     "statistics": "",
--     "errorStats": "",
--     "extended": true,
--     "keyFormat": "KAFKA",
--     "valueFormat": "DELIMITED",
--     "topic": "msg-user-csv",
--     "partitions": 1,
--     "replication": 1,
--     "statement": "create stream user_csv\n(\n    `id` int,\n    `first_name` varchar\n) with (\n    kafka_topic='msg-user-csv',\n    value_format='delimited'\n);"
--   },
--   "warnings": []
-- }
```

6. Visualize only the `first_name` on the stream `user_csv`.

```sql
select first_name from user_csv;
-- output:
-- {"FIRST_NAME": "Daniel"}
-- {"FIRST_NAME": "Gabriel"}
-- {"FIRST_NAME": "Rafael"}
```
