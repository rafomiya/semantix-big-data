# Kafka Commands

​	All the commands shown bellow are executed on the broker of a Kafka cluster.

## Topics

- `kafka-topics --bootstrap-server localhost:9092 --list`: list topics.
- `kafka-topics --bootstrap-server localhost:9092 --topic <topicname> --create --partitions <numberp> --replication-factor 1`: creates a topic.
- `kafka-topics --bootstrap-server localhost:9092 --topic <topicname> --describe`: describes a topic.
- `kafka-topics --bootstrap-server localhost:9092 --topic <topicname> --delete`: deletes a topic.

## Producers

- `kafka-console-producer --broker-list localhost:9092 --topic <topicname>`: sends the `data` to the specified topic, inside the `localhost:9092` broker.
- `kafka-console-producer --broker-list localhost:9092 --topic <topicname> --producer-property acks=all`: does the same thing as the previous item, but with `acks=all`.

​	Note that we didn't had to specify to which partition the data is being sent. That is because Kafka will already try to balance the size of the partitions by default.

## Consumers

- `kafka-console-consumer --bootstrap-server localhost:9092 --topic <topicname>`: receives messages in real time.
- `kafka-console-consumer --bootstrap-server localhost:9092 --topic <topicname> --from-beginning`: receives messages since the creation of the topic.
- `kafka-console-consumer --bootstrap-server localhost:9092 --topic <topicname> --group <groupname>`: creates a consumer group.

### Consumer groups

- `kafka-consumer-groups --bootstrap-server localhost:9092 --list`: list groups.
- `kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group <groupname>`: describes a group.
- `kafka-consumer-groups --bootstrap-server localhost:9092 --group <groupname> --reset-offsets --to-earliest --execute --topic <topicname>`: redefines the reading to the first message of the topic.
- `kafka-consumer-groups --bootstrap-server localhost:9092 --group <groupname> --reset-offsets --shift-by <number> --execute --topic <topicname>`: change the shifts the reading to the specified number.