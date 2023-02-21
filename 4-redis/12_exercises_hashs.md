# Exercises - Hashs

1. Delete the key `"user:100"`.

```bash
del user:100
# output:
# (integer) 0
```

2. Create the key `"user:100"` of type hash with the following fields:

- `"name"`: `"Augusto"`
- `"state"`: `"SP"`
- `"views"`: `10`

```bash
hset user:100 name Augusto state SP views 10
# output:
# (integer) 3
```

3. Visualize all the keys and values.

```bash
hgetall user:100
# output:
# 1) "name"
# 2) "Augusto"
# 3) "state"
# 4) "SP"
# 5) "views"
# 6) "10"
```

4. Count the amount of fields.

```bash
hlen user:100
# output:
# (integer) 3
```

5. Visualize only the `"name"` and `"views"`.

```bash
hmget user:100 name views
# output:
# 1) "Augusto"
# 2) "10"
```

6. Count the length of the value inside the `"name"`.

```bash
hstrlen user:100 name
# output:
# (integer) 7
```

7. Increment in 2 the value of the field `"views"`.

```bash
hincrby user:100 views 2
# output:
# (integer) 12
```

8. Visualize only the fields.

```bash
hkeys user:100
# output:
# 1) "name"
# 2) "state"
# 3) "views"
```

9. Visualize only the values.

```bash
hvals user:100
# output:
# 1) "Augusto"
# 2) "SP"
# 3) "12"
```

10. Delete the field `"state"`.

```bash
hdel user:100 state
# output:
# (integer) 1
```

