# Exercises - List

1. Create the key "views:last_user" and insert, in this order, the following values as a list:

- Final da lista `"Joao"`
- Final da lista `"Ana"`
- Inicio da lista `"Carlos"`
- Final da lista `"Carol"`

```bash
lpush views:last_user Joao Ana
# output:
# (integer) 2

rpush views:last_user Carlos
# output:
# (integer) 3

lpush views:last_user Carol
# output:
# (integer) 4
```

2. Visualize all the elements from the list.

```bash
lrange views:last_user 0 -1
# output:
# 1) "Carol"
# 2) "Ana"
# 3) "Joao"
# 4) "Carlos"
```

3. Visualize all the elements from the list, except for the last.

```bash
lrange views:last_user 0 -2
# 1) "Carol"
# 2) "Ana"
# 3) "Joao"
```

4. Visualize the list's length.

```bash
llen views:last_user
# output:
# (integer) 4
```

5. Redefine the list's length, removing the first element (not using pop).

```bash
ltrim views:last_user 1 -1
# output:
# OK
```

6. Visualize the list's length once again.

```bash
llen views:last_user
# output:
# (integer) 3
```

7. Recover the elements from the list, on the following order:

- First
- Last
- First with a delay of 5 seconds if the list is empty
- First with a delay of 5 seconds if the list is empty

```bash
lpop views:last_user
# output:
# "Ana"

rpop views:last_user
# output:
# "Carlos"

blpop views:last_user 5
# output:
# 1) "views:last_user"
# 2) "Joao"

blpop views:last_user 5
# output:
# (nil)
# (5.06s)
```
