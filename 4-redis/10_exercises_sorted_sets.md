# Exercises - Sorted sets

1. Delete the key `"search:product"`

```bash
del search:product
# output:
# (integer) 1
```

2. Create the key `"search:product"` of type sorted set with the following values:

- Value: `"monitor"`; Score: 100.
- Value: `"HD"`; Score: 20.
- Value: `"mouse"`; Score: 10.
- Value: `"keyboard"`; Score: 50.

```bash
zadd search:product 100 monitor 20 HD 10 mouse 50 keyboard
# output:
# (integer) 4
```

OBS: The score represents the amount of searchs made for that product on the application.

3. Visualize the amount of products.

```bash
zcard search:product
# output:
# (integer) 4
```

4. Visualize all the products, from the most searched to the least searched.

```bash
zrange search:product 0 -1
# output:
# 1) "mouse"
# 2) "HD"
# 3) "keyboard"
# 4) "monitor"
```

5. Visualize the rank of the product `"keyboard"`.

```bash
zrank search:product keyboard
# output:
# (integer) 2
```

6. Visualize the score of the product `"keyboard"`.

```bash
zscore search:product keyboard
# output:
# "50"
```

7. Remove the value `"HD"` from the key.

```bash
zrem search:product HD
# output:
# (integer) 1
```

8. Recover and remove the most searched product from the set.

```bash
zpopmax search:product
# output:
# 1) "monitor"
# 2) "100"
```

9. Recover and remove the least searched product from the set.

```bash
zpopmin search:product
# output:
# 1) "mouse"
# 2) "10"
```

10. Visualize all the products.

```bash
zrange search:product 0 -1
# output:
# 1) "keyboard"
```
