# Exercises - Operations

1. Create the index `product` and insert the following documents:

- _id: 1
    - name: "mouse"
    - quantity: 50
    - description: "com fio USB, compatível com Windows, Mac e Linux"
- _id: 2
    - name: "hd"
    - quantity: 20
    - description: "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
- _id: 3
    - name: "memória ram"
    - quantity: 10
    - description: "8GB, DDR4"
- _id: 4
    - name: "cpu"
    - quantity: 15
    - description: "i5, 2.5Ghz"

```bash
POST product/_doc/1
{
  "name": "mouse",
  "quantity": 50,
  "description": "com fio USB, compatível com Windows, Mac e Linux"
}
POST product/_doc/2
{
  "name": "hd",
  "quantity": 20,
  "description": "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
}
POST product/_doc/3
{
  "name": "memória ram",
  "quantity": 10,
  "description": "8GB, DDR4"
}
POST product/_doc/4
{
  "name": "cpu",
  "quantity": 15,
  "description": "i5, 2.5Ghz"
}
```

2. Verify if the document with `_id=3` exists.

```bash
HEAD product/_doc/4
# output:
# 200 - OK
```

3. Update the value of the attribute `quantity` to `30` on the document where `_id=3`.

```bash
POST product/_update/3
{
  "doc": {
    "quantity": 30
  }
}
# output:
# {
#   "_index" : "product",
#   "_type" : "_doc",
#   "_id" : "3",
#   "_version" : 2,
#   "result" : "updated",
#   "_shards" : {
#     "total" : 2,
#     "successful" : 1,
#     "failed" : 0
#   },
#   "_seq_no" : 4,
#   "_primary_term" : 1
# }
```

4. Search for the document with `_id=1`.

```bash
GET product/_doc/1
# output:
# {
#   "_index" : "product",
#   "_type" : "_doc",
#   "_id" : "1",
#   "_version" : 1,
#   "_seq_no" : 0,
#   "_primary_term" : 1,
#   "found" : true,
#   "_source" : {
#     "name" : "mouse",
#     "quantity" : 50,
#     "description" : "com fio USB, compatível com Windows, Mac e Linux"
#   }
# }
```

5. Delete the document where `_id=4`.

```bash
DELETE product/_doc/4
# output:
# {
#   "_index" : "product",
#   "_type" : "_doc",
#   "_id" : "1",
#   "_version" : 2,
#   "result" : "deleted",
#   "_shards" : {
#     "total" : 2,
#     "successful" : 1,
#     "failed" : 0
#   },
#   "_seq_no" : 5,
#   "_primary_term" : 1
# }
```

6. Count how many documents exists on the index `product`.

```bash
GET product/_count
# output:
# {
#   "count" : 3,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   }
# }
```
