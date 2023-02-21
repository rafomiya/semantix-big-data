# Exercises - Search Order

Do all the following searches on the index `product`.

1. Search all the documents containing the words `"Windows"` and `"Linux"` on the attribute `description`.

```bash
GET product/_search
{
  "query": {
    "match": {
      "description": {
        "query": "Windows Linux",
        "operator": "and"
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
#     "max_score" : 1.5408392,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.5408392,
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

2. Search all the documents containing the words `"Windows"`, `"Linux"` or `"USB"` on the attribute `description`.

```bash
GET product/_search
{
  "query": {
    "match": {
      "description": "Windows Mac USB"
    }
  }
}
# output:
# {
#   "took" : 2,
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
#     "max_score" : 1.8305303,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.8305303,
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
#         "_score" : 1.1706734,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
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
#       }
#     ]
#   }
# }
```

3. Search all the documents containing at least 2 words of the following list: `["Windows", "Linux", "USB"]` (on the attribute `description`).

```bash
GET product/_search
{
  "query": {
    "match": {
      "description": {
        "query": "Windows Linux USB",
        "minimum_should_match": 2
      }
    }
  }
}
# output:
# {
#   "took" : 4,
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
#     "max_score" : 1.8305303,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.8305303,
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
#         "_score" : 1.1706734,
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

4. Search all the documents containing at least 50% of the following list of words: `["Windows", "Linux", "USB"]` (on the attribute `description`).

```bash
GET product/_search
{
  "query": {
    "match": {
      "description": {
        "query": "Windows Linux USB",
        "minimum_should_match": "50%"
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
#       "value" : 3,
#       "relation" : "eq"
#     },
#     "max_score" : 1.8305303,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.8305303,
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
#         "_score" : 1.1706734,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
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
#       }
#     ]
#   }
# }
```
