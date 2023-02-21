# Exercises - Pub/Sub

1. Create a subscriber to receive messages from the channel `"news:sp"`.

```bash
subscribe news:sp
# output:
# Reading messages... (press Ctrl-C to quit)
# 1) "subscribe"
# 2) "news:sp"
# 3) (integer) 1
```

2. Create a publisher to send the following messages on the channel `"news:sp"`:

- `"Msg 1"`
- `"Msg 2"`
- `"Msg 3"`

```bash
publish news:sp 'Msg 1'
publish news:sp 'Msg 2'
publish news:sp 'Msg 3'
# output:
# (integer) 1
# (integer) 1
# (integer) 1
```

3. Cancel the subscriber `"news:sp"`.

```bash
# 1) "message"
# 2) "news:sp"
# 3) "Msg 1"
# 1) "message"
# 2) "news:sp"
# 3) "Msg 2"
# 1) "message"
# 2) "news:sp"
# 3) "Msg 3"
^C
```

4. Create a subscriber to receive the messages from the channels with the pattern `"news:*"`.

```bash
psubscribe news:*
# output:
# 1) "psubscribe"
# 2) "news:*"
# 3) (integer) 1
```

5. Create a publisher to send the following messages to the channel `"news:rj"`:

- `"Msg 4"`
- `"Msg 5"`
- `"Msg 6"`

```bash
publish news:rj 'Msg 4'
publish news:rj 'Msg 5'
publish news:rj 'Msg 6'
# output:
# (integer) 1
# (integer) 1
# (integer) 1
```
