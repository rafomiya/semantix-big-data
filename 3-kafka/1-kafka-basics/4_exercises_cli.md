# Exercises - Kafka CLI

1. Create the topic `msg-cli` with 2 partitions and 1 replica.

```bash
# Terminal A
kafka-topics --bootstrap-server localhost:9092 --topic msg-cli --create --partitions 2 --replication-factor 1
# output:
# Created topic msg-cli.
```

2. Describe the topic `msg-cli`.

```bash
# Terminal A
kafka-topics --bootstrap-server localhost:9092 --topic msg-cli --describe
# output:
# Topic: msg-cli  PartitionCount: 2       ReplicationFactor: 1    Configs: 
#         Topic: msg-cli  Partition: 0    Leader: 1       Replicas: 1     Isr: 1  Offline: 
#         Topic: msg-cli  Partition: 1    Leader: 1       Replicas: 1     Isr: 1  Offline:
```

3. Create the consumer from the group `app-cli`.

```bash
# Terminal A
kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli
# output (after exercise 4):
# Msg 1
# Msg 2
```

4. Send the following messages from the producer.

- Msg 1
- Msg 2

```bash
# Terminal B:
kafka-console-producer --broker-list localhost:9092 --topic msg-cli
>Msg 1
>Msg 2
```

5. Create other consumer from the group `app-cli`.

```bash
# Terminal C
kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli
```

6. Send the following messages from the producer.

- Msg 4
- Msg 5
- Msg 6
- Msg 7

```bash
# Terminal B
>Msg 4
>Msg 5
>Msg 6
>Msg 7
```

7. Create other consumer from the group `app2-cli`.

```bash
# Terminal D
kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app2-cli
```

8. Send the following messages from the producer.

- Msg 8
- Msg 9
- Msg 10
- Msg 11

```bash
# Terminal B
>Msg 8
>Msg 9
>Msg 10
>Msg 11
```

9. Stop the `app-cli`

```bash
^C
# output:
# Processed a total of 10 messages
```

10. Define the shift to `-2` offsets on `app-cli`.

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --reset-offsets --shift-by -2 --execute --topic msg-cli --group app-cli
# output:
# 
# GROUP                          TOPIC                          PARTITION  NEW-OFFSET     
# app-cli                        msg-cli                        0          4              
# app-cli                        msg-cli                        1          2              
```

11. Describe the group.

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group app-cli
# output:
# 
# Consumer group 'app-cli' has no active members.
# 
# GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
# app-cli         msg-cli         0          4               6               2               -               -               -
# app-cli         msg-cli         1          2               4               2               -               -               -
```

12. Start the `app-cli`.

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --group app-cli --topic msg-cli
# Msg 9
# Msg 10
# Msg 7
# Msg 11
```

13. Redefine the shift on `app-cli`.

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --group app-cli --topic msg-cli --reset-offsets --to-earliest --execute
# output:
# 
# GROUP                          TOPIC                          PARTITION  NEW-OFFSET     
# app-cli                        msg-cli                        0          0              
# app-cli                        msg-cli                        1          0  
```

14. Start the `app-cli`.

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --group app-cli --topic msg-cli
# output:
# Msg 1
# Msg 4
# Msg 6
# Msg 8
# Msg 9
# Msg 10
# Msg 2
# Msg 5
# Msg 7
# Msg 11
```

15. List the groups.

```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --list
# output:
# 
# app2-cli
# _confluent-controlcenter-5-5-2-1
# _confluent-controlcenter-5-5-2-1-command
# app-cli
```
