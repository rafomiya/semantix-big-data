# Pub/Sub

​	Message paradigm that stands for publish/subscribe.

- There is a publisher, who sends the message through a channel.
- There is a subscriber, who receives the message.

​	The publisher doesn't know the subscribers.

## Pub/sub in Redis

- `publish <channel> <message>`: publishs the message on the channel.
- `subscribe <channel1> ... <channeln>`: subscribes to receive the messages from the channel(s).
- `psubscribe <pattern1> ... <patternn>`: subscribes to receive messages from all the channels matching the given pattern(s).
- `unsubscribe <channel1> ... <channeln>`: unsubscribes from the specified channel(s). If none is specified, it unsubscribes from all the channels.
- `punsubscribe <pattern1> ... <patternn>`: unsubscribes from all the channels mmatching the given pattern(s).
