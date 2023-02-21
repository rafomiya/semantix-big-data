# String

​	Strings are the only data type memcached. They are commonly used in web pages, as cache.

## `strlen`

​	Outputs the length of the string from the key.

​	Example:

```bash
set loremIpsum dolorSitAmet
# output:
OK

strlen loremIpsum
# output:
(integer) 12
```

## String as an integer

- `incr <key>`: increments 1 on the value from the key.
- `decr <key>`: decrements 1 on the value from the key.
- `incrby <key> <number>`: increments `number` on the value from the key.
- `decrby <key> <number>`: decrements `number` on the value from the key.
