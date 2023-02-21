# Understanding key-value

​	Redis stores data within a key-value structure. This structure accepts many data types, such as:

- Strings.
- Lists.
- Sets.
- Ordered sets.
- Hashs.
- HyperLogLogs.
- Streams.

## Data manipulation

​	In Redis, the keys are binary safe. That means that they are binary sequences, and have some predefined rules:

- Max size: 512MB.
  - Not recommended to use keys larger than 1MB.
- Conventionally, we use the format `"<type>:<id>"`. Example: `"user:300"`

### `get` and `set`

​	Basic syntax:

```bash
# set:
set <key> <value>
# output:
# OK

# get:
get <key>
# output:
# <value>
```

#### `set` options

- `nx`: fails if the key already exists.

```bash
# set if the key already exists:
set <key> <newValue> nx
# output:
# (nil)
```

- `xx` (default): replaces the key's value.

```bash
# set if the key already exists:
set <key> <newValue> xx
# output:
# OK
```

#### Multiple `get` or `set`

​	Syntax:

```bash
mget <key1> <value1> <key2> <value2> ... <keyn> <valuen>
mset <key1> <key2> ... <keyn>
```

#### Key persistence

​	It is possible to define an expiration for a specific key:

- If the key already exists:
  - `expire <key> <time>`: time in seconds.
  - `pexpire <key> <time>`: time in milliseconds.
- If the key doesn't exists yet:
  - `set <key> <value> ex <time>`: time in seconds.
  - `set <key> <value> px <time>`: time in milliseconds.

​	To verify the remaining time of a key to expire:

- `ttl <key>`: remaining time in seconds.
- `pttl <key>`: remaining time in milliseconds.

​	To remove the expiration of a key:

```bash
persist <key>
# output:
# (integer) 1
```

#### Other options

- `exists`: returns 0 or 1, whether the key exists or not.
- `type`: returns the type of the value identified by the key.
- `del`: deletes the key and returns 0 or 1, whether it was deleted or not.

```bash
set thisKey thisValue
# output:
# OK

exists thisKey
# output:
# (integer) 1

type thisKey
# output:
# string

del thisKey
# output:
# (integer) 1

get thisKey
# output:
# (nil)

exists thisKey
# output:
# (integer) 0
```
