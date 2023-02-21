# Managing Indexes

- Create;
- Get;
- Verify if exists;
- Delete;
- Open/close Index API.

## Create

​	When creating a new index, we will use the command `PUT`.
​	An index creation requires three principal parameters:

- `settings`
- `mappings`
- `aliases`

```bash
PUT client
{
  "settings": {
    "index": {
      "number_of_shards": 1, # default value
      "number_of_replicas": 1 # default value
    }
  },
  "mappings": {...},
  "aliases": {...}
}
```

​	It is recommended that each shard has from 20GB to 50GB.

## Get

​	Retrieve informations about the index:

```bash
GET client
GET client/_search
GET client/_settings
GET client/_mapping
GET client/_alias
GET client/_stats
```

​	Verify if it exists:

```bash
HEAD client
```

## Delete

```bash
DELETE client
```

## Open/Close

​	When an index is closed, it doesn't accept read/write requests. The only data available are its metadata, such as `settings` and `mappings`.

​	Open/close:

```bash
POST client/_open
POST client/_close
```
