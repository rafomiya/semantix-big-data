# Hashs

​	Hash is a data structure based on a key-value values.

## Set

- `hset <key> <field> <value>`: set one field.
- `hmset <key> <field1> <value1> ... <fieldn> <valuen>`: set multiple fields.

## Get

- `hget <key> <field>`: get one field.
- `hmget <key> <field1> ... <fieldn>`: get multiple fields.
- `hgetall <key>`: get all fields.

## Increment

​	It is possible to increment values of a hash field using the `hincrby` command.

```bash
hincrby <key> <field> <increment>
```

## Other options

- `hlen <key>`: returns the amount of fields.
- `hstrlen <key> <field>`: return the length of the string inside the field.
- `hkeys <key>`: returns all the fields of the hash.
- `hvals <key>`: returns all the values of the hash.
- `hdel <key> <field>`: deletes a field of the hash.
