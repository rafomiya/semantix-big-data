# Exercises - Indexes

1. Visualize the settings of the index `product`.

```bash
GET product/_settings
# output:
# {
#   "product" : {
#     "settings" : {
#       "index" : {
#         "creation_date" : "1648697537801",
#         "number_of_shards" : "1",
#         "number_of_replicas" : "1",
#         "uuid" : "7LkiRZOpRPKzL0NKGpswkQ",
#         "version" : {
#           "created" : "7090299"
#         },
#         "provided_name" : "product"
#       }
#     }
#   }
# }
```

2. Visualize the mapping of the index `product`.

```bash
GET product/_mapping
# output:
# {
#   "product" : {
#     "mappings" : {
#       "properties" : {
#         "description" : {
#           "type" : "text",
#           "fields" : {
#             "keyword" : {
#               "type" : "keyword",
#               "ignore_above" : 256
#             }
#           }
#         },
#         "name" : {
#           "type" : "text",
#           "fields" : {
#             "keyword" : {
#               "type" : "keyword",
#               "ignore_above" : 256
#             }
#           }
#         },
#         "quantity" : {
#           "type" : "long"
#         }
#       }
#     }
#   }
# }
```

3. Visualize the mapping of attribute `name` from the index `product`.

```bash
GET product/_mapping/field/name
# output:
# {
#   "product" : {
#     "mappings" : {
#       "name" : {
#         "full_name" : "name",
#         "mapping" : {
#           "name" : {
#             "type" : "text",
#             "fields" : {
#               "keyword" : {
#                 "type" : "keyword",
#                 "ignore_above" : 256
#               }
#             }
#           }
#         }
#       }
#     }
#   }
# }
```

4. Insert the field `date` of type `date` on the index `product`.

```bash
PUT product/_mapping
{
  "properties": {
    "date": { "type": "date" }
  }
}
# output:
# {
#   "acknowledged" : true
# }
```

5. Add the document:

- `"_id": 6`
    - `"name": "keyboard"`
    - `"quantity": 100`
    - `"description": "USB"`
    - `"date": "2020-09-18"`
    
```bash
POST product/_doc/6
{
  "name": "keyboard",
  "quantity": 100,
  "description": "USB",
  "date": "2020-09-18"
}
# output:
# {
#   "_index" : "product",
#   "_type" : "_doc",
#   "_id" : "6",
#   "_version" : 1,
#   "result" : "created",
#   "_shards" : {
#     "total" : 2,
#     "successful" : 1,
#     "failed" : 0
#   },
#   "_seq_no" : 8,
#   "_primary_term" : 6
# }
```

6. Reindex the index `product` to `product2`, with the field `quantity` as `short`.

```bash
# creating the `dest` index
PUT product2
{
  "mappings": {
    "properties" : {
      "description" : {
        "type" : "text",
        "fields" : {
          "keyword" : {
            "type" : "keyword",
            "ignore_above" : 256
          }
        }
      },
      "name" : {
        "type" : "text",
        "fields" : {
          "keyword" : {
            "type" : "keyword",
            "ignore_above" : 256
          }
        }
      },
      "quantity" : {
        "type" : "short"
      }
    }
  }
}
# output:
# {
#   "acknowledged" : true,
#   "shards_acknowledged" : true,
#   "index" : "product2"
# }

# reindexing
POST _reindex
{
  "source": {
    "index": "product"
  },
  "dest": {
    "index": "product2"
  }
}
# output:
# {
#   "took" : 51,
#   "timed_out" : false,
#   "total" : 4,
#   "updated" : 0,
#   "created" : 4,
#   "deleted" : 0,
#   "batches" : 1,
#   "version_conflicts" : 0,
#   "noops" : 0,
#   "retries" : {
#     "bulk" : 0,
#     "search" : 0
#   },
#   "throttled_millis" : 0,
#   "requests_per_second" : -1.0,
#   "throttled_until_millis" : 0,
#   "failures" : [ ]
# }
```

7. Visualize the mapping of the index `product2`.

```bash
GET product2/_mapping
# output:
# {
#   "product2" : {
#     "mappings" : {
#       "properties" : {
#         "date" : {
#           "type" : "date"
#         },
#         "description" : {
#           "type" : "text",
#           "fields" : {
#             "keyword" : {
#               "type" : "keyword",
#               "ignore_above" : 256
#             }
#           }
#         },
#         "name" : {
#           "type" : "text",
#           "fields" : {
#             "keyword" : {
#               "type" : "keyword",
#               "ignore_above" : 256
#             }
#           }
#         },
#         "quantity" : {
#           "type" : "short"
#         }
#       }
#     }
#   }
# }
```

8. Close the index `product`.

```bash
POTS product/_close
# output:
# {
#   "acknowledged" : true,
#   "shards_acknowledged" : true,
#   "indices" : {
#     "product" : {
#       "closed" : true
#     }
#   }
# }
```

9. Search all the documents of the index `product`.

```bash
GET product/_search
# output:
# {
#   "error" : {
#     "root_cause" : [
#       {
#         "type" : "index_closed_exception",
#         "reason" : "closed",
#         "index_uuid" : "7LkiRZOpRPKzL0NKGpswkQ",
#         "index" : "product"
#       }
#     ],
#     "type" : "index_closed_exception",
#     "reason" : "closed",
#     "index_uuid" : "7LkiRZOpRPKzL0NKGpswkQ",
#     "index" : "product"
#   },
#   "status" : 400
# }
```

10. Open the index `product`.

```bash
POST product/_open
# output:
# {
#   "acknowledged" : true,
#   "shards_acknowledged" : true
# }
```
