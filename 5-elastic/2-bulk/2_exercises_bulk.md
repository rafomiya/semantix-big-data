# Exercises - Bulk API

1. Import the data from the directory `dataset`:

- Index: dealership2
    - `dataset/cars.bulk`
- Index: population
    - `dataset/populacaoLA.csv`

```bash
# Done through the Kibana GUI
```

2. Execute the queries:

- Count the amount of documents in each of the new indexes.

```bash
GET dealership2/_count
# output:
# {
#   "count" : 16,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   }
# }
GET population/_count
# output:
# {
#   "count" : 319,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   }
# }
```

- Show all the documents of each of the new indexes.

```bash
GET populatiop2/_search
GET population/_search
```
