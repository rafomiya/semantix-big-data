# Exercises - Bool Query

Do all the following exercises on the index `product`.

1. Search on the term `name` the value `"mouse"`.

```bash
GET product/_search
{
  "query": {
    "term": { "name": "mouse" }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 1,
#       "relation" : "eq"
#     },
#     "max_score" : 1.3112575,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.3112575,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }
```

2. Search on the term `name` the values `"mouse"` and `"keyboard"`.

```bash
GET product/_search
{
  "query": {
    "terms": {
      "name": ["mouse", "keyboard"]
    }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 2,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "6",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "keyboard",
#           "quantity" : 100,
#           "description" : "USB",
#           "date" : "2020-09-18"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }
```

3. Redo the searches from items 1 and 2, desconsindering the `_score`.

```bash
GET product/_search
{
  "query": {
    "constant_score": {
      "filter": {
        "term": {
          "name": "mouse"
        }
      }
    }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 1,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }

GET product/_search
{
  "query": {
    "constant_score": {
      "filter": {
        "terms": {
            "name": ["mouse", "keyboard"]
        }
      }
    }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 2,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "6",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "keyboard",
#           "quantity" : 100,
#           "description" : "USB",
#           "date" : "2020-09-18"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }
```

4. Search all the documents that contains the word `"USB"` on the attribute `description`.

```bash
GET product/_search
{
  "query": {
    "match": {
      "description": "USB"
    }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 3,
#       "relation" : "eq"
#     },
#     "max_score" : 0.53873885,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "6",
#         "_score" : 0.53873885,
#         "_source" : {
#           "name" : "keyboard",
#           "quantity" : 100,
#           "description" : "USB",
#           "date" : "2020-09-18"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 0.28969106,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "2",
#         "_score" : 0.2596799,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
#         }
#       }
#     ]
#   }
# }
```

5. Search all the documents that contains the word `"USB"` and don't contains the word `"Linux"` on the attribute description.

```bash
GET product/_search
{
  "query": {
    "bool": {
      "must_not": {
        "match": {
          "description": "Linux"
        }
      },
      "must": [
        {
          "match": {
            "description": "USB"
          }
        }
      ]
    }
  }
}
# output:
# {
#   "took" : 1,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 2,
#       "relation" : "eq"
#     },
#     "max_score" : 0.53873885,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "6",
#         "_score" : 0.53873885,
#         "_source" : {
#           "name" : "keyboard",
#           "quantity" : 100,
#           "description" : "USB",
#           "date" : "2020-09-18"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "2",
#         "_score" : 0.2596799,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
#         }
#       }
#     ]
#   }
# }
```

6. Search all the documents that can have the word `"memória"` on the attribute `name` or contains the word `"USB"` and don't contains the word `"Linux"` on the attribute description.

```bash
GET product/_search
{
  "query": {
    "bool": {
      "should": [
        {
          "match": {
            "name": "memória"
          }
        },
        {
          "match": {
            "description": "USB"
          }
        }
      ],
      "must_not": [
        {
          "match": {
            "description": "Linux"
          }
        }
      ]
    }
  }
}
# output:
# {
#   "took" : 0,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 3,
#       "relation" : "eq"
#     },
#     "max_score" : 0.9666934,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "3",
#         "_score" : 0.9666934,
#         "_source" : {
#           "name" : "memória ram",
#           "quantity" : 30,
#           "description" : "8GB, DDR4"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "6",
#         "_score" : 0.53873885,
#         "_source" : {
#           "name" : "keyboard",
#           "quantity" : 100,
#           "description" : "USB",
#           "date" : "2020-09-18"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "2",
#         "_score" : 0.2596799,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
#         }
#       }
#     ]
#   }
# }
```

