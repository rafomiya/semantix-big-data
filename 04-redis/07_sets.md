# Sets

​	Sets are unordered collections of strings, expressing a relation between its items.

## Add

```bash
sadd <key> <value1> <value2> ... <valuen>
```

## Recover elements

```bash
# returns all the elements
smembers <key>

# removes and returns an element from the set
spop <key>
```

## Set operations

- `sismember <key> <value>`: verifies if the element exists on the set.
- `scard <key>`: returns the amount of elements in the set.
- `srem <key>`: removes the specified element from the set.

## Multiple sets operations

- `sinter <key1> ... <keyn>`: intersection of two or more sets.
  - `sinterstore <newkey> <key1> ... <keyn>`: does the same thing, but storing the output on a new key.
- `sdiff <key1> ... <keyn>`: symmetric difference of two or more sets.
  - `sdiffstore <newkey> <key1> ... <keyn>`: does the same thing, but storing the output on a new key.
- `sunion <key1> ... <keyn>`: union of two or more sets.
  - `sunionstore <newkey> <key1> ... <keyn>`: does the same thing, but storing the output on a new key.


