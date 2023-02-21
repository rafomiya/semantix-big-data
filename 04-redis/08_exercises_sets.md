# Exercises - Set

1. Delete the key `"search:product"`

```bash
del search:product
# output:
# (integer) 0
```

2. Create the key `"search:product"` of type set with the following values: `"monitor"`, `"mouse"` e `"keyboard"`.

```bash
sadd search:product monitor mouse keyboard
# output:
# (integer) 3
```

3. Visualize the amount of values inside the key.

```bash
scard search:product
# output:
# (integer) 3
```

4. Return all the elements of the key.

```bash
smembers search:product
# output:
# 1) "mouse"
# 2) "monitor"
# 3) "keyboard"
```

5. Verify if the value `"monitor"` exists.

```bash
exists search:product monitor
# output:
# (integer) 1
```

6. Remove the value `"monitor"`.

```bash
srem search:product monitor
# output:
# (integer) 1
```

7. Recover an element and remove it from the set.

```bash
spop search:product
# output:
# "keyboard"
```

8. Create the key `"search:discount"` of type set with the following values: `"RAM"`, `"monitor"`, `"keyboard"` and `"HD"`.

```bash
sadd search:discount RAM monitor keyboard HD
# output:
# (integer) 4
```

9. On the sets `"search:product"` and `"search:discount"`.

- Visualize the intersection of the sets.

```bash
sinter search:product search:discount
# output:
# (empty array)
```

- Visualize the difference of the sets.

```bash
sdiff search:product search:discount
# output:
# 1) "mouse"
```

- Create the set `"search:product_discount"` with the union of the sets.

```bash
sunionstore search:product_discount search:product search:discount
# output:
# (integer) 5
```
