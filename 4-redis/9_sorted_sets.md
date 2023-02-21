# Sorted Sets

​	Sorted sets are a combination of sets and hashs. They consist in a collection of unique string elements. Each element is associated to a score.

## Add

```bash
zadd <key> <score1> <value1> ... <scoren> <valuen>
```

## Range

​	To visualize elements on a range of the set:

- `zrange <key> <start> <end> [withscores]`: returns the sorted by score in crescent order.
- `zrevrange <key> <start> <end> [withscores]`:  returns the sorted by score in decrescent order.

## Pop

​	Recovers and deletes an element from the set.

- `zpopmax <key>`: pops the element with maximum score.
- `zpopmin <key>`: pops the element with minimum score.
- `bzpopmax <key> <time>`: tries to perform a `zpopmax` during the specified time.
- `bzpopmin <key> <time>`: tries to perform a `zpopmin` during the specified time.

## Other options

- `zrank <key> <value>`: returns the position of the specified element.
- `zrevrank <key> <value>`: performs a reversed `zrank`.
- `zscore <key> <value>`: returns the score of the specified element.
- `zcard <key>`: returns the amount of elements on the set.
- `zrem <key> <value>`: removes the specified element from the set.
