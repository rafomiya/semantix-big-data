# Exercises - String

1. Create the key `"user:name"` with the value of `"Rafael"`.

```bash
set user:name Rafael
# output:
# OK
```

2. Create the key `"user:surname"` with the value of `"Omiya"`.

```bash
set user:surname Omiya
# output:

```

3. Search for the key `"user:name"`.

```bash
get user:name
# output:
# OK
```

4. Verify the length of the key `"user:name"`.

```bash
strlen user:name
# output:
# (integer) 6
```

5. Verify the type of the key `"user:surname"`.

```bash
type user:surname
# output:
# string
```

6. Create the key `"views:quantity"` with the value of `100`.

```bash
set views:quantity 100
# output:
# OK
```

7. Increment the value of the key `"views:quantity"` with 10.

```bash
incrby views:quantity 10
# output:
# (integer) 110
```

8. Search for the key `"views:quantity"`.

```bash
get views:quantity
# output:
# "110"
```

9. Delete the key `"user:surname"`.

```bash
del user:surname
# output:
# (integer) 1
```

10. Verify if the key `"user:surname"` exists.

```bash
exists user:surname
# output:
# (integer) 0
```

11. Define a time of 3600 seconsd to the key `"views:quantity"` to expire.

```bash
expire views:quantity 3600
# output:
# (integer) 1
```

12. Verify how much time is left for the key `"views:quantity"` to expire.

```bash
ttl views:quantity
# output:
# (integer) 3586
```

13. Verify the persistency of the key `user:name`.

```bash
ttl user:name
# output:
# (integer) -1
```

14. Define the key `"views:quantity"` to be persistent forever.

```bash
persist views:quantity
# output:
# (integer) 1
```
